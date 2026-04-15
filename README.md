[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574039&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** ngohaivan7@gmail.com
**Name:** Ngô Hải Văn

---

## Mô tả

Bài lab xây dựng một ETL Pipeline tự động xử lý dữ liệu sản phẩm từ file JSON. Pipeline thực hiện 4 bước: Extract (đọc dữ liệu), Validate (lọc bỏ record lỗi), Transform (tính giá giảm và chuẩn hoá category), Load (lưu ra CSV). Ngoài ra, bài lab còn nghiên cứu tác động của dữ liệu "rác" đến kết quả của AI Agent.

---

## Cách chạy (How to Run)

### Yêu cầu
```bash
pip install pandas
```

### Chạy ETL Pipeline
```bash
python3 solution.py
```
Kết quả: file `processed_data.csv` sẽ được tạo ra sau khi chạy.

### Chạy Agent Simulation (Stress Test)
```bash
# Bước 1: Tạo dữ liệu rác
python3 generate_garbage.py

# Bước 2: Chạy agent với dữ liệu sạch
python3 agent_simulation.py processed_data.csv

# Bước 3: Chạy agent với dữ liệu rác
python3 agent_simulation.py garbage_data.csv
```

---

## Cấu trúc thư mục

```
├── solution.py              # ETL Pipeline script
├── raw_data.json            # Dữ liệu đầu vào
├── processed_data.csv       # Output của pipeline
├── generate_garbage.py      # Script tạo dữ liệu rác
├── agent_simulation.py      # Script mô phỏng AI Agent
├── experiment_report.md     # Báo cáo thí nghiệm
└── README.md                # File này
```

---

## Kết quả

- Tổng số records đọc vào: 5
- Records hợp lệ (đã xử lý): 3
- Records bị loại: 2 (1 record giá âm, 1 record category rỗng)
- Output: `processed_data.csv` với các cột: id, product, price, category, discounted_price, processed_at
