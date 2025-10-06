---
title: "Đọc metrics của giải pháp predictive scaling"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: "<strong>7.4. </strong>"
---

### Predictive Scaling

Từ những lượng truy cập, công việc mà hệ thống mà chúng ta sẽ nhận và gửi đi mỗi ngày, thì ASG có thể "dự đoán" được lượng truy cập, công việc đó trong khoảng nhiều ngày tới, từ đó giúp cho ASG sẽ phản ứng tốt hơn trong việc khởi tạo và huỷ các instances đi. Thông thường thì Predictive Scaling sẽ dược dùng với các loại scaling khác.

#### Tiến hành cấu hình

Giống ở phần trước, thì mình vẫn sẽ thực hiện scale in thủ công với ASG và chờ cho ASG xoá hết các instances mà dịch vụ này đã tạo.

![7.4.1](/images/7-test-solution/7.4.1.png)

Sau đó là xoá đi chính sách scaling tự động để tránh việc ảnh hưởng tới phần test này.

![7.4.2](/images/7-test-solution/7.4.2.png)

Tiếp theo, vào trong tab **Activity**, kéo xuống phần **Predictive scaling policies** và ấn **Create predictive policy** để tạo mới.

![7.4.3](/images/7-test-solution/7.4.3.png)

Trong biểu mẫu này, chúng ta sẽ cấu hình như sau:

- Policy details
  - Name: `PredictCPUUtilizationAt15Percent` (có thể đặt tên bất kì)
- Turn on scaling: bật **Scale based on forecast**. Với chính sách scaling mang tính dự đoán, thì về bản chất là nó chỉ có dự đoán, nhưng mà chúng ta cũng có thể dùng nó để khởi tạo các instances.

![7.4.4](/images/7-test-solution/7.4.4.png)

Tiếp theo, trong phần **Metric and target utilization**

- Metrics: chọn **Custom metric pair**.
- Load metric: chọn **Custom CloudWatch metric**.
- Scaling metric: chọn **Custom CloudWatch metric**.

Các bạn sẽ thêm các custom metric json như sau

- Với **Load metric**

```json
{
  "CustomizedLoadMetricSpecification": {
    "MetricDataQueries": [
      {
        "Label": "Total CPU Utilization in ASG",
        "Id": "cpu_sum",
        "MetricStat": {
          "Metric": {
            "MetricName": "WSCustomCPUUTILIZATION",
            "Namespace": "FCJ Management Custom Metrics",
            "Dimensions": [
              {
                "Name": "AutoScalingGroupName",
                "Value": "FCJ-Management-ASG"
              }
            ]
          },
          "Stat": "Sum"
        },
        "ReturnData": true
      }
    ]
  }
}
```

- Với **Scaling metric**

```json
{
  "CustomizedScalingMetricSpecification": {
    "MetricDataQueries": [
      {
        "Label": "Average CPU Utilization in ASG",
        "Id": "cpu_avg",
        "MetricStat": {
          "Metric": {
            "MetricName": "WSCustomCPUUTILIZATION",
            "Namespace": "FCJ Management Custom Metrics",
            "Dimensions": [
              {
                "Name": "AutoScalingGroupName",
                "Value": "FCJ-Management-ASG"
              }
            ]
          },
          "Stat": "Average"
        },
        "ReturnData": true
      }
    ]
  }
}
```

![7.4.5](/images/7-test-solution/7.4.5.png)

Tiếp theo là tích chọn **Add custom capacity metric**.

Và tương tự như 2 bước ở trên, mình sẽ thêm custom metric json cho **Capacity metric**

```json
{
  "CustomizedCapacityMetricSpecification": {
    "MetricDataQueries": [
      {
        "Label": "Number of instances in ASG",
        "Id": "capacity_avg",
        "MetricStat": {
          "Metric": {
            "MetricName": "WSCustomGroupInstances",
            "Namespace": "FCJ Management Custom Metrics",
            "Dimensions": [
              {
                "Name": "AutoScalingGroupName",
                "Value": "FCJ-Management-ASG"
              }
            ]
          },
          "Stat": "Average"
        },
        "ReturnData": true
      }
    ]
  }
}
```

![7.4.6](/images/7-test-solution/7.4.6.png)

{{% notice info %}}
Nếu như bạn có cấu hình ở bước **2.6 - Prepare metrics for predictive scaling** trước đó, thì sau khi cấu hình xong, bạn sẽ thấy được 2 biểu đồ được hiển thị.
{{% /notice %}}

Ở phần **Pre-launch instances** trong phần **Additional scaling settings - optional**, chỉnh xuống **1 minutes**. Ấn **Create** để tạo.

![7.4.7](/images/7-test-solution/7.4.7.png)

{{% notice info %}}
Giống với Dynamic, thì thông số Pre-launch instances này cũng sẽ ảnh hưởng tới thời điểm mà các instances sẽ được khởi tạo. Ví dụ như ASG dự đoán là lúc 23:00 giờ cao điểm, thì ASG sẽ dựa vào thông số này và tạo instance vào lúc 22:59 phút, theo như cấu hình.
{{% /notice %}}

Kiểm tra lại kết quả

![7.4.8](/images/7-test-solution/7.4.8.png)

#### Đọc metric từ dữ liệu mẫu

Vào trong chính sách đó, chúng ta sẽ đọc được 2 biểu đồ là **Load** và **Capacity**. Biểu đồ này cung cấp cho chúng ta về dữ liệu của các lưu lượng cũng như là số các instance đã dùng trong các ngày trước đó, từ đó thì nó đưa ra được dự đoán của các ngày tiếp theo, đươc biểu diễn bằng đường màu tím.

![7.4.9](/images/7-test-solution/7.4.9.png)

{{% notice tip %}}
Biểu đồ được lấy theo giờ UTC + 0, và chúng ta đang ở múi giờ +7 nên chúng ta sẽ cần phải thêm 7 khi đọc các biểu đồ này.
{{% /notice %}}

Trước tiên, tập chung vào biểu đồ ở bên trái trước, vào thời điểm 09:00 (theo giờ của Việt Nam là 26:00) thì lượng chịu tải tổng là **773.542**.

![7.4.10](/images/7-test-solution/7.4.10.png)

Và để hiểu được thông số trên là của cái gì thì chúng ta nhìn qua biểu đồ bên phải.

![7.4.11](/images/7-test-solution/7.4.11.png)

Chúng ta có thể thấy là vào thời điểm đó thì dự đoán sẽ có 13 instance được khởi tạo, và lượng tải dữ liệu kia sẽ tương ứng với số các instance đó.

Chúng ta có thể xem các thời điểm khác.

![7.4.12](/images/7-test-solution/7.4.12.png)

![7.4.13](/images/7-test-solution/7.4.13.png)

Nếu bạn có thể chờ được thời điểm được dự báo, thì vào trong phần tab Activity của ASG, chúng ta sẽ thấy được là ASG khởi tạo một instance mới vào lúc 15:59, 1 phút trước thời điểm 16:00 như đã dự đoán ở trên.

![7.4.14](/images/7-test-solution/7.4.14.png)

#### Kết luận

Chúng ta có thể kết hợp Predictive scaling với Dynamic scaling hoặc là các loại scaling khác để tăng độ linh hoạt cho ASG cũng như là độ tin cậy của hệ thống. Hệ thống nào cho lượng tải đồng đều theo thời gian thì sử dụng predictive để dự đoán cũng rất hợp lý.
