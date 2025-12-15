# BÁO CÁO THỰC HÀNH MÔN TRÍ TUỆ NHÂN TẠO

- **Họ và tên:** Trương Minh Lạc
- **MSSV:** 2001230426

---

## 📝 Giới thiệu
Repository này là nơi lưu trữ báo cáo và mã nguồn các bài thực hành môn **Trí tuệ Nhân tạo**. Dự án bao gồm các thuật toán tìm kiếm, các trò chơi đối kháng và bài toán tối ưu hóa trên đồ thị.

## 📂 Danh sách bài thực hành

### 1. Bài tập 1: Giải bài toán N-Puzzle (Trò chơi trượt số)
Sử dụng thuật toán tìm kiếm để đưa bảng số từ trạng thái ngẫu nhiên về trạng thái đích.
- **Thuật toán:** Branch and Bound (Nhánh và Cận) / A* Search.
- **Tính năng:**
  - Hỗ trợ nhập kích thước bàn cờ $N \times N$ (3x3, 4x4...).
  - Sử dụng Heuristic (số ô sai vị trí) để tìm đường đi tối ưu.
  - In ra từng bước di chuyển để dẫn đến kết quả.
- **Thư mục:** `Buoi02/`
- **Demo:**
  ![Demo N-Puzzle](Buoi02/ketqua.png)

### 2. Bài tập 2: Cờ Caro (Tic-Tac-Toe) $N \times N$ với AI
Xây dựng AI chơi cờ Caro bất bại (hoặc khó đánh bại) với người chơi.
- **Thuật toán:** Minimax kết hợp Cắt tỉa Alpha-Beta (Alpha-Beta Pruning).
- **Tính năng:**
  - Tùy chỉnh kích thước bàn cờ (3x3, 4x4, 5x5...).
  - **Giới hạn độ sâu (Depth Limit):** Giúp AI tính toán nhanh kể cả với bàn cờ lớn ($4 \times 4$ trở lên).
  - Giao diện Console trực quan, hiển thị bàn cờ sau mỗi nước đi.
- **Thư mục:** `Buoi03/`
- **Demo:**
  ![Demo Tic-Tac-Toe](Buoi03/ketqua.png)

### 3. Bài tập 3: Tô màu đồ thị & Bài toán Người du lịch (TSP)
Giải quyết hai bài toán kinh điển trên đồ thị có sử dụng thư viện đồ họa `ColabTurtle`.
- **Phần A: Tô màu đồ thị (Graph Coloring)**
  - **Mục tiêu:** Tô màu các đỉnh sao cho 2 đỉnh kề nhau không trùng màu.
  - **Thuật toán:** Tham lam (Greedy) dựa trên bậc của đỉnh.
- **Phần B: Bài toán Người du lịch (TSP)**
  - **Mục tiêu:** Tìm lộ trình ngắn nhất đi qua tất cả thành phố và quay về điểm xuất phát.
  - **Thuật toán:** Vét cạn (Brute Force) - Tìm kiếm toàn cục.
- **Thư mục:** `Buoi04/`
- **Demo:**
  ![Demo Graph](Buoi04/ketqua.png)

---

## 🚀 Hướng dẫn cài đặt và chạy

### Yêu cầu hệ thống
- Python 3.x
- Các thư viện cần thiết: `numpy`, `ColabTurtle` (đối với bài đồ thị).

### Cách chạy chương trình
1. **Clone repository về máy:**
   ```bash
   git clone [https://github.com/lacminhtruong/BaoCao-ThucHanhTTNT.git](https://github.com/lacminhtruong/BaoCao-ThucHanhTTNT.git)
