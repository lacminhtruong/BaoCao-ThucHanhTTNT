# Báo cáo Thực hành: Tô màu đồ thị và Bài toán Người du lịch (TSP)

## Phần 1: Bài toán Tô màu đồ thị (Graph Coloring)

### 1.1. Mô tả bài toán
Tô màu các đỉnh của một đồ thị sao cho **không có hai đỉnh nào kề nhau (nối với nhau bằng một cạnh) có cùng màu**. Mục tiêu là sử dụng số lượng màu ít nhất có thể.

### 1.2. Giải thuật sử dụng: Tham lam (Greedy Algorithm)
Chương trình sử dụng chiến lược tham lam dựa trên bậc của đỉnh (tương tự thuật toán Welsh-Powell):
1.  **Tính bậc (Degree):** Tính số lượng cạnh nối của mỗi đỉnh.
2.  **Sắp xếp:** Sắp xếp các đỉnh theo thứ tự bậc giảm dần (ưu tiên tô các đỉnh có nhiều kết nối trước vì chúng khó tô nhất).
3.  **Tô màu:** Duyệt qua danh sách đỉnh đã sắp xếp:
    - Kiểm tra màu của các đỉnh hàng xóm (đỉnh kề).
    - Chọn màu đầu tiên trong danh sách màu (Blue, Red, Yellow...) mà chưa bị hàng xóm sử dụng.

### 1.3. Giải thích Code
- **Input:**
  - Code hỗ trợ đọc Ma trận kề từ file `dothi.txt`.
  - Hoặc sử dụng ma trận `G` cứng (hardcoded) trong trường hợp demo đồ họa.
- **Xử lý chính:**
  - `bac.append(sum(G[i]))`: Tính bậc của đỉnh.
  - Vòng lặp `sortedNode`: Sắp xếp đỉnh dựa trên bậc.
  - `if setTheColor in colorDict[neighbor_name]`: Loại bỏ màu đã dùng khỏi danh sách màu khả dụng của các đỉnh kề.
- **Trực quan hóa (ColabTurtle):**
  - Các đỉnh được sắp xếp trên một đường tròn bằng công thức lượng giác:
    $$x = center\_x + radius \times \cos(\alpha)$$
    $$y = center\_y + radius \times \sin(\alpha)$$
  - Sử dụng thư viện `ColabTurtle` để vẽ đỉnh, cạnh nối và tô màu tương ứng với kết quả thuật toán.

---

## Phần 2: Bài toán Người du lịch (Traveling Salesman Problem - TSP)

### 2.1. Mô tả bài toán
Một người giao hàng (Shipper) cần xuất phát từ thành phố A, đi qua tất cả các thành phố khác đúng một lần và quay trở về A. Tìm lộ trình có **tổng quãng đường ngắn nhất**.

### 2.2. Giải thuật sử dụng: Vét cạn (Brute Force)
Do số lượng thành phố nhỏ ($N=7$), ta có thể sử dụng phương pháp vét cạn để đảm bảo tìm ra kết quả chính xác nhất (Global Optimum).

**Các bước thực hiện:**
1.  Cố định điểm xuất phát là đỉnh đầu tiên (A - index 0).
2.  Liệt kê tất cả các hoán vị (cách sắp xếp) của các đỉnh còn lại ($N-1$ đỉnh).
    - Sử dụng thư viện `itertools.permutations`.
3.  Với mỗi hoán vị, tạo thành một lộ trình khép kín:
    $$A \rightarrow P_1 \rightarrow P_2 \rightarrow \dots \rightarrow P_{n-1} \rightarrow A$$
4.  Tính tổng độ dài của từng lộ trình. Nếu gặp cạnh có trọng số $0$ (không có đường đi), coi như độ dài là Vô cực (`INF`).
5.  So sánh và giữ lại lộ trình có tổng độ dài nhỏ nhất.

### 2.3. Giải thích Code
- **Dữ liệu:** Ma trận trọng số `G` (Ma trận kề có trọng số), trong đó `G[i][j]` là khoảng cách từ $i$ đến $j$.
- **Hàm `tinh_tong_quang_duong`:** Cộng dồn khoảng cách các chặng. Trả về `float('inf')` nếu đường đi bị đứt đoạn.
- **Mô phỏng:**
  - Sau khi tìm được `duong_di_ngan_nhat`, chương trình sử dụng Turtle để vẽ lại hành trình.
  - Con rùa (đại diện cho Shipper) đổi màu đỏ (`color("red")`) và di chuyển theo đúng thứ tự các đỉnh trong lộ trình tối ưu.

---

## 3. Kết quả chạy chương trình
*(Phần này em sẽ demo trực tiếp trên Google Colab)*

1.  **Tô màu đồ thị:** Các đỉnh kề nhau có màu khác nhau, hình ảnh trực quan rõ ràng.
2.  **TSP:** Chương trình in ra lộ trình tối ưu và tổng quãng đường (km), đồng thời mô phỏng đường đi của Shipper trên bản đồ.