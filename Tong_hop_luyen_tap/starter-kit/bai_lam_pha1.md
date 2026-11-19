    ## 4.1. Bảo vệ dữ liệu và chống ảo giác

    ### a) Ghi chú đã ẩn danh hoá

    **GHI CHU DA AN DANH**

    ```text
    Khán giả [tên_khách_hàng], [số_điện_thoại], [số_CCCD], [email], đặt 3 vé gói SVT trận bán kết Cúp Sao Vàng [ngày] cho 2 người lớn và 1 trẻ em 9 tuổi. Khán giả đã [thông_tin_chuyển_khoản]. Khán giả yêu cầu 3 ghế ngồi cạnh nhau gần lối đi.

    ```

    ### b) Hai câu lệnh chống ảo giác

    **CAU LENH**

    ```text
    Câu 1: dựa trên file chính sách hoàn/hủy mà tôi hãy trả lời câu hỏi của tôi. Nếu trong chính sách không có thông tin thì không bịa ra thông tin mà phải trả lời là [không có]
    Câu 2: khi bạn trả lời cho tôi hãy nêu ra lấy từ mục nào trong file hoàn hủy.
    ```

    ## 4.2. Trích xuất tin nhắn đặt vé ra JSON

    **PROMPT**

    ```text
    [context] bạn là một chuyên gia phân tích nhu cầu khách hàng
    [repuest] bạn hãy chuyển dữ liệu TN1, TN2, TN3 trong thể <tin_nhan> thành một mảng JSON 3 đối tượng, đúng thứ tự, đúng 6 trường như tin nhắn mẫu
    [explanation] khi chuyển về định dạng json phải tuân thủ theo <quy_chuan> bạn có thể tham khảo theo một số <vi_du> mà tôi đã làm sẵn
    1. ma_goi lấy theo bảng mã gói.
    2. ngay_su_kien dạng YYYY-MM-DD; tin nhắn không ghi năm thì lấy năm 2026; không có ngày cụ thể thì null.
    3. Khách không nhắc trẻ em thì tre_em là 0 và mọi khách là người lớn.
    4. loai_ve chỉ nhận "thuong", "vip" hoặc null.
    5. ghi_chu chỉ ghi yêu cầu đặc biệt về chỗ ngồi, hỗ trợ di chuyển hoặc ăn uống; không có thì null.
    [action] đọn dữ liệu mà tôi gửi trước khi chuyển về json=> chuẩn hóa dữ liệu => trả đúng về định dạng json
    [tone] chuyên nghiệp, ngắn gọn
    [extras]chỉ trả về JSON, không chào hỏi, không giải thích.


    <quy_chuẩn>


    1. ma_goi lấy theo bảng mã gói.
    2. ngay_su_kien dạng YYYY-MM-DD; tin nhắn không ghi năm thì lấy năm 2026; không có ngày cụ thể thì null.
    3. Khách không nhắc trẻ em thì tre_em là 0 và mọi khách là người lớn.
    4. loai_ve chỉ nhận "thuong", "vip" hoặc null.
    5. ghi_chu chỉ ghi yêu cầu đặc biệt về chỗ ngồi, hỗ trợ di chuyển hoặc ăn uống; không có thì null.



    </quy_chuẩn>

    <vi_du>
    
    
    Tin nhắn mẫu 1:
Đặt giúp mình 2 vé VIP trận chung kết ngày 15/11/2026, 2 người lớn và 1 bé. Cần chỗ ngồi cạnh lối đi.
Kết quả đúng:
{"ma_goi": "VIP", "ngay_su_kien": "2026-11-15", "nguoi_lon": 2, "tre_em": 1, "loai_ve": "vip", "ghi_chu": "chỗ ngồi cạnh lối đi"}

Tin nhắn mẫu 2:
Cho mình một vé Fan Zone, ngày nào cũng được, mình đi một mình.
Kết quả đúng:
{"ma_goi": "FZ", "ngay_su_kien": null, "nguoi_lon": 1, "tre_em": 0, "loai_ve": "thuong", "ghi_chu": null}
    
    
    
    </vi_du>


    <tin_nhan>
    
    
    TN1: Mình muốn đặt gói Sân Vận Động trận tứ kết ngày 20/12 nha, 2 người lớn với 1 bé 8 tuổi, vé thường.

TN2: Cho 3 người đi Fan Zone trận ngày 05/01/2027 ạ. Một người cần hỗ trợ xe lăn.

TN3: Trận chung kết Cúp Sao Vàng tháng 12 còn vé không ạ? Nhà em 4 người lớn, có một người khiếm thị cần hỗ trợ tìm chỗ, lấy vé VIP.

    
    
    
    </tin_nhan>
    ```

    ## 4.3. Báo giá vé bằng Chain-of-Thought

    ### a) Prompt

    **PROMPT**

    ```text
   [context] Bạn là một chuyên gia soát vé . 
   [request] hãy tính tổng tiền vé 
   hãy đọc thẻ <bang_gia_ve>, <quy_tac_tinh_gia> và <yeu_cau_bao_gia> để cho ra kết quả và suy luận từng bước theo thứ tự tiền người lớn → tiền trẻ em → tiền vé → giảm giá nhóm → phụ thu → tổng tiền, mỗi bước ghi phép tính; dòng cuối có dạng [RESULT: <tổng tiền> đồng].
<bang_gia_ve>


BẢNG GIÁ VÉ (đồng/người lớn)
SVT – Sân Vận Động: 1.200.000
FZ – Fan Zone: 800.000
VIP – Khán đài VIP: 2.500.000




</bang_gia_ve>


<quy_tac_tinh_gia>


1. Trẻ em từ 5 đến 11 tuổi tính 70% giá người lớn. Trẻ dưới 5 tuổi miễn phí.
2. Nhóm từ 5 người lớn trở lên được giảm 5% trên tiền vé (tiền người lớn + tiền trẻ em).
3. Phụ thu khu ghế ưu tiên: 300.000 đồng/người. Phụ thu không được giảm giá.
4. Tổng tiền = tiền vé sau giảm + phụ thu.



</quy_tac_tinh_gia>


<yeu_cau_bao_gia>

Nhóm cổ động viên đi xem trận bán kết, mua gói SVT, gồm 5 người lớn, 2 trẻ em (8 tuổi và 10 tuổi) và 1 bé 3 tuổi. Có 1 người lớn chọn khu ghế ưu tiên.


</yeu_cau_bao_gia>
    ```

    ## 4.4. Dây chuyền xử lý khiếu nại (Prompt Chaining)

    ### a) Prompt Trạm 1

    **PROMPT**

    ```text
    [context] bạn là một chuyên gia chăm sóc khách hàng
    [repuest] bạn hãy phân tích và chuyển dữ liệu từ <email> và <chinh_sach_den_bu> theo định dạng json gồm đúng 4 trường theo <vi_du>
    
    
    <email>
    
    Tôi là khán giả mua vé gói SVT trận Cúp Sao Vàng ngày 02/11/2026, đi 2 người lớn. Ban tổ chức cam kết khu khán đài có mái che nhưng trong 2 hiệp đầu chúng tôi bị xếp sang khu không mái, trời mưa và ghế ướt. Nhân viên soát vé rất nhiệt tình, tôi không có gì phàn nàn về nhân viên. Tôi đề nghị ban tổ chức giải quyết thỏa đáng.


    
    
    </email>


    <chinh_sach_den_bu>


- tran_gio: trận đấu bắt đầu trễ trên 2 giờ do ban tổ chức: tặng voucher 200.000 đồng/khách.
- sai_khu_vuc: khán giả bị xếp sang khu vực thấp hơn quyền lợi đã cam kết: hoàn 500.000 đồng/khách cho mỗi hiệp bị ảnh hưởng.
- nhan_vien: khiếu nại về thái độ nhân viên: tặng voucher 300.000 đồng/khách.
- khac: chuyển bộ phận Chăm sóc khán giả xem xét, chưa đề xuất mức đền bù.
- Tổng mức đền bù trên 1.500.000 đồng phải được Trưởng ban Chăm sóc khán giả duyệt trước khi gửi khách.



    </chinh_sach_den_bu>


    <vi_du>
    "loai_su_co", "tran_gio" ,"sai_khu_vuc","nhan_vien" "khac", "so_khach" , "so_hiep_bi_anh_huong","tom_tat"


    
    
    </vi_du>
    không giải thích gì thêm
    ```

    ### b) Hai điều cần kiểm tra ở JSON đầu ra của Trạm 1

    1. đúng định dạng json

    2.các thông tin đền bù không được ngoài chính sách

    ### c) Câu lệnh viết tiếp

    **CAU LENH**

    ```text
    bạn đang bị ngắt giữa chừng ở đoạn "…Ban tổ chức Cúp Sao Vàng xin hoàn lại Quý khán giả khoản" hãy viết tiếp
    ```
