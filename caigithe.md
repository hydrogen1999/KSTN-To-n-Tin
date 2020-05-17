
# ***Hệ thống và mạng máy tính***
### Mục lục
1. [Chương 1:Phân loại mạng và phương thức truyền tin](#C1)
2. [Chương 2:Phân lớp và bộ giao thức](#C2)
3. [Third Example](#third-example)
--------------------------------
## <a id= "C1">Chương 1: Phân loại mạng và phương thức truyền tin</a>

### 1. Mạng truyền thông

Communication Networks
- Switched networks
    + [Circuit switching (Chuyển mạch kín)](#Chuyenmachkin)
    + [Packet switching (Chuyển mạch gói)](#Chuyenmachgoi)
        > [Datagram networks](#DatagramNetworks)
        > [Virtual circcuit networks](#VirtualCircuitNetworks)
- Broadcast networks

#### 1.1. <a id="Chuyenmachkin">Circuit Switching (Chuyển mạch kín) </a>
###### a) Đặc điểm
- **Đường truyền riêng** được thiết lập giữa hai nút đầu cuối thông qua các nút mạng
    > *<p style="font-size: 14px">Nghĩa là:  hai trạm muốn trao đổi thông tin với nhau thì giữa chúng sẽ được thiết lập một “kênh” (circuit) cố định, kênh kết nối này được duy trì và dành riêng cho hai trạm cho tới khi cuộc truyền tin kết thúc.<p>*
- **Khả năng/tốc độ cố định** trong suốt quá trình kết nối. Phần năng lực không được khai thác cũng không thể sử dụng cho mạch khác.
- **Dữ liệu không bị trễ tại bộ chuyển mạch**
- **Dữ liệu truyền liên tục (từng bit)**. Gặp sự cố $\implies$ Lại từ đầu

###### b) Quá trình thiết lập gồm: 3 giai đoạn
- Giai đoạn 1 (***Thiết lập kết nối***): liên kết các tuyến giữa các trạm trên mạng thành một tuyến (kênh) duy nhất dành riêng cho cuộc gọi. Nếu mạch không được thiết thập 
$\implies$Báo lỗi
- Giai đoạn 2 (***Truyền dữ liệu***): thông tin được trao đổi là trong suốt.
    > *<p style="font-size: 14px">Trong suốt theo hai yếu tố: <b>Dữ liệu không bị thay đổi</b> và <b>Độ trễ nhỏ</b><p>*
- Giai đoạn 3 (***Ngắt mạch***): Hủy đường truyền.

###### c) Tính toán độ trễ

$$Tổng=\underbrace{d_{proc}}_{Trễ xử lí} + \underbrace{d_{prop}}_{Trễ lan truyền}+ \underbrace{d_{trans}}_{Trễ truyền}$$
 > *<p style="font-size: 14px"> ***Trễ lan truyền***: thời gian truyền <span style="color:red">bit đầu tiên</span> của gói tin từ nguồn tới đích.<p>*$$d_{prop}={Độ dài đường truyền \over Tốc độ lan truyền}$$

 > *<p style="font-size: 14px"> ***Trễ truyền***: thời gian truyền <span style="color:red">một gói tin</span> qua mạng.<p>*$$d_{trans}={Kích thước gói [bits] \over Tốc độ truyền[bps]}$$

 ###### d) Ưu - nhược điểm
 
- Ưu điểm:
    - Chất lượng đường truyền tốt, ổn định, độ trễ nhỏ
    - Các thiết bị mạng đơn giản, có tính ổn định cao, chống nhiễu tốt.
- Nhược điểm:
    - Tốn thời gian để thiết lập kênh truyền
    - Sử dụng băng thông không hiệu quả:
        - Độ rộng băng thông cố định
        - Không thể chia sẻ đường truyền cho kết nối khác
    - Không an toàn: do toàn bộ gói tin được gửi nguyên bản nên rất dễ bị đánh cắp dữ liệu.
    - Khả năng mở rộng của kênh mạng kém: khó nâng cấp.

#### 1.2. <a id="Chuyenmachgoi">Packet switching (Chuyển mạch gói)</a>
##### 1.2.1. Khái quát về chuyển mạch gói
###### a) Quá trình chuyển mạch gói
- Dữ liệu được chia thành các gói (packet) nhỏ.
- Các gói xếp hàng để được xử lý và truyền độc lập.
- Sau khi nhận được đủ các gói thì ghép lại thành gói ban đầu.

###### b) Đặc điểm
- Dữ liệu chia thành các gói.
- Cấu trúc một gói:

    |Header (A)|Payload (P) |Trailer (T)|
    |-|-|-|
    > **Header**: Địa chỉ nguồn, địa chỉ đích, số thứ tự của gói tin,...
    **Payload**: chứa nội dung gói tin
    **Trailer**: Xác định và xử lí lỗi
- Tại mỗi nút, gói tin được nhận, nhớ và chuyển tiếp đến trạm đích.
- Trong quá trình truyền tin có thể định tuyến động
    >**Định tuyến cho gói tin**: là nút trong mạng chuyển mạch gói nhằm xác định đường truyền cho gói tin từ trạm đầu $\rightarrow$ trạm cuối
- Tài nguyên trong chuyển mạch gói: 
    1. Mỗi gói chờ đến lượt tại hàng đợi ra $\rightarrow$ Có thể sinh ra tắc nghẽn do nhiều gói xếp hàng chờ kênh truyền
    2. Khi đến lượt, nó sử dụng toàn bộ giải thông. Sử dụng theo nhu cầu (có thể lớn).

###### c) Chuyển mạch gói tin >< Chuyển mạch thông điệp
- ***Chuyển mạch thông điệp :***
    - Trạm đầu và cuối bằng việc gửi và nhận cả thông điệp, thông qua các nút trung gian.
    - Cơ chế ***Store and forward***: các nút trung gian có nhiệm vụ chuyển toàn bộ thông điệp sang nút kế tiếp. Do đó, mỗi nút phải có dung lượng lưu trữ. Message chỉ được truyền sang nút kế tiếp nếu có đủ tài nguyên và kết nối còn khả dụng, nếu không, message sẽ được lưu trữ vô thời hạn.
    - Tính toán độ trễ:
        - Kích thước message: M
        - Địa chỉ (thời gian xử lý):A
        - Độ trễ thiết lập truyền thông: s
        - Số lượng trạm: n
        - Băng thông truyền: R
            - Thời gian truyền ($d_{trans}$):$$n\left(s+{M+A \over R}\right)$$
            - Độ trễ: $$(n-1)\left(s+{M+A \over R}\right)$$
    - Ưu/Nhược điểm:
        > **Ưu điểm**: 
        -Truyền thông điệp có thể lưu trữ (store) khi kênh không khả dụng $\rightarrow$ Giảm tắc nghẽn.
        -Có thể chia sẻ kênh truyền.
        -Quản lý lưu lượng hiệu quả nhờ việc gán mức độ ưu tiên cho thông điệp
        
        >**Nhược điểm**:
        -Tại mỗi bước đều phải đợi cho đến khi nhận được toàn bộ thông điệp, lưu trữ và truyền đi sau khi xử lý nút tiếp theo $\rightarrow$ Độ trễ rất lớn
        -Yêu cầu các trạm trung gian phải có dung lượng lưu trữ lớn để chứa toàn bộ thông điệp $\rightarrow$ Tốn kém
- ***Chuyển mạch gói:***
    - Đặc điểm (bên trên)
    - Tính toán độ trễ:
        - Thời gian truyền: $$(n-1)\left(s+{A+P \over R} \right)+ \frac M P \left(s+{A+P \over R}\right)$$
        - Độ trễ: $$(n-1)\left({A+P \over R}\right)$$
    - Ưu/Nhược điểm:
        > **Ưu điểm**:
        -Mềm dẻo, hiệu suất truyền tin cao: Cho phép chia sẻ chung đường truyền $\rightarrow$ Tối đa hiệu quả đường truyền.
        -Khả năng truyền ưu tiên: sắp xếp thứ tự các gói theo mức độ ưu tiên
        -Khả năng sống sót cao: Khi một đường truyền bị hỏng thì các gói tin đi theo đường khác.

        >**Nhược điểm**:
        -Qua mỗi trạm trung gian, các gói được lưu trữ, xử lí rồi mới tiếp tục truyền đi $\rightarrow$Độ trễ khá lớn.
        -Độ tin cậy/bảo mật không cao, dễ mất gói, tắc nghẽn,...do dùng chung đường truyền.
        -Thứ tự truyền các gói đến điểm nhận phụ thuộc tốc độ từng đường truyền $\rightarrow$ Xử lí ghép thành dữ liệu ban đầu phức tạp hơn.

##### 1.2.2. Kỹ thuật chuyển mạch gói Datagram và Virtual Circuit Networks
###### a) <a id="DatagramNetworks">Datagram Networks (Chuyển mạch gói Datagram)</a>
- Mỗi gói (datagram) được chuyển mạch độc lập với nhau.
- Đây là dịch vụ không kết nối (Connectiveless service) nên không có kênh riêng cho kết nối. Thường sử dụng cho mạng IP và các kết nối Internet.
- Tất cả các gói có thể đi theo các con đường khác nhau bằng cách thay đổi động bảng định tuyến trên bộ định tuyến. Dựa vào địa chỉ đích mà bộ định tuyến chọn đường (có thể thay đổi trong 1 session).
    > Hệ quả:
    -Thứ tự các gói nhận được ở địa chỉ đích có thể khác với thứ tự truyền.
    -Header mỗi gói chứa thông tin về địa chỉ đích
- Độ trễ trong mạng chuyển mạch gói:
    - Gói tin trễ qua từng nút (hop).
    - Có 4 kiểu trễ:
        - **Trễ do xử lý**: kiểm tra lỗi và định tuyến.
        - **Trễ hàng đợi**: chờ đến lượt truyền
            - Phụ thuộc vào số lượng gói tin trong hàng đợi.
            - Phụ thuộc kích thước hàng đợi: kích thước lớn $\rightarrow$ chứa được nhiều gói. Nếu đầy thì drop (từ chối) gói tin.
        - **Truyền**: Thời gian gửi gói tin đến đường truyền (phụ thuộc tốc độ đường truyền)
        - **Trễ lan truyền**: thời gian truyền từ router này sang router khác.
    - Tính toán:
        + R: băng thông [bps]
        + L: chiều dài gói tin [bits]
        + $\lambda$: tốc độ truyền bits trung bình [bit/s]
        + L$\lambda$: tốc độ truyền gói tin trung bình [pkt/s]
###### b) <a id="VirtualCircuitNetworks">Virtual circuit Networks (Mạng mạch vòng ảo) </a>
- Là sự kết hợp của Circuit Switching và Packet Switching.
- Dữ liệu chia thành các gói, đi theo 1 đường định trước $\rightarrow$ chỉ cần Header chung nằm ở gói đầu tiên, các gói sau chỉ cần lưu ID đường truyền.
- Đảm bảo thứ tự các gói tin.
- Tuy nhiên, các gói tin của mạch khác có thể bị lẫn vào.
- Được sử dụng cho mạng ATM (Chế độ truyền không đồng bộ).

<p style="color: red">So sánh Mạng mạch vòng ảo và Chuyển mạch gói<P>

||Mạng mạch vòng ảo|Chuyển mạch gói|
|-|-|-|
|Ưu điểm| Độ tin cậy cao. Trong quá trình truyền vẫn giữ nguyên thứ tự gói. Không cần phải định tuyến và viết header cho tất cả các gói tin|Sử dụng đường truyền hiệu quả do sự dồn kênh phân thời gian. Cài đặt khá đơn giản. Chi phí truyền tin không cao.|
|Nhược điểm|Mỗi lần kết nối phải thiết lập kênh truyền $\rightarrow$ tốn kém.Không tối ưu được hiệu quả đường truyền|Dễ tắc nghẽn dẫn đến trễ, mất gói tin $\rightarrow$ cần xây dựng giao thức đảm bảo quá trình truyền ổn định. Phải viết header và định tuyến cho từng gói tin.


------------------------------------------------------
## <a id= "C2">Chương 2: Phân lớp và bộ giao thức</a>
### 1. Phân lớp
#### 1.1. Hệ truyền thông phân lớp - Kiến trúc mạng phân lớp.

![Protocol](C:/Users/nguye/OneDrive/Desktop/abc.png)
- Tầng N chỉ giao tiếp với tầng N+1 và N-1.
- Giữa hai tầng cùng mức thì sử dụng cùng 1 giao thức (Protocol) (Không giao tiếp trực tiếp).
- Tầng N cung cấp dịch vụ cho tầng N+1 và sử dụng dịch vụ của tầng N-1.
#### 1.2. Tại sao phải phân lớp?
- **Ưu điểm:**
    - Mỗi lớp chỉ có một số nhiệm vụ, chức năng chuyên biệt $\rightarrow$ Giảm sự phức tạp.
    - Mỗi lớp có một bộ giao thức riêng.
    - Có thể sửa đổi bên trong một phân lớp mà không làm hệ thống bị phá vỡ (miễn là vẫn cung cấp 1 dịch vụ) $\rightarrow$ Dễ bảo trì, nâng cấp.
- **Nhược điểm:**
    - Tốn chi phí tiền xử lí giữa các tầng.
    - Nếu tổ chức phân chia các tầng không tốt (nhiều hoặc ít) $\rightarrow$ Hiệu quả không cao.
    - Trong nhiều trường hợp, phần mềm không tối ưu.
### 2. Giao thức
- Là thỏa thuận giữa hai bên về cách thức xử lí truyền thông.
- Giao thức là:
    - Định dạng thông điệp trao đổi.
    - Tập hợp các trạng thái và các thông điệp được phép gửi tại mỗi trạng thái.
    - Các trạng thái này xác định thứ tự của thông điệp, ràng buộc về thời gian và các tính chất khác.
- VD: FTP, TCP, HTTP,...
### 3. Dịch vụ
- Dịch vụ: là tính năng của đối tượng.
- Chất lượng dịch vụ: là các đặc tính phi chức năng của dịch vụ (tốc độ, độ ổn định).
    - Nhiều dịch vụ cần đảm bảo các thông số vận hành sau:
        - Độ trễ 2 điểm đầu-cuối, dao động độ trễ
        - Thông lượng
        - Tỷ suất lỗi
    - Cài đặt dịch vụ để: kiểm soát tài nguyên, băng thông, packet scheduling.
- Các dịch vụ được cung cấp bởi các tầng khác nhau.
- 2 kiểu dịch vụ là: ***báo nhận*** và ***không báo nhận***.
    > ***Báo nhận***: Có phản hồi về kết quả giữa trạm đầu - cuối.
    ***Không báo nhận***: Không có phản hồi về kết quả gửi.
#### 3.1. Dịch vụ tin cậy và Dịch vụ không tin cậy
- Dịch vụ tin cậy:
    - Đảm bảo dữ liệu tới được đích
    - Các cơ chế:
        - Ack (báo nhận)
        - Retransmission (Gửi lại)
        - Timer: bộ đếm thời gian, nếu sau một khoảng thời gian mà không có phản hồi thì gửi lại.
- Dịch vụ không tin cậy: 
    - Không đảm bảo dữ liệu tới được đích.
        VD: dịch vụ cơ sở trong Datagram Networks.
> Tại sao vẫn có dịch vụ không tin cậy?
$\implies$ Trong nhiều trường hợp thì không cần thiết phải đảm bảo dữ liệu tới đích (Vd: quảng cáo hàng loạt,...); để giảm chi phí hoặc do bên cung cấp có hệ thống xử lí lỗi riêng,...
#### 3.2. Dịch vụ hướng kết nối và Dịch vụ phi kết nối.
- ***Dịch vụ hướng kết nối:*** 
    - VD: TCP, ...
    - Ưu điểm:
        - Chủ yếu là dịch vụ tin cậy
        - Ít xảy ra tắc nghẽn hơn
        - Thứ tự các gói được đảm bảo nên không bị trùng lặp
        - Thích hợp cho các kết nối lâu dài
    - Nhược điểm:
        - Phân bổ tài nguyên trước khi kết nối khiến tài nguyên mạng không được tận dụng.
        - Tốc độ kết nối thấp.
        - Trong trường hợp lỗi bộ định tuyến hoặc tắc nghẽn mạng, không có cách nào khác để tiếp tục kết nối.
    - Các bước kết nối:
        1. Thiết lập kết nối
        2. Khai thác
        3. Hủy kết nối
    - Cài đặt:
        - Mặc định trong Virtual Circuit Networks
        - Trong Datagram Networks, cài đặt thông qua các cơ chế: số thứ tự, truyền lại,...
- ***Dịch vụ phi kết nối:***
    - Không đảm bảo chuyển phát đến nơi, có thể thất lạc.
    - Cài đặt:
        - Mặc định trong Datagram Networks
        - Không nên cài đặt trong Circuit-Switching và Virtual Circuit Networks.
    - Ưu điểm:
        - Đơn giản, chi phí thấp.
        - Tốc độ kết nối khá cao.
        - Truyền- phát đa tin nhắn (1 người gửi, nhiều người nhận).
        - Trong trường hợp bộ định tuyến bị lỗi hoặc tắc nghẽn mạng, các gói dữ liệu được định tuyến thông qua các đường dẫn thay thế $\rightarrow$ không bị gián đoạn.
    - Nhược điểm:
        - Là dịch vụ không tin cậy
        - Gói tin phải chứa địa chỉ đích và thông tin định tuyến.
        - Dễ xảy ra tắc nghẽn mạng.
#### 3.3. Đồng bộ
- Dịch vụ với độ trễ cố định, tỷ lệ lỗi biết trước.
- Cài đặt:
    - Mặc định trong Circuit Switching Networks
    - Khó thực hiện trong Packet Switching Networks
#### 3.4. Dịch vụ cơ bản
##### 3.4.1. Hàm nguyên thủy của dịch vụ
- Dịch vụ của tầng là tập hợp các hàm (tác vụ) nguyên thủy/cơ sở mà một tầng cung cấp cho tầng phía trên. Nó định nghĩa các hàm có thể thực hiện (tương tự như 1 interface).
- Các hàm:
    - LISTEN: Chờ đợi kết nối
    - CONNECT: thiết lập kết nối
    - RECEIVE: nhận thông điệp
    - SEND: báo nhận
    - DISCONNECT: hủy kết nối
##### 3.4.2 Điểm truy cập dịch vụ
- VD: trong TCP/IP là Port,...
- Điểm mà tại đó dịch vụ được cung cấp cho User.
- Là thành phần của địa chỉ mạng, định danh tiến trình, thực thể truyền tin
- Các điểm truy cập dịch vụ khác nhau phân biệt các dịch vụ, ứng dụng khác nhau trên cùng một máy.

>    Chú ý: ***Protocol Data Unit***: đơn vị dữ liệu giao thức, mỗi tầng trong mô hình sử dụng các PDU để giao tiếp và trao đổi thông tin mà chỉ có thể được đọc bởi các lớp nằm ngang bên thiết bị nhận và sẽ được chuyển lên cho các lớp bên trên sau khi bóc tách thông tin.
Tầng 1 – Tầng Physical : Nó là Bits
Tầng 2 – Tầng Data Link: Nó là Frame
Tầng 3 – Tầng Network: Nó là Packet
Tầng 4 – Tầng Transport: Nó là Segment

<h4><p style = "color: red">So sánh Dịch vụ và Giao thức<p></h4>

|Giao thức|Dịch vụ|
|-|-|
|Giao thức là một tập các luật mô tả khuôn dạng dữ liệu, ý nghĩa của các gói tin và thứ tự các gói tin được sử dụng trong quá trình giao tiếp.|Là một tập các hàm mà một tầng cung cấp cho tầng phía trên của nó gọi sử dụng.|

> Chú ý: Cùng một service có thể được thực hiện bởi các protocol khác nhau, mỗi protocol có thể được cài đặt theo một cách thức khác nhau (sử dụng cấu trúc dữ liệu khác nhau, ngôn ngữ lập trình là khác nhau, vv...).

##### 3.4.3. Cấu trúc phân tầng
- Có 2 quá trình:
    - Đóng gói (quan trọng nhất).
    - Hợp nhất
- Các tầng xử lý độc lập

### 4. Mô hình OSI (Open System Interconnect)

