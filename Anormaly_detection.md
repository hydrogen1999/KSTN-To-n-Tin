##  Mô hình động Markov cho đánh giá độ tin cậy hệ thống điện tử công suất

- DMM là một mô hình được phát triển dựa trên Mô hình Markov truyền thống. Vấn đề của mô hình Markov truyền thống là tỷ lệ lỗi xảy ra của hệ thống giá trị được xác định trước không đổi và không phụ thuộc vào điều kiện làm việc thực tế của hệ thống.
- Do ta có ma trận chuyển trạng thái nên độ tin cậy của hệ thống sẽ được tính dựa trên những giá trị cho trước, và tỷ lệ lỗi cố định sẽ không ảnh hưởng đến các giá trị độ tin cậy của hệ thống. Để có thêm giá trị đáng tin cậy cho độ tin cậy của hệ thống, tỷ lệ lỗi trong mỗi trạng thái của mô hình Markov phải phụ thuộc vào điều kiện làm việc của từng trạng thái.
- Độ tin cậy của hệ thống có thể được tính bằng cách lấy tích phân của hàm phân phối lỗi từ t đến vô cùng:
$$R=\int\limits_{t}^{\infty} R(t)dt$$
$$R(t)=e^{-\lambda t},$$ trong đó:
    - $\lambda$: tỉ lệ lỗi
    - $t$: thời gian hoạt động
- Để có tỷ lệ lỗi tùy thuộc vào điều kiện của mạch, $\lambda$ có thể xác định theo công thức:
$$\lambda=\lambda_b.\prod\limits_{i=1}^n \pi_i,$$ trong đó:
    - $\lambda_b$: là tỉ lệ lỗi cơ sở.
    - $\pi_i$: các yếu tố làm thay đổi tỉ lệ lỗi dựa trên các điều kiện thực tế của hệ thống:
        - $\pi_T$: yếu tố nhiệt độ
                $\pi_{T(\text{bán dẫn})}={T \over T_j}$, với $T_j=T_C+\theta_{jC}*P_{\text{hao tổn}}$
                $\pi_{T(\text{cuộn cảm})}={\text{trạng thái hiện tại}\over\text{đánh giá hiện tại}}$

-------------------------
## Phát hiện bất thường
- Ngày nay có nhiều kĩ thuật phát hiện bất thường trong dữ liệu theo thời gian. Mục đích chính của các kĩ thuật này là mô hình hóa hành vi xử lý để phát hiện sự phụ thuộc vào các điều kiện bên ngoài. 
- Có 2 loại phát hiện bất thường
    - Phát hiện bất thường tượng trưng
    - Phát hiện bất thường theo chuỗi thời gian đơn
#### Phát hiện bất thường với chuỗi thời gian đơn
- Vấn đề phát hiện bất thường trong một chuỗi thời gian đơn thường được dựa trên việc phát hiện thay đổi bất thường của các thuộc tính, tức là, xác định khi nào các tham số của một mô hình chuỗi thời gian thay đổi.
##### Phương pháp phát hiện bất thường
- Nhiều bài toán không thuộc dạng chuỗi thời gian có thể tuân theo các cách tiếp cận dựa trên khoảng cách Euclid, trong đó sự bất thường tương đối của một điểm dữ liệu được tính bằng khoảng cách đến các điểm dữ liệu khác.
- Trong khi đó phương pháp này không hữu hiệu với bài toán chuỗi thời gian, vì các biến số được gán stamp thời gian. Các bước thay thế:
    - Tính khoảng cách vuông góc giữa một data item và đoạn thẳng nối data item trước và sau của nó (trừ điểm đầu và điểm cuối).
    - Tính khoảng cách giữa một data point và đoạn đường nối hai data point gần nhất (phân đoạn dòng) (theo thời gian) của nó. Cho phép tính toán điểm bất thường cho cả điểm cuối cùng, mặc dù có yêu cầu ngoại suy thay vì nội suy trong một số trường hợp. Cho phép chuỗi thời gian có độ dốc khác nhau ở từng thời điểm.
    - Có thể sử dụng k> 2 điểm lân cận để xây dựng các phân đoạn dòng.
    - Khoảng cách của một điểm có thể được tính từ một đường cong được sử dụng để mô tả chuỗi thời gian, trong đó đường cong thu được bằng hồi quy hoặc spline.
#### Phát hiện bất thường đa chuỗi thời gian
- Khi hai chuỗi thời gian được biểu diễn thích hợp bởi mô hình tự hồi quy ARIMA$(p,d,q)$ và các tham số xác định chuỗi ($\varphi, \theta$) được ước tính bằng các dữ liệu của chuỗi thời gian, ta có thể định nghĩa một khái niệm về khoảng cách giữa hai chuỗi thời gian bởi sự khác biệt giữa các tham số xác định chuỗi ($\varphi, \theta$), chẳng hạn như khoảng cách Euclid giữa các vector ($\varphi, \theta$) của hai chuỗi thời gian. 
- Tuy nhiên, có một vài nhược điểm: số lượng tham số AR và MA phải bằng nhau, và ngoài ra, dù chỉ là một sự chênh lệch nhỏ trong các tham số p, d, q của hai mô hình ARIMA có thể dẫn đến chuỗi thời gian khác nhau đáng kể (sự phụ thuộc không liên tục vào dữ kiện đầu vào).
- Việc tính toán khoảng cách giữa một chuỗi thời gian đơn $X$ với đa chuỗi thời gian khác (giả sử trên cùng một tập dữ liệu D) là khá phức tạp. Trong trường hợp các vector tham số của tất các các chuỗi (cùng trên tập dữ liệu D) cơ bản là giống nhau và đều được mô hình bởi lớp ARIMA (tức là cùng các tham số p, d, q), khi đó thì giá trị trung bình của các vector ($\varphi, \theta$) của các chuỗi thời gian là đủ để ta có thể kết luận đặc điểm của tập các chuỗi thời gian này. Khi đó, ta có thể tính được khoảng cách giữa vector tham số của $X$ với trung bình vector tham số của các chuỗi thời gian (có cùng tập D) với độ chính xác cho phép.
- Trái lại, nếu có sự khác biệt đáng kể giữa các mô hình của chuỗi thời gian trong D, thì việc áp dụng cách trên là không hiệu quả. Để giải quyết vấn đề đó, tập dữ liệu gốc D sẽ được tính trung bình, đưa ra một chuỗi thời gian đại diện $X_D$ xuất phát từ mô hình ARIMA. Sau đó đem so sánh vector ($\varphi, \theta$) với vector của mô hình ARIMA$(p,d,q)$ của chuỗi $X$. Nếu khoảng cách thu được lớn, ta kết luận rằng $X$ là bất thường trên tập D (Quá trình này yêu cầu giá trị tham số $p,d,q$ thu được từ mô hình tự hồi quy ARIMA phải là tốt nhất).
- Tương tự, ta cũng có thể được sử dụng cách này để xác định sự bất thường trong cùng một chuỗi thời gian $X$ dao động theo thời gian từ $t_1$ đến $t_n$.