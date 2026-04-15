# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-XXXX
**Name:** Ngô Hải Văn
**Date:** 2026-04-15

---

## 1. Kết quả thí nghiệm

Chạy `agent_simulation.py` với 2 bộ dữ liệu và ghi lại kết quả:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | "the best choice is Laptop at $1200" | 9 | Kết quả hợp lý, Laptop là sản phẩm electronics đắt nhất trong dữ liệu sạch |
| Garbage Data (`garbage_data.csv`) | "the best choice is Nuclear Reactor at $999999" | 1 | Kết quả sai hoàn toàn do outlier cực đoan trong dữ liệu rác |

---

## 2. Phân tích & nhận xét

### Tai sao / Phan tich: Tại sao Agent trả lời sai khi dùng Garbage Data?

Khi sử dụng dữ liệu rác (`garbage_data.csv`), Agent đã đưa ra câu trả lời hoàn toàn sai lệch vì dữ liệu đầu vào chứa nhiều vấn đề nghiêm trọng về chất lượng.

Thứ nhất, **Duplicate IDs**: record id=1 xuất hiện hai lần (Laptop và Banana), gây nhầm lẫn khi truy vấn và có thể dẫn đến kết quả không nhất quán.

Thứ hai, **Wrong data types**: sản phẩm "Broken Chair" có giá là chuỗi "ten dollars" thay vì số, khiến các phép tính số học bị lỗi hoặc bị bỏ qua.

Thứ ba, **Extreme Outlier**: "Nuclear Reactor" có giá $999,999 — một giá trị bất thường cực đoan. Agent chọn sản phẩm có giá cao nhất nên đã chọn nhầm outlier này làm "best choice", mặc dù đây rõ ràng là dữ liệu không đáng tin cậy.

Thứ tư, **Null values**: record cuối có id=None và category=None, gây ra lỗi khi lọc dữ liệu theo category.

Tóm lại, dù logic của Agent hoàn toàn đúng, nhưng vì dữ liệu đầu vào bị "nhiễm độc", kết quả trả ra vẫn sai. Đây là minh chứng rõ ràng cho nguyên tắc "Garbage In, Garbage Out" trong khoa học dữ liệu.

---

## 3. Kết luận

**Quality Data > Quality Prompt?** — Đồng ý hoàn toàn.

Dù Agent có logic tốt và prompt rõ ràng, nếu dữ liệu đầu vào kém chất lượng thì kết quả vẫn sai. Việc xây dựng pipeline ETL với bước Validate kỹ lưỡng là nền tảng bắt buộc trước khi đưa dữ liệu vào bất kỳ hệ thống AI nào. Chất lượng dữ liệu quyết định chất lượng kết quả — không có prompt nào có thể bù đắp cho dữ liệu xấu.
