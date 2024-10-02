---
title: "Chuẩn bị các metric cho Predictive scaling"
date: "`r Sys.Date()`"
weight: 6
chapter: false
pre: "<strong>2.6. </strong>"
---

### Chuẩn bị dữ liệu cho Predictive scaling

Bởi vì Predictive scaling cần phải có một lượng dữ liệu trong vòng hơn 2 ngày để có thể đưa ra được các dự đoán vào các ngày tiếp theo, mà ở đây chúng ta lại không có các dữ liệu đó cho nên là chúng ta sẽ cần phải chuẩn bị để giải lập một môi trường như thế.

### Các bước chuẩn bị

Đầu tên là chúng ta sẽ tạo một folder mới với tên là `metric-preparation` và chuyển vào trong thư mục này

```bash
mkdir metric-preparation && cd metric-preparation
```

Sau đó là tải kịch bản để chuẩn bị các dữ liệu

```bash
curl -o prepare-metric-data.sh https://raw.githubusercontent.com/awslabs/ec2-spot-workshops/master/workshops/efficient-and-resilient-ec2-auto-scaling/prepare-metric-data.sh
```

![2.6.1.png](/images/2-preparation/2.6-prepare-metric-data/2.6.1.png)

Sau khi tải xong thì vào trong để thay đổi phần câu lệnh trong kịch bản này lại một xíu

```bash
vim prepare-metric-data.sh
```

![2.6.2.png](/images/2-preparation/2.6-prepare-metric-data/2.6.2.png)

Sau khi chỉnh sửa xong thì giờ chúng ta tiến hành tải các dữ liệu chưa qua xử lý, đó là lý do vì sao mà chúng ta cần tải kịch bản xử lý dữ liệu này trước. Trước tiên là metric cho các instances.

```bash
curl -o metric-cpu.json https://raw.githubusercontent.com/awslabs/ec2-spot-workshops/master/workshops/efficient-and-resilient-ec2-auto-scaling/metric-cpu.json
```

![2.6.3.png](/images/2-preparation/2.6-prepare-metric-data/2.6.3.png)

Tiếp theo là dữ liệu cho CPU

```bash
curl -o metric-cpu.json https://raw.githubusercontent.com/awslabs/ec2-spot-workshops/master/workshops/efficient-and-resilient-ec2-auto-scaling/metric-cpu.json
```

![2.6.4.png](/images/2-preparation/2.6-prepare-metric-data/2.6.4.png)

Tiến hành sửa đổi lần lượt 2 loại dữ liệu này, đầu tiên là cho CPU trước

```bash
bash prepare-metric-data.sh metric-cpu.json FCJ-Management-ASG && cat metric-cpu.json
```

![2.6.5.png](/images/2-preparation/2.6-prepare-metric-data/2.6.5.png)

Tiếp theo là cho instances

```bash
bash prepare-metric-data.sh metric-instances.json FCJ-Management-ASG && cat metric-instances.json
```

![2.6.6.png](/images/2-preparation/2.6-prepare-metric-data/2.6.6.png)

{{% notice note %}}
Ở 2 lệnh ở trên đều xuất hiện tham số **FCJ-Management-ASG** thì nó chính là tên của Auto Scaling Group mà chúng ta sẽ tạo về sau, nên về sau thì bạn cần sẽ phải tạo ASG với cùng tên như thế. Còn không thì bạn nên thay một cái tên khác từ bây giờ.
{{% /notice %}}

### Tải dữ liệu lên CloudWatch

Trong Amazon Linux 2023, và dùng đúng AMI thì AWS CLI đã được cài đặt sẵn ở bên trong, lúc này thì chúng ta chỉ cần lấy ra để cấu hình lại các crediential là được. Nên nhớ là bạn phải có một IAM User đủ quyền để tải dữ liệu lên CloudWatch hoặc ít nhất là đủ quyền để làm bài workshop này.

Vào trang IAM, vào thông tin IAM User và ấy Access Key Id và Serect Access Key, nếu chưa có thì tạo mới.

```bash
aws configure
```

Và tiến hành cấu hình

![2.6.7.png](/images/2-preparation/2.6-prepare-metric-data/2.6.7.png)

Sau đó là tải 2 file dữ liệu mà chúng ta đã chuẩn bị trước đó lên trên CloudWatch

```bash
aws cloudwatch put-metric-data --namespace 'FCJ Management Custom Metrics' --metric-data file://metric-cpu.json
```

```bash
aws cloudwatch put-metric-data --namespace 'FCJ Management Custom Metrics' --metric-data file://metric-instances.json
```

![2.6.8.png](/images/2-preparation/2.6-prepare-metric-data/2.6.8.png)

### Kiểm tra

Cuối cùng thì chúng ta sẽ vào trong CloudWatch để kiểm tra kết quả

- Tìm **CloudWatch**
- Click để vào trong CloudWatch Console

![2.6.9.png](/images/2-preparation/2.6-prepare-metric-data/2.6.9.png)

Trong giao diện Console của **CloudWatch**

- Chọn **All metrics**
- Chọn **FCJ Management Custom Metrics**

![2.6.10.png](/images/2-preparation/2.6-prepare-metric-data/2.6.10.png)

Chọn tiếp **AutoScalingGroupName**

![2.6.11.png](/images/2-preparation/2.6-prepare-metric-data/2.6.11.png)

Chọn tiếp 2 thông số như trên hình, chờ một khoảng thời gian để nhận được kết quả.

![2.6.12.png](/images/2-preparation/2.6-prepare-metric-data/2.6.12.png)

{{% notice note %}}
Chúng ta sẽ phải chờ khoảng **30 phút** hoặc hơn để cho CloudWatch xử lý xong. Thay vì chờ thì chúng ta nên làm tiếp các phần tiếp theo.
{{% /notice %}}
