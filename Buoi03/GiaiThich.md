# Báo cáo Buổi 3: Game Tic-Tac-Toe $N \times N$ với AI Minimax & Alpha-Beta Pruning

## 1. Mô tả bài toán
Xây dựng chương trình chơi cờ Caro (Tic-Tac-Toe) giữa Người và Máy.
- **Mở rộng:** Không chỉ giới hạn ở bàn cờ 3x3 truyền thống, chương trình cho phép nhập kích thước $N \times N$ (ví dụ: 4x4, 5x5).
- **Quy tắc:** Người chơi nào đạt được $N$ quân liên tiếp (ngang, dọc, chéo) sẽ thắng.
- **Mục tiêu:** Xây dựng AI "bất bại" (hoặc khó đánh bại) sử dụng thuật toán tìm kiếm đối kháng.

## 2. Giải thuật sử dụng

### 2.1. Minimax (Cốt lõi)
Minimax là thuật toán đệ quy dùng để chọn nước đi tối ưu trong các trò chơi đối kháng có tổng bằng không (zero-sum game).
- **MAX (AI):** Luôn cố gắng chọn nước đi có điểm số cao nhất.
- **MIN (Người chơi):** AI giả định người chơi luôn chơi tối ưu, tức là chọn nước đi làm cho điểm số của AI thấp nhất.

### 2.2. Cắt tỉa Alpha-Beta (Tối ưu hóa)
Với bàn cờ lớn, số lượng trạng thái là cực lớn. Alpha-Beta giúp loại bỏ (cắt tỉa) các nhánh cây tìm kiếm không cần thiết mà không ảnh hưởng đến kết quả cuối cùng.
- **Alpha:** Giá trị tốt nhất mà MAX đã tìm thấy.
- **Beta:** Giá trị tốt nhất mà MIN đã tìm thấy.
- Nếu một nhánh có giá trị tệ hơn giá trị đã tìm thấy trước đó, thuật toán sẽ dừng duyệt nhánh đó ngay lập tức.

### 2.3. Giới hạn độ sâu (Depth Limit) - Quan trọng
Đối với bàn cờ $4 \times 4$ trở lên, không gian trạng thái quá lớn ($16!$ trường hợp). Minimax thuần túy sẽ chạy mãi không xong.
- **Giải pháp:** Sử dụng biến `MAX_DEPTH_LIMIT`.
- **Cách hoạt động:** Thuật toán chỉ tính trước một số nước đi nhất định (ví dụ: 5 nước cho bàn 4x4). Nếu chưa tìm thấy thắng/thua tại độ sâu đó, hàm đánh giá (Heuristic) sẽ trả về điểm số ước lượng.

## 3. Cấu trúc chương trình

Chương trình được viết bằng Python, chia thành các hàm chức năng rõ ràng:

### Các hàm xử lý bàn cờ
- **`GetWinner(board, n)`**: Hàm kiểm tra chiến thắng tổng quát cho mọi kích thước $N$. Kiểm tra đủ 4 hướng: Ngang, Dọc, Chéo chính, Chéo phụ.
- **`GetAvailableCells(board)`**: Trả về danh sách các ô còn trống để đi.
- **`PrintBoard(board, n)`**: Vẽ bàn cờ ra màn hình console một cách trực quan, tự động căn chỉnh theo kích thước $N$.

### Các hàm trí tuệ nhân tạo (AI)
- **`minimax(...)`**:
  - Hàm đệ quy thực hiện thuật toán Minimax kết hợp Alpha-Beta.
  - Tích hợp kiểm tra độ sâu: `if depth >= MAX_DEPTH_LIMIT: return 0`.
  - **Hàm lượng giá:**
    - Thắng: $+100 - depth$ (Ưu tiên thắng càng sớm càng tốt).
    - Thua: $-100 + depth$ (Cố gắng kéo dài trận đấu nếu thế cờ thua).
- **`FindBestMove(...)`**:
  - Duyệt qua các nước đi khả thi và gọi `minimax` để lấy điểm số.
  - Chọn nước đi có điểm cao nhất cho AI.
  - **Tối ưu đặc biệt:** Nếu là bàn cờ $4 \times 4$ và là nước đầu tiên, AI sẽ đánh vào giữa để tiết kiệm thời gian tính toán.

## 4. Hướng dẫn sử dụng và Demo

### Bước 1: Khởi chạy
Chạy file code Python. Chương trình sẽ yêu cầu nhập kích thước bàn cờ.

### Bước 2: Nhập thông số
- **Nhập kích thước:** Ví dụ nhập `3` (cho 3x3) hoặc `4` (cho 4x4).
- **Chọn phe:** Nhập `X` (đi trước) hoặc `O` (đi sau).

### Bước 3: Cách chơi
- Bàn cờ được đánh số từ $1$ đến $N \times N$.
- Người chơi nhập con số tương ứng với ô muốn đánh.

### Ví dụ kết quả chạy (Demo 3x3)
*(Chèn ảnh chụp màn hình file ketqua.png của bạn vào đây)*

```text
Máy (O) đang suy nghĩ (Độ sâu: 9)...

 X | 2 | 3 
 ---------
 4 | O | 6 
 ---------
 7 | 8 | 9 

Nhập ô (1-9) cho X: