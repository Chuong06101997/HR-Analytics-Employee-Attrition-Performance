# Trong 100 người mới vào công ty năm nay, khoảng 35 người sẽ không còn ở đó vào năm sau.

Bạn đã biết ai trong số họ đã nghỉ. Điều đó nằm sẵn trong hệ thống rồi.

Câu hỏi khó hơn là: trong những người **đang** ngồi cạnh bạn lúc này, ai sắp đi tiếp — và ai mới thực sự đáng để giữ lại?

Đây là câu hỏi mà phân tích này cố gắng trả lời.

---

## Vấn đề này tốn kém cỡ nào?

Một nhân viên mới nghỉ trước 1 năm không chỉ tốn tiền tuyển lại. Đó là thời gian đào tạo chưa sinh lời, giờ quản lý huấn luyện người sắp rời đi, kiến thức mất đi trước khi truyền lại được.

Lãnh đạo thường đã có sẵn giả thuyết: "Tăng lương", "Giảm OT", "Cải thiện tinh thần". Nghe hợp lý.

Nhưng sai nhóm, sai lý do — vừa tốn ngân sách, vừa không giải quyết được gì.

---

## Phát hiện đã xác nhận (bằng chứng mạnh)

Hai điều sau đã qua kiểm định thống kê (chi-square, z-test, CI hẹp) và được xếp bậc **Strong evidence** — đủ tin để làm nền cho hành động:

**1. Nhân viên mới nghỉ nhiều hơn hẳn nhân viên lâu năm.**
Tỷ lệ nghỉ việc ở nhóm dưới 1 năm là 34.9%, ở nhóm trên 11 năm là 8.1% — chênh nhau khoảng **4.3 lần**. Đây là so sánh mô tả trực tiếp trên dữ liệu, không phải một con số đã kiểm soát biến nhiễu.

**2. Trong nhóm nhân viên mới, người phải làm nhiều OT nghỉ việc nhiều hơn rõ rệt.**
55.1% (có OT) so với 25.3% (không OT) — chênh khoảng **2.2 lần**. Đã kiểm tra thử xem có phải chỉ do đặc thù một phòng ban (ví dụ Sales) gây ra không — không phải, hiệu ứng này vẫn còn ở cả nhóm Sales lẫn ngoài Sales, chỉ là ở Sales rõ hơn.

Cả hai con số trên chỉ mô tả sự khác biệt quan sát được, **không phải mức độ rủi ro tăng thêm do OT hay do làm mới gây ra** — dữ liệu không cho phép khẳng định nhân quả.

---

## Giả thuyết đang theo dõi (chưa đủ để hành động)

**Đi công tác nhiều (Business Travel_Frequently)** — tín hiệu khá rõ trong nhóm quan sát, nhưng mẫu chỉ có 36 người, nên khoảng tin cậy rất rộng. Xếp mức **Moderate**: đáng ghi nhận, nhưng không nên dùng làm căn cứ chính cho chính sách.

**Lương thấp hơn mặt bằng cùng vị trí** và **mức độ hài lòng công việc thấp** — có chênh lệch giữa người nghỉ và người ở lại, nhưng chênh lệch nhỏ và không đủ mạnh sau khi soát lại. Xếp mức **Weak/exploratory**: nên tiếp tục theo dõi, chưa nên ra chính sách lương hay khảo sát diện rộng chỉ dựa vào hai điều này.

**Tương tác giữa OT và mức hài lòng** (ví dụ "OT càng làm người không hài lòng càng dễ nghỉ") — đã kiểm định riêng, **không tìm thấy bằng chứng** cho hiệu ứng cộng hưởng này. Coi như hai yếu tố độc lập.

---

## Khuyến nghị hành động

1. **Ưu tiên nguồn lực giữ chân vào 12 tháng đầu tiên** — đây là giai đoạn rủi ro cao nhất theo phát hiện #1, không nên rải đều cho mọi nhân viên.
2. **Trong nhóm nhân viên mới, rà soát lại việc phân bổ OT trước tiên** — đây là đòn bẩy rõ ràng nhất và HR có thể can thiệp trực tiếp (khác với nơi ở hay tuổi tác). Ưu tiên kiểm tra ở Sales trước vì hiệu ứng rõ nhất ở đó.
3. **Chưa vội triển khai chính sách lương hay khảo sát tinh thần diện rộng** — nên thử nghiệm nhỏ (pilot) trước, đo hiệu quả thật, rồi mới nhân rộng.
4. **Dùng công cụ xếp hạng rủi ro như một gợi ý ưu tiên gọi ai vào nói chuyện trước** — không dùng để tự động ra quyết định (nghỉ việc, lương, đánh giá) cho từng cá nhân. Luôn cần người review lại.

---

## Giới hạn cần lưu ý trước khi dùng

- Dữ liệu mẫu công khai (IBM, qua Kaggle) — không phải dữ liệu công ty cụ thể nào; đây là cách tiếp cận minh hoạ, không phải kết luận áp dụng ngay cho một tổ chức thật.
- Chỉ là một lát cắt tại một thời điểm (không có ngày vào/ngày nghỉ thật) — nên mọi phát hiện chỉ là "A và B có xu hướng đi cùng nhau", không phải "A gây ra B".
- Không có dữ liệu phỏng vấn nghỉ việc thật, không phân biệt được nghỉ tự nguyện hay bị cho nghỉ — nên không biết chắc lý do thật khi nhân viên rời đi.
- Công cụ xếp hạng rủi ro ra con số phần trăm, nhưng con số đó **không nên đọc theo nghĩa đen** ("80%" không có nghĩa đúng 80% sẽ nghỉ) — chỉ đáng tin ở việc xếp hạng ai rủi ro hơn ai.
- Không có cơ sở để khẳng định 1.470 nhân viên này đại diện cho một tổng thể nào khác — mọi kết luận chỉ nằm trong phạm vi dữ liệu này.

---

**Nếu dùng thật, phân tích này giúp HR biết nên gọi ai vào phòng trước để giữ chân, thay vì đoán mò hoặc chờ đến lúc họ nộp đơn nghỉ mới biết.**

---

## Chi tiết kỹ thuật (tóm tắt, xem đầy đủ trong notebook)

- Dữ liệu: 1.470 nhân viên, IBM HR Attrition (Kaggle), snapshot một thời điểm.
- "Nghỉ sớm" = `YearsAtCompany ≤ 1`.
- Model: Logistic Regression, chọn thay vì Random Forest vì diễn giải tốt hơn cho HR (hiệu năng hai model tương đương qua 5-fold CV). ROC-AUC ≈ 0.78–0.79.
- Toàn bộ test thống kê (loại test, p-value, OR, CI), bậc bằng chứng chi tiết, và log quyết định: xem notebook và `Decision_Log.md` đi kèm.
