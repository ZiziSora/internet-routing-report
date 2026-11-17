# Hướng dẫn tổ chức thư mục báo cáo Internet Routing

Báo cáo được viết bằng LaTeX. Nội dung được chia thành nhiều tệp để các thành viên có thể viết từng phần riêng, còn `main.tex` ghép các phần thành một báo cáo hoàn chỉnh.

## 1. Cấu trúc thư mục

```text
Report MMTNC Routing/
├── main.tex                         # Tệp chính để biên dịch báo cáo
├── README.md                        # Hướng dẫn tổ chức và bổ sung nội dung
├── references.bib                   # Nơi lưu tài liệu tham khảo
├── preamble/
│   ├── packages.tex                 # Khai báo các gói LaTeX
│   └── formatting.tex               # Font, lề, tiêu đề, chú thích, kiểu mã lệnh
├── frontmatter/
│   ├── cover.tex                    # Trang bìa
│   └── ip_addressing.tex            # Bảng quy hoạch địa chỉ IP
├── chapters/
│   ├── chapter1_overview.tex         # Dự kiến: tổng quan
│   ├── chapter2_configuration.tex   # Triển khai cấu hình mạng
│   ├── chapter3_testing.tex          # Dự kiến: kiểm thử
│   ├── chapter4_advanced.tex         # Dự kiến: nội dung nâng cao
│   └── chapter5_conclusion.tex       # Dự kiến: kết luận
├── sections/
│   ├── part_0.tex                   # Cấu hình cơ bản
│   ├── part_A.tex                   # Nội dung phần A
│   ├── part_B.tex                   # Nội dung phần B
│   ├── part_C.tex                   # Cấu hình OSPF trong AS B
│   ├── part_D.tex                   # Cấu hình BGP
│   └── part_E.tex                   # Nội dung phần E
└── images/
    ├── Logo_HCMUS.png               # Logo dùng trên trang bìa
    └── configuration/
        ├── part_0/                  # Ảnh cấu hình cơ bản, interface, loopback
        ├── part_A/                  # Ảnh minh chứng phần A
        ├── part_B/                  # Ảnh minh chứng phần B
        ├── part_C/                  # Ảnh minh chứng phần C
        ├── part_D/                  # Ảnh minh chứng phần D
        └── part_E/                  # Ảnh minh chứng phần E
```

## 2. Vai trò và cách liên kết các tệp

- **`main.tex`**: quản lý thứ tự toàn bộ báo cáo, nạp thiết lập, trang bìa, bảng địa chỉ IP và các chương; tạo mục lục, danh sách hình và danh sách bảng.
- **`preamble/`**: chứa thiết lập dùng chung. Thêm gói vào `packages.tex`; chỉnh hình thức trình bày trong `formatting.tex` để áp dụng thống nhất.
- **`frontmatter/`**: chứa nội dung đầu báo cáo. Sửa thông tin nhóm tại `cover.tex`, sửa quy hoạch địa chỉ tại `ip_addressing.tex`.
- **`chapters/`**: chứa các chương cấp cao. Mỗi chương dùng `\chapter{...}` và có thể nạp các phần nhỏ bằng `\input{...}`.
- **`sections/`**: chứa nội dung chi tiết từng phần bài thực hành. Dùng `\section`, `\subsection` và các mức nhỏ hơn để tổ chức mục tiêu, cấu hình, kết quả và nhận xét.
- **`images/`**: lưu ảnh được chèn trong báo cáo, phân nhóm theo phần để dễ tìm và tránh nhầm ảnh giữa các nội dung.
- **`references.bib`**: dành cho dữ liệu tài liệu tham khảo. Hiện tệp còn trống và báo cáo chưa cấu hình xuất danh mục tài liệu tham khảo.

Luồng ghép nội dung hiện tại:

```text
main.tex
├── preamble/packages.tex + preamble/formatting.tex
├── frontmatter/cover.tex + frontmatter/ip_addressing.tex
└── chapters/chapter1...chapter5
    └── chapter2_configuration.tex
        ├── sections/part_0.tex
        ├── sections/part_C.tex
        └── sections/part_D.tex
```

