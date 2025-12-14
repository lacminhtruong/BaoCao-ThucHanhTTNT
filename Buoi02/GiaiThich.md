# Báo cáo: Giải bài toán N-Puzzle bằng thuật toán Branch and Bound

## 1. Giới thiệu bài toán
Bài toán N-Puzzle (hay trượt số) bao gồm một bảng vuông kích thước $N \times N$ với $N^2 - 1$ ô số và 1 ô trống (được biểu diễn bằng số 0).
- **Mục tiêu:** Di chuyển các ô số (bằng cách trượt vào ô trống) để đưa bảng từ trạng thái ban đầu (*Initial State*) về trạng thái đích (*Final State*).
- **Quy tắc:** Chỉ có thể di chuyển các ô nằm cạnh ô trống (trên, dưới, trái, phải).

## 2. Thuật toán sử dụng: Branch and Bound (Nhánh và Cận)
Để giải quyết bài toán này và tìm ra đường đi tối ưu, chương trình sử dụng kỹ thuật **Branch and Bound** (Nhánh và Cận) kết hợp với **Hàng đợi ưu tiên** (Priority Queue).

### Hàm chi phí (Cost Function)
Tại mỗi trạng thái (mỗi node), chi phí được tính theo công thức:
$$C(x) = g(x) + h(x)$$

Trong đó:
- **$g(x)$ (Level):** Chi phí thực tế để đi từ trạng thái ban đầu đến trạng thái hiện tại (số bước đã di chuyển).
- **$h(x)$ (Heuristic):** Chi phí ước lượng để đi từ trạng thái hiện tại đến đích. Trong bài này, heuristic là **số lượng ô đặt sai vị trí** (Misplaced Tiles).

### Cơ chế hoạt động
1.  **Khởi tạo:** Bắt đầu từ trạng thái gốc, tính chi phí và đưa vào hàng đợi ưu tiên (Min-Heap).
2.  **Vòng lặp:**
    - Lấy node có chi phí thấp nhất ($C(x)$ nhỏ nhất) ra khỏi hàng đợi.
    - Nếu chi phí $h(x) = 0$ (không còn ô sai vị trí) $\rightarrow$ Đã tìm thấy đích $\rightarrow$ In đường đi và kết thúc.
    - Nếu chưa đến đích: Sinh ra các trạng thái con (di chuyển ô trống lên, xuống, trái, phải).
    - Tính chi phí cho các node con và đưa chúng vào hàng đợi ưu tiên để xét tiếp.
3.  **Cắt tỉa:** Hàng đợi ưu tiên giúp thuật toán luôn mở rộng hướng đi có triển vọng nhất (chi phí thấp nhất) trước, giúp tối ưu hóa quá trình tìm kiếm.

## 3. Cấu trúc chương trình (Code Python)

### Các Class chính
- **`class priorityQueue`**: Quản lý danh sách các node đang chờ xử lý. Sử dụng `heapq` của Python để đảm bảo luôn lấy ra node có chi phí thấp nhất.
- **`class nodes`**: Đại diện cho một trạng thái của bàn cờ. Lưu trữ:
    - `parent`: Node cha (để truy vết đường đi).
    - `mats`: Ma trận hiện tại.
    - `empty_tile_posi`: Vị trí số 0.
    - `costs`: Số ô sai vị trí ($h(x)$).
    - `levels`: Số bước đã đi ($g(x)$).

### Các Hàm quan trọng
- **`calculateCosts(mats, final)`**: Hàm Heuristic. Đếm số lượng ô trong ma trận hiện tại khác với ma trận đích (bỏ qua ô trống).
- **`newNodes(...)`**: Sinh ra một trạng thái mới khi di chuyển ô trống.
- **`solve(...)`**: Hàm chính thực thi thuật toán Branch and Bound.

## 4. Hướng dẫn sử dụng và Kết quả
Chương trình cho phép người dùng nhập kích thước $N$ để chọn bài toán tương ứng.

### Cách chạy:
1.  Chạy file code Python.
2.  Nhập kích thước bàn cờ ($n$) từ bàn phím.
    - Nhập `3`: Giải bài toán 8-puzzle ($3 \times 3$).
    - Nhập `4`: Giải bài toán 15-puzzle ($4 \times 4$).
    - Nhập `5`: Giải bài toán 24-puzzle ($5 \times 5$).
3.  Chương trình sẽ tự động tải ma trận Input/Output tương ứng đã được định nghĩa sẵn và in ra từng bước di chuyển.

### Ví dụ kết quả (với N=3):
```text
Nhập kích thước n của bàn cờ (ví dụ 3, 4, 5): 
3

Đang giải bài toán...
Đường đi đến nghiệm:
1 2 3 
5 6 0 
7 8 4 

1 2 3 
5 0 6 
7 8 4 

... (các bước di chuyển) ...

1 2 3 
5 8 6 
0 7 4