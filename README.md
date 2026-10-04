# proxy xoay dân cư: phân biệt gói theo IP và theo GB, cách đặt xoay mỗi request và mức giá thực tế của 9Proxy

Gõ cụm từ này vào Google thường xuất phát từ một trong hai tình huống: bạn cần một dãy IP dân cư đổi liên tục để chạy tool mà không bị chặn, hoặc bạn đã từng mua proxy và thấy tiền tiêu nhanh hơn dự tính. Cả hai đều dẫn về cùng một câu hỏi — xoay theo cách nào, và trả tiền theo đơn vị nào.

Phần khó chịu nhất của proxy xoay dân cư không nằm ở việc tìm nhà cung cấp. Nó nằm ở chỗ mỗi nơi định nghĩa chữ "xoay" một kiểu, còn mô hình tính tiền lại quyết định chính cái hành vi xoay đó. Mua gói tính theo IP rồi kỳ vọng IP tự đổi sau mỗi request là cách nhanh nhất để thấy tiền biến mất mà job vẫn fail. Mua gói tính theo GB cho một tác vụ cần giữ nguyên một IP suốt 20 phút cũng không sai, chỉ là bạn đang trả tiền cho thứ mình không dùng tới.

## Xoay dân cư khác gì proxy thường

Proxy dân cư là proxy đi qua IP do nhà cung cấp dịch vụ Internet cấp cho một thiết bị trong hộ gia đình. Về phía website đích, request trông giống như đến từ một người dùng bình thường ở một thành phố cụ thể, chứ không phải từ dải IP của datacenter — thứ bị đưa vào blacklist gần như ngay lập tức.

Chữ "xoay" thêm vào đó một tính chất nữa: IP thoát không cố định. Hệ thống lấy IP từ một pool lớn và đổi theo từng request, hoặc đổi sau một khoảng thời gian định sẵn. Mục đích rất thực dụng — không để một địa chỉ nào gánh đủ số request để bị rate limit.

Nhưng xoay không phải cây đũa thần. Nếu bạn đổi IP nhanh hơn mức một người thật có thể làm, chính tốc độ đó lại là dấu hiệu bất thường. Vài tài liệu kỹ thuật của các nhà cung cấp lớn chỉ ra rằng xoay dưới 1 giây mỗi IP dễ kích hoạt cơ chế phát hiện kiểu honeypot, còn để một IP sống quá 10 phút thì gần như mất hết lợi ích ẩn danh mà bạn đã trả tiền. Khoảng giữa hai con số đó là nơi mọi thứ hoạt động.

## Xoay mỗi request hay giữ phiên: chọn sai thì tốn tiền vô ích

Có hai chế độ, và hầu hết tool đều hỗ trợ cả hai:

- **Xoay (rotating)**: mỗi request hoặc mỗi kết nối dùng một IP mới. Hợp với thu thập dữ liệu khối lượng lớn, kiểm tra giá, kiểm tra quảng cáo, quét SERP.
- **Giữ phiên (sticky)**: giữ nguyên một IP trong khoảng thời gian bạn đặt. Bắt buộc phải dùng khi có đăng nhập, giỏ hàng, thanh toán nhiều bước — những luồng mà đổi IP giữa chừng sẽ làm rơi cookie và mất phiên.

Đây là chỗ nhiều người mua sai gói. Nếu công việc của bạn là nuôi tài khoản, mỗi profile cần một IP riêng và ổn định vài giờ, thì gói tính theo IP là lựa chọn hợp lý. Còn nếu bạn cào dữ liệu và mỗi request chỉ vài chục KB, gói tính theo GB thường rẻ hơn nhiều so với việc mua cả một IP chỉ để dùng vài lần.

