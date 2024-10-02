---
title: "Kiểm thử các giải pháp"
date: "`r Sys.Date()`"
weight: 7
chapter: false
pre: "<strong>7. </strong>"
---

### Các giải pháp / kỹ thuật scaling

Dịch vụ **Auto Scaling Group** cung cấp cho mình các giải pháp scaling khác nhau, tuỳ thuộc vào nhu cầu và mức độ sử dụng hệ thống của chúng ta. Vì thề mà chúng ta cần phải tính toán, ước lượng, quan sát và lập kế hoạch sử dụng cho từng loại hoặc là kết hợp các loại với nhau để tăng độ linh hoạt của hệ thống.

Trong phần này thì chúng ta sẽ đi thử từng giải pháp, nhưng trước khi đi vào từng giải pháp thì chúng ta hãy cũng tìm hiểu sơ về các giải pháp scaling này.

#### Manual scaling

Chúng ta thực hiện mở rộng hay thu hẹp các target trong một Target Group bằng cách là điều chỉnh thông số Desired capacity trong **Auto Scaling Group**, thì hành động này được gọi là Manual Scaling. Trong một số tình huống đơn lẻ, nhanh, thì chúng ta cần sẽ phải thực hiện việc thêm và bớt các targets thủ công.

#### Scheduled scaling

Khi mà chúng ta nắm rõ được lưu lượng mạng vào và ra của hệ thống hoặc là thời điểm mà các target hoạt động ở công suất gần như là cao nhất, và hoạt động này diễn ra liên tục và mang tính dài hạng (có thể là hàng năm) thì mình có thể đặt lịch (và cả hẹn giờ) để cho **Auto Scaling Group** thực hiện việc mở rộng và thu gọn các targets.

#### Dynamic scaling

Ngoài ra nếu như lưu lượng mạng đi vào hệ thống không diễn ra theo một trật tự nào và khó đoán thì chúng ta có thể dùng giải pháp tự động scaling của ASG. Khi đó thì ASG sẽ dựa vào cấu hình Dynamic scalang policy để triển khai việc mở rộng và thu gọn các targets cho phù hợp hơn với hệ thống.

#### Predictive scaling

Còn một kỹ thuật khác nữa là ASG sẽ dự đoán các lưu lượng mạng trong vòng 3 hoặc nhiều ngày tới. Với những hệ thống khó đoán, thì chúng ta có thể dựa vào giải pháp này và Dynamic scaling để tăng tính linh hoạt cho hệ thống. Giải pháp này sẽ biểu diễn các thông số tuỳ vào việc mà mình cấu hình, nhưng ý tưởng chung vẫn là dữ đoán trước các lưu lượng, mức sử dụng trong hệ thống.

{{% notice note %}}
Vì khi thực hiện phần này thì chúng ta không có dữ liệu ở phần trước, nên đó là lý do mà chúng ta cần phải chuẩn bị và chạy dữ liệu mẫu ở phần **2.6 - Prepare metrics for predictive scaling** trước đó.
{{% /notice %}}

### Cài đặt chương trình kiểm thử

Trước khi đi vào phần này, thì chúng ta cần phải tải một chương trình kiểm thử để có thể giải lập được hệ thống đang chịu tải ở lưu lượng cao. Đầu tiên, vào đường dẫn này để tải chương trình kiểm thử về: [https://www.paessler.com/tools/webstress](https://www.paessler.com/tools/webstress)

![7.1](/images/7-test-solution/7.1.png)

Chúng ta sẽ tải về file Rar, vào trong file Rar đó trích xuất file cài đặt ở bên trong và cài đặt chương trình. Sau khi cài đặt xong thì chúng ta vào trong chương trình và thấy được giao diện như sau

![7.2](/images/7-test-solution/7.2.png)

### Nội dung

1. [Kiểm thử giải pháp manual scaling](/7-test-solutions/7.1-test-manual-scaling-solution)
2. [Kiểm thử giải pháp scheduled scaling](/7-test-solutions/7.2-test-scheduled-scaling-solution)
3. [Kiểm thử giải pháp dynamic scaling](/7-test-solutions/7.3-test-dynamic-scaling-solution)
4. [Kiểm thử giải pháp predictive scaling](/7-test-solutions/7.4-test-predictive-scaling-solution)

{{% notice ìn %}}
Thời gian để làm phần này là rất lâu, và cần phải quan sát kỹ lưỡng (bạn có thể test trong quá trình chạy kiểm thử), nên bạn phải kiên nhẫn và kĩ lường để quan sát kết quả.
{{% /notice %}}