**Tình trạng hiện tại:** các chương 1, 3, 4, 5 và các phần A, B, E đang là tệp trống. Chương 2 hiện chỉ nạp phần 0, C và D; ảnh của phần A, B, E đã có trong thư mục nhưng các tệp nội dung tương ứng chưa được nạp vào chương 2.

## 3. Cách bổ sung nội dung

### Viết hoặc cập nhật một phần

1. Mở tệp tương ứng trong `sections/`, ví dụ `sections/part_A.tex`.
2. Viết nội dung theo trình tự: mục tiêu → cấu hình → kết quả kiểm tra → nhận xét. Điều chỉnh các mục theo yêu cầu thực tế của phần đó.
3. Đặt ảnh minh chứng vào `images/configuration/part_A/`.
4. Khi phần đã sẵn sàng, thêm lệnh nạp vào chương phù hợp. Nếu các phần 0–E đều thuộc chương cấu hình, thứ tự trong `chapters/chapter2_configuration.tex` có thể là:

```latex
\chapter{TRIỂN KHAI CẤU HÌNH MẠNG}

\input{sections/part_0}
\input{sections/part_A}
\input{sections/part_B}
\input{sections/part_C}
\input{sections/part_D}
\input{sections/part_E}
```

Các tệp con chỉ chứa nội dung; không thêm `\documentclass`, `\begin{document}` hoặc `\end{document}` vào chúng.

### Đặt tên và chèn ảnh

Giữ cách đặt tên đang dùng: `<thiết_bị>_<nội_dung>.png`, ví dụ `A2_protocols.png`, `B2_route_ospf.png`, `A3_bgp_after.png`. Ưu tiên tên không dấu, không khoảng trắng; thêm `before`/`after` nếu cần so sánh trước và sau thay đổi.

Đường dẫn ảnh được viết từ thư mục gốc chứa `main.tex`, kể cả khi lệnh chèn nằm trong `sections/`:

```latex
\begin{figure}[H]
    \centering
    \includegraphics[width=0.9\textwidth]{images/configuration/part_C/B2_route_ospf.png}
    \caption{Bảng định tuyến OSPF trên router B2}
    \label{fig:part-c-b2-route-ospf}
\end{figure}
```

Đặt nhãn duy nhất cho từng hình, bảng hoặc mục. Tham chiếu bằng `\ref{...}`, ví dụ `Hình~\ref{fig:part-c-b2-route-ospf}`, để số thứ tự tự cập nhật.

### Thêm chương hoặc nhóm ảnh mới

- Tạo chương trong `chapters/`, khai báo `\chapter{...}` và thêm `\input{chapters/ten_tep}` vào đúng vị trí trong `main.tex`.
- Nếu cần ảnh riêng cho kiểm thử hoặc nội dung nâng cao, có thể tạo thêm `images/testing/` hoặc `images/advanced/`. Đây là thư mục đề xuất, chưa có trong cấu trúc hiện tại.

## 4. Biên dịch và phối hợp làm việc

- Lưu các tệp văn bản bằng UTF-8 để giữ đúng tiếng Việt.
- Luôn biên dịch **`main.tex`** từ thư mục gốc. Dùng **XeLaTeX** vì báo cáo sử dụng `fontspec` và font Times New Roman; môi trường biên dịch cần có font này.
- Nếu dùng dòng lệnh, chạy `xelatex main.tex` hai lần để cập nhật mục lục và tham chiếu. Nếu dùng Overleaf, chọn compiler XeLaTeX và tệp chính `main.tex`.
- Mỗi thành viên nên phụ trách tệp nội dung và thư mục ảnh tương ứng. Thống nhất khi sửa `main.tex` hoặc `preamble/` vì các tệp này ảnh hưởng toàn bộ báo cáo.
- Sau khi sửa, kiểm tra PDF: đúng thứ tự phần, ảnh hiển thị rõ, chú thích phù hợp và không có tham chiếu `??`.
- Các tệp sinh ra như `.aux`, `.log`, `.toc`, `.lof`, `.lot`, `.out` là tệp trung gian; không dùng để lưu nội dung hoặc đưa vào quản lý phiên bản. Giữ bản PDF cuối theo quy ước nộp bài của nhóm.