👉 [Xem hai mô hình proxy dân cư của 9Proxy](https://bit.ly/9-Proxy)

## 9Proxy bán hai kiểu proxy dân cư, không phải một

9Proxy là nền tảng proxy dân cư toàn cầu, tự công bố pool hơn 20 triệu IP tại hơn 90 quốc gia. Điểm đáng chú ý là họ không gộp mọi thứ vào một bảng giá duy nhất mà tách thành hai sản phẩm riêng, được thiết kế cho hai kiểu workload khác nhau.

| Tiêu chí | Gói tính theo IP | Gói tính theo GB |
| --- | --- | --- |
| Cách tính tiền | Trả theo số lượng IP | Trả theo dung lượng |
| Băng thông | Không giới hạn trong thời gian IP hoạt động | Giới hạn theo GB đã mua |
| Thời lượng IP | Vài giờ đến khoảng 24 giờ, tùy IP | Xoay tự động theo request hoặc theo phiên |
| Tạo endpoint | Không giới hạn endpoint, chỉ trừ GB | Mỗi IP = 1 lượt dùng |
| Hết hạn | IP chưa dùng không mất | Hiệu lực 180 ngày, Enterprise không giới hạn |
| Cách xác thực | Cần app desktop (port forwarding nội bộ) | User/password hoặc whitelist IP |
| Cấu hình | Cần cài app | Làm trực tiếp trong Dashboard |

Sự khác biệt về cách xác thực là thứ ảnh hưởng tới vận hành nhiều hơn người ta tưởng. Gói theo IP cần app desktop chạy local để forward port, nên nếu bạn đẩy job lên VPS Linux không có giao diện, gói theo GB sẽ nhẹ đầu hơn hẳn: chỉ cần user/password hoặc whitelist IP là chạy được từ Dashboard.

Với gói theo GB, bạn có thể chọn mục tiêu theo quốc gia, tiểu bang, thành phố, mã ZIP hoặc cả ISP — ví dụ nhắm riêng một nhà mạng ở một thành phố cụ thể. Còn với gói theo IP vốn không tự xoay, 9Proxy cung cấp thêm tính năng Auto Rotation Proxy cho phép đổi IP theo khoảng thời gian tùy chỉnh trên những port đã chọn.

## Bảng giá đầy đủ của 9Proxy

9Proxy từng điều chỉnh giá lần đầu trong lịch sử hoạt động, áp dụng từ ngày 1 tháng 6 năm 2026 cho các gói tính theo IP và gói bundle. Các gói tính theo GB giữ nguyên mức giá. Số liệu dưới đây là mức công bố sau lần điều chỉnh đó — trước khi thanh toán, bạn nên đối chiếu lại với bảng giá hiển thị trong tài khoản vì nhà cung cấp có thể thay đổi tiếp.

### Gói tính theo IP (băng thông không giới hạn)

| Gói | Đơn giá/IP | Tổng | Mua |
| --- | --- | --- | --- |
| 100 IPs | $0,24 | $24 | [Chọn gói 100 IPs](https://bit.ly/9-Proxy) |
| 500 IPs | $0,144 | $72 | [Chọn gói 500 IPs](https://bit.ly/9-Proxy) |
| 1.000 IPs + 500 IPs tặng | $0,084 | $126 | [Chọn gói 1.500 IPs](https://bit.ly/9-Proxy) |
| 2.500 IPs | $0,084 | $210 | [Chọn gói 2.500 IPs](https://bit.ly/9-Proxy) |
| 5.000 IPs | $0,072 | $360 | [Chọn gói 5.000 IPs](https://bit.ly/9-Proxy) |
| 15.000 IPs | $0,048 | $720 | [Chọn gói 15.000 IPs](https://bit.ly/9-Proxy) |
| 25.000 IPs | $0,035 | $863 | [Chọn gói 25.000 IPs](https://bit.ly/9-Proxy) |
| 50.000 IPs | $0,029 | $1.438 | [Chọn gói 50.000 IPs](https://bit.ly/9-Proxy) |
| 100.000 IPs | $0,023 | $2.300 | [Chọn gói 100.000 IPs](https://bit.ly/9-Proxy) |
| 200.000 IPs | $0,021 | $4.140 | [Chọn gói 200.000 IPs](https://bit.ly/9-Proxy) |
| 500.000 IPs | $0,018 | $8.625 | [Chọn gói 500.000 IPs](https://bit.ly/9-Proxy) |

### Gói tính theo GB

| Gói | Đơn giá/GB | Tổng | Hiệu lực | Mua |
| --- | --- | --- | --- | --- |
| 5 GB | $3,00 | $15 | 180 ngày | [Mua gói 5 GB](https://bit.ly/9-Proxy) |
| 50 GB + 5 GB tặng | $2,10 | $105 | 180 ngày | [Mua gói 55 GB](https://bit.ly/9-Proxy) |
| 100 GB | $1,50 | $150 | 180 ngày | [Mua gói 100 GB](https://bit.ly/9-Proxy) |
| 200 GB | $1,00 | $200 | 180 ngày | [Mua gói 200 GB](https://bit.ly/9-Proxy) |
| 1.000 GB | $0,80 | $800 | 180 ngày | [Mua gói 1.000 GB](https://bit.ly/9-Proxy) |
| 2.000 GB | $0,75 | $1.500 | 180 ngày | [Mua gói 2.000 GB](https://bit.ly/9-Proxy) |
| 3.000 GB (Enterprise) | $0,72 | $2.160 | Không giới hạn | [Mua gói 3.000 GB](https://bit.ly/9-Proxy) |
| 6.000 GB (Enterprise) | $0,70 | $4.200 | Không giới hạn | [Mua gói 6.000 GB](https://bit.ly/9-Proxy) |
| 10.000 GB (Enterprise) | $0,68 | $6.800 | Không giới hạn | [Mua gói 10.000 GB](https://bit.ly/9-Proxy) |

Ba gói Enterprise không chỉ bỏ giới hạn 180 ngày. Theo mô tả của 9Proxy, nhóm này còn có chế độ team gồm 1 chủ tài khoản và tối đa 5 thành viên, chia sẻ dung lượng không hết hạn trong nội bộ, kiểm soát hạn mức theo từng thành viên, xem log hoạt động và tạo Share Code không giới hạn.

### Gói bundle (IP + GB)

| Gói | Cấu hình | Giá | Mua |
| --- | --- | --- | --- |
| Starter Bundle | 100 IPs + 5 GB | $30 | [Chọn gói Starter Bundle](https://bit.ly/9-Proxy) |
| Popular Bundle | 1.500 IPs + 50 GB | $180 | [Chọn gói Popular Bundle](https://bit.ly/9-Proxy) |
| Pro Bundle | 5.000 IPs + 500 GB | $720 | [Chọn gói Pro Bundle](https://bit.ly/9-Proxy) |

Bundle là lựa chọn cho những ai không muốn chia job thành hai nhóm rõ ràng. Ví dụ một agency vừa nuôi profile cho khách hàng vừa cào dữ liệu thị trường: nhóm việc thứ nhất cần IP ổn định, nhóm thứ hai chỉ cần băng thông.

## Nên chọn gói nào: vài tình huống cụ thể

Không có gói nào tốt nhất cho mọi người, nhưng có vài điểm gãy rõ ràng trong thực tế.

**Bạn chạy MMO, nuôi nhiều tài khoản trên AdsPower hoặc Dolphin Anty.** Mỗi profile cần một IP riêng và ổn định đủ lâu để thực hiện vài thao tác. Gói tính theo IP hợp hơn, vì băng thông không giới hạn nên bạn không phải đếm dung lượng khi trình duyệt tự tải ảnh và script. Gói 500 IPs ở mức $72 là điểm khởi đầu hợp lý cho cá nhân.

**Bạn cào dữ liệu, mỗi request vài chục KB.** Trả $24 cho 100 IP nhưng chỉ dùng mỗi IP vài lần là lãng phí. Gói 50 GB + 5 GB ở mức $105 cho phép lấy IP mới ở mọi request mà không bị tính thêm phí xoay.

**Bạn kiểm tra quảng cáo theo khu vực.** Cần nhắm tới thành phố, mã ZIP hoặc nhà mạng cụ thể. Gói theo GB xử lý được việc này ngay trong Dashboard, và nhờ gộp IP dân cư + dung lượng, bạn có thể đổi vị trí liên tục mà không lo hết IP.

**Bạn có ngân sách cố định và ghét mô hình subscription.** Cả hai mô hình của 9Proxy đều trả một lần, không phải thuê bao tháng. IP chưa dùng trong gói theo IP không hết hạn, còn dung lượng GB có hiệu lực 180 ngày. Với dự án làm theo đợt, đây là điểm cộng thật.

Một chi tiết tiết kiệm đáng để biết: 9Proxy có tính năng Today List cho phép dùng lại miễn phí bất kỳ proxy nào đã dùng trong 24 giờ trước. Với những job chạy lặp lại theo ngày, nhà cung cấp ước tính tính năng này tiết kiệm khoảng 20–30% — đây là con số do phía 9Proxy công bố, không phải kết quả đo độc lập.

## Cấu hình xoay IP: những thứ cần chuẩn bị trước khi trả tiền

Với gói theo GB, quy trình nằm gọn trong Dashboard:

1. Chọn phương thức xác thực — user/password hoặc whitelist IP.
2. Chọn vị trí đích theo quốc gia, tiểu bang, thành phố, mã ZIP hoặc ISP.
3. Chọn chế độ phiên: Rotating để đổi IP mỗi request, hoặc Sticky để giữ IP trong khoảng thời gian bạn đặt.
4. Xuất danh sách endpoint dưới dạng .txt hoặc .csv, kèm mẫu code sẵn cho một số ngôn ngữ.

Với gói theo IP, bạn cần cài app desktop để forward port, sau đó có thể bật Auto Rotation Proxy để đổi IP theo chu kỳ tùy chỉnh trên các port đã chọn. Nếu bạn muốn dùng proxy dân cư xoay cùng proxychains, script Python hoặc trình duyệt antidetect, cả hai mô hình đều hỗ trợ SOCKS5 và HTTP/HTTPS.

Một lưu ý về thời lượng phiên: nếu khoảng nghỉ giữa hai request vượt quá vài phút, phiên sticky có thể bị coi là hết hạn và request tiếp theo sẽ đi qua một IP khác. Với các luồng đăng nhập nhiều bước, hãy đặt thời gian nghỉ giữa các bước đủ ngắn, hoặc cấu hình session cố định để buộc hệ thống chỉ dùng một IP duy nhất.

👉 [Bắt đầu với 9Proxy và tạo proxy xoay dân cư đầu tiên](https://bit.ly/9-Proxy)

## Vài điểm cần chấp nhận trước khi mua

Không có nhà cung cấp nào phù hợp với tất cả mọi người, và 9Proxy cũng có những giới hạn nên biết trước:

- **Gói theo IP cần app desktop.** Nếu toàn bộ hạ tầng của bạn là VPS Linux không giao diện, gói theo IP sẽ vướng ở khâu cài đặt. Gói theo GB không có rào cản này.
- **Dung lượng GB có hạn 180 ngày.** Mua 1.000 GB rồi dùng dở dang thì phần còn lại sẽ hết hiệu lực nếu không nâng lên Enterprise. Đừng mua dung lượng lớn hơn tốc độ tiêu thụ thực tế của bạn.
- **Gói theo IP không tự xoay.** Cần bật Auto Rotation Proxy nếu muốn đổi IP theo chu kỳ.
- **Tỷ lệ thành công phụ thuộc mục tiêu.** Các bài đánh giá bên thứ ba đưa ra con số khác nhau — một số nêu khoảng 92–97%, con số khác lại ghi nhận gần 99,5% trên tập mục tiêu cụ thể. Chênh lệch này bình thường, vì site chống bot mạnh như sàn thương mại điện tử lớn sẽ khó hơn nhiều so với blog thông thường. Hãy test trên chính mục tiêu của bạn trong ngày đầu.
- **Chính sách bù cho IP lỗi.** Một số bài đánh giá nhắc đến việc 9Proxy cấp lại cho những IP không kết nối được trong 60 giây đầu. Nếu bạn gặp IP chết, cứ gửi ticket — nhưng đừng coi đây là lý do để bỏ qua bước kiểm tra ban đầu.

### Có bản dùng thử không?

9Proxy có chương trình dùng thử giới hạn cho người dùng mới, tùy theo tình trạng còn hàng tại thời điểm đăng ký. Đây là cách hợp lý để đo tỷ lệ thành công trên mục tiêu cụ thể của bạn trước khi nạp tiền.

### Có cần thanh toán theo tháng không?

Không. Cả hai mô hình đều là trả một lần. Bạn nạp số dư, mua gói, và dùng cho tới khi hết IP hoặc hết GB. Không có phí thuê bao định kỳ.

### Gói theo IP hay theo GB rẻ hơn?

Không có câu trả lời chung, vì đơn vị đo khác nhau. Nếu tác vụ của bạn tiêu tốn nhiều băng thông trên mỗi IP — duyệt web, tải ảnh, xem video — gói theo IP rẻ hơn nhiều vì băng thông không giới hạn. Nếu mỗi request chỉ vài chục KB nhưng cần đến hàng trăm nghìn IP khác nhau, gói theo GB sẽ tiết kiệm hơn. Cách nhanh nhất để quyết: ước lượng số request mỗi ngày, nhân với dung lượng trung bình mỗi request, rồi so với số IP bạn thực sự sẽ dùng hết.

### Có dùng được với trình duyệt antidetect không?

Có. 9Proxy hỗ trợ SOCKS5, nên cắm được vào AdsPower, Dolphin Anty, BitBrowser, Multilogin và bất kỳ tool nào nhận định dạng host:port:user:pass.

## Chốt lại

Với proxy xoay dân cư, thứ quyết định chi phí không phải giá mỗi GB hay mỗi IP, mà là việc bạn chọn đúng mô hình tính tiền cho đúng kiểu tác vụ. Xoay mỗi request cần trả theo dung lượng; giữ phiên dài cần trả theo số IP. Chọn ngược lại thì hoặc bị chặn, hoặc trả tiền cho phần mình không dùng.

9Proxy thuận lợi ở chỗ bán cả hai mô hình trên cùng một pool, nên bạn không phải đổi nhà cung cấp nếu cách làm thay đổi giữa đường. Mức giá khởi điểm $24 cho 100 IP và $15 cho 5 GB đủ thấp để thử nghiệm trước khi cam kết lớn hơn.

👉 [Xem toàn bộ gói proxy dân cư và chọn gói phù hợp với workload của bạn](https://bit.ly/9-Proxy)
