## 4.2. Trích xuất tin nhắn đặt vé ra JSON

**KET QUA AI**

```text
[
  {
    "ma_goi": "SVD",
    "ngay_su_kien": "2026-12-20",
    "nguoi_lon": 2,
    "tre_em": 1,
    "loai_ve": "thuong",
    "ghi_chu": null
  },
  {
    "ma_goi": "FZ",
    "ngay_su_kien": "2027-01-05",
    "nguoi_lon": 3,
    "tre_em": 0,
    "loai_ve": null,
    "ghi_chu": "hỗ trợ xe lăn"
  },
  {
    "ma_goi": "CSV",
    "ngay_su_kien": "2026-12-01",
    "nguoi_lon": 4,
    "tre_em": 0,
    "loai_ve": "vip",
    "ghi_chu": "hỗ trợ tìm chỗ, người khiếm thị cần hỗ trợ"
  }
]
```

**Link trò chuyện:https://share.gemini.google/kX6VlOTWsmF5**

## 4.3. Báo giá vé bằng Chain-of-Thought

**KET QUA AI**

```text
Tiền người lớn:

Gói vé: SVT – Sân Vận Động (1.200.000 đồng/người lớn)

Số lượng người lớn: 5 người

Phép tính: 
5
×
1.200.000
=
6.000.000
5×1.200.000=6.000.000 đồng

Tiền trẻ em:

Trẻ 8 tuổi và 10 tuổi (từ 5 đến 11 tuổi): tính 70% giá người lớn 
→
2
×
(
1.200.000
×
70
%
)
=
2
×
840.000
=
1.680.000
→2×(1.200.000×70%)=2×840.000=1.680.000 đồng

Bé 3 tuổi (dưới 5 tuổi): miễn phí 
→
0
→0 đồng

Phép tính: 
1.680.000
+
0
=
1.680.000
1.680.000+0=1.680.000 đồng

Tiền vé (Tổng tiền người lớn + tiền trẻ em):

Phép tính: 
6.000.000
+
1.680.000
=
7.680.000
6.000.000+1.680.000=7.680.000 đồng

Giảm giá nhóm:

Số lượng người lớn là 5 người 
→
→ Đạt điều kiện nhóm từ 5 người lớn trở lên, được giảm 5% trên tổng tiền vé.

Tiền giảm giá: 
7.680.000
×
5
%
=
384.000
7.680.000×5%=384.000 đồng

Tiền vé sau giảm: 
7.680.000
−
384.000
=
7.296.000
7.680.000−384.000=7.296.000 đồng

Phụ thu:

Có 1 người lớn chọn khu ghế ưu tiên (phụ thu 300.000 đồng/người, không được giảm giá).

Phép tính: 
1
×
300.000
=
300.000
1×300.000=300.000 đồng

Tổng tiền:

Tổng tiền = tiền vé sau giảm + phụ thu

Phép tính: 
7.296.000
+
300.000
=
7.596.000
7.296.000+300.000=7.596.000 đồng

[RESULT: 7.596.000 đồng]
```

**Link trò chuyện:https://share.gemini.google/yTqcN87vQO0X**

### b) Kiểm tra kết quả AI

đúng

## 4.4. Dây chuyền xử lý khiếu nại – kết quả Trạm 1

**KET QUA AI**

```text
(Dán câu trả lời của AI vào đây (bấm nút Copy dưới câu trả lời) – xoá dòng này)
```

**Link trò chuyện:**
