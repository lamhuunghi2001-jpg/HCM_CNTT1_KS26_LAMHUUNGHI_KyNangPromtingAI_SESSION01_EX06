# HỌ VÀ TÊN: LÂM HỮU NGHỊ
# LỚP: HCM_KS26_CNTT1_KYNANGPROMTING_AI_SESSION01_EX06

## Phần 1: Giải thích hình tượng Chiếc cốc nướcContext Window (bộ nhớ ngữ cảnh) của AI giống như một chiếc cốc nước có dung lượng cố định.

Mỗi lượt chat (câu hỏi của khách + câu trả lời của AI) là một lượng nước được đổ vào cốc.
Cốc có giới hạn (thường vài chục nghìn token). Khi đầy, nước mới đổ vào sẽ tràn và đẩy nước cũ ra ngoài → đó chính là hiện tượng Truncation (cắt bỏ thông tin cũ).
Trong ví dụ của bạn:
Lượt 1: Khách nói “Tôi tên Trần Văn B, đơn #MTX-9988…” → nước chỉ chiếm khoảng 5% cốc, còn trống rất nhiều.
40 lượt tiếp theo (tư vấn rau củ chi tiết) → AI trả lời dài, tích lũy đến khoảng 32.000 token → cốc đầy 100%.
Lượt 42: Khách hỏi về hoàn tiền → token mới tràn vào, đẩy hết thông tin Lượt 1 ra khỏi cốc.
Vì vậy AI không còn nhớ tên khách và mã đơn, phải hỏi lại “Chào chị Mai, xin lại mã đơn?”.
AI không “quên” theo kiểu con người. Nó chỉ không còn thấy thông tin cũ vì thông tin đó đã bị đẩy ra khỏi bộ nhớ tạm thời (Context Window).
## Phần 2: Phương án quản lý RAM bộ nhớPhương án 1: Thao tác phía người dùng (nhân viên CSKH)

Tóm tắt định kỳ: Cứ khoảng 15–20 lượt, nhân viên chủ động nhắc lại thông tin quan trọng dưới dạng ngắn gọn:
“Em xin xác nhận lại: Anh Trần Văn B – đơn #MTX-9988 – mua tại MartX Q1 đúng không ạ?”
→ Đưa thông tin quan trọng lên lại “mặt nước” (gần nhất), giảm nguy cơ bị đẩy ra.
Tách phiên chat: Khi chủ đề chuyển sang hoàn toàn mới (ví dụ từ tư vấn hàng sang khiếu nại hoàn tiền), nên mở phiên chat mới và copy thông tin cốt lõi sang.
Viết ngắn gọn: Tránh để AI trả lời quá dài dòng. Nhắc AI “trả lời ngắn gọn, chỉ tập trung vào câu hỏi”.
Phương án 2: Thiết kế hệ thống (phía kỹ thuật / sản phẩm)
Bộ nhớ dài hạn bên ngoài: Lưu thông tin quan trọng của khách (tên, mã đơn, lịch sử mua hàng) vào database hoặc CRM. Mỗi lần bắt đầu hoặc giữa phiên, hệ thống tự động “đổ” lại các thông tin này vào đầu Context Window.
Cơ chế tóm tắt tự động (Summarization): Hệ thống định kỳ tóm tắt toàn bộ lịch sử hội thoại thành 1 đoạn ngắn (ví dụ 300–500 token) và chỉ giữ bản tóm tắt + vài lượt gần nhất. Cách này giúp giữ được thông tin quan trọng dù phiên chat kéo dài hàng trăm lượt.
Cửa sổ trượt thông minh: Ưu tiên giữ lại các thông tin được đánh dấu quan trọng (tên khách, mã đơn, yêu cầu chính) thay vì cắt theo thứ tự thời gian thuần túy.
Hai phương án trên kết hợp sẽ giúp phiên tư vấn dài không bị “tràn cốc” và AI không còn quên thông tin ngay từ đầu phiên.