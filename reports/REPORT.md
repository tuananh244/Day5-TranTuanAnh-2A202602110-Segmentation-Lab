# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: Trần Tuấn Anh
- Ngày / CVAT local: 17/09/2026
- Công cụ đã dùng: CVAT Local

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3/3 | 20 |
| medium_instance | medium_instance.zip | 3/ 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2/2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: ảnh 000000181542.jpg/ phần `motorcycle` `id 6`
- Class và quy tắc tôi dùng để chọn biên: `motorcycle`, quy tắc *vật bị che: chỉ gán phần nhìn thấy, vẫn là một instance"*
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: "Không dùng"
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.
Em sử dụng tool `Draw a Mask` bởi vì cái xe đang bị che đi một phần ở giữa bởi 1 `person`, vì vậy em sử dụng tool này để tạo ra 1 chiếc xe cùng `id` (bỏ qua phần bị che), thể hiện rõ đây là `motorcycle` và đang `bị che`

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `medium_instance, 000000181542.jpg, person_id_02`
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: các nhân tố `person` bị gộp với nhau.
- Bằng chứng tôi nhìn thấy: annotation `id 2` class `person` có bbox mask cho toàn thể, thay vì dùng cho từng người.
- Quy tắc và hành động sửa: theo quy tắc "mỗi người là một instance dù nhỏ/ở xa", cần tách annotation id 2 thành nhiều mask riêng, mỗi người một id, thay vì một mask gộp.
- Sau sửa đã Save và export lại chưa? chưa

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `000000458325.jpg`, cụm `car id 57–60` | (a) Đây là 4 xe hơi riêng biệt đậu sát nhau, mỗi xe một mask nhỏ; (b) đây là 2–3 xe thật sự bị tách quá nhiều (over-split) do ranh giới mờ ở khoảng cách xa | 4 bbox chồng lấn khá nhiều trong khi kích thước mỗi box rất nhỏ - khó phân biệt bằng mắt xe nào tách với xe nào ở độ phân giải này | Cho em hỏi ở khoảng cách xa thế này, nếu ranh giới giữa 2 xe không chắc chắn, nên ưu tiên tách nhiều instance nhỏ hay gộp lại thành 1 vùng "cluster xe" nếu không chắc số lượng chính xác?|