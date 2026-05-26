🚀 LAB 4 — Forecasting & Predictive Analytics cho AIoT
Dự báo tiêu thụ điện năng bằng Machine Learning + FastAPI

Từ phát hiện bất thường → dự báo tương lai → phân tích rủi ro → khuyến nghị vận hành.

📌 Tổng quan dự án

Đây là project xây dựng hệ thống Forecasting cho AIoT sử dụng:

Dữ liệu telemetry IoT
Machine Learning cho time-series
FastAPI deployment
Phân tích rủi ro vận hành

Hệ thống sử dụng bộ dữ liệu:

UCI Appliances Energy Prediction Dataset

để dự đoán:

mức tiêu thụ điện năng của thiết bị trong tương lai
🎯 Mục tiêu chính

Project thực hiện:

Xây dựng pipeline forecasting hoàn chỉnh
Tạo feature engineering cho time-series
Tránh data leakage
So sánh baseline và ML models
Deploy API bằng FastAPI
Sinh risk level và recommendation 
🧠 Khác biệt giữa Lab 3 và Lab 4
Lab 3	Lab 4
Anomaly Detection	Forecasting
“Hệ thống có bất thường không?”	“Giá trị sắp tới sẽ là bao nhiêu?”
Output: anomaly_score	Output: predicted_value
Phát hiện lỗi hiện tại	Dự báo tương lai
🏗️ Pipeline Forecasting
UCI telemetry
    ↓
Feature Engineering
    ↓
Time-series Split
    ↓
Baseline Models
    ↓
Machine Learning Models
    ↓
Forecast Prediction
    ↓
Risk Analysis
    ↓
Recommendation
    ↓
FastAPI Deployment
📂 Cấu trúc project
lab4_aiot_forecasting_predictive_analytics_uci_appliances/
│

├── data/

├── diagrams/

├── figures/

├── models/

├── notebooks/

├── outputs/

├── src/

├── README.md

└── requirements.txt

📊 Dataset sử dụng
UCI Appliances Energy Prediction Dataset

Nguồn:
https://archive.ics.uci.edu/dataset/374/appliances+energy+prediction

Target
Appliances

Lượng điện năng tiêu thụ của thiết bị gia dụng (Wh).

Chu kỳ lấy mẫu
10 phút/lần
Dữ liệu gồm
nhiệt độ
độ ẩm
áp suất
tốc độ gió
ánh sáng
lịch sử tiêu thụ điện
⚙️ Feature Engineering

Hệ thống sử dụng nhiều kỹ thuật time-series.

⏳ Lag Features

Dùng dữ liệu quá khứ để dự báo tương lai.

Ví dụ:

appliances_lag_1
appliances_lag_6
appliances_lag_24

Ý nghĩa:

giá trị trước 1 bước
trước 6 bước
trước 24 bước
📈 Rolling Statistics
rolling_mean
rolling_std

Dùng để lấy:

xu hướng trung bình
độ biến động
🔄 Delta Features
appliances_delta_1
appliances_delta_6

Giúp model biết:

điện năng đang tăng nhanh hay giảm nhanh.
🕒 Time Features
hour
dayofweek
month
is_weekend

Giúp model học:

hành vi theo giờ
theo ngày
theo cuối tuần.
🤖 Các model sử dụng
Baseline Models
Last Value Baseline
Moving Average Baseline
Machine Learning Models
Linear Regression
Random Forest
Gradient Boosting
📉 So sánh hiệu năng model
MAE Comparison
<img width="1600" height="720" alt="model_comparison_mae" src="https://github.com/user-attachments/assets/c36e3067-eab8-4fc5-b94e-6027f3bbe9eb" />
Model	MAE
Last Value Baseline	~15
Moving Average	~22
Linear Regression	~13 (tốt nhất)
Random Forest	~14
Gradient Boosting	~14
🏆 Model tốt nhất
linear_regression_v1

Linear Regression cho:

MAE thấp nhất
tổng quát hóa tốt
ít overfit hơn Random Forest.
📈 Forecast vs Actual
<img width="1920" height="800" alt="forecast_vs_actual" src="https://github.com/user-attachments/assets/49849aad-d45f-40f8-8607-f7cb27f80beb" />

Biểu đồ cho thấy:

prediction bám khá sát actual value
model học được xu hướng tiêu thụ điện.

Tuy nhiên:

ở các spike lớn
model vẫn dự đoán thấp hơn thực tế.
📉 Forecast Error Over Time
<img width="1920" height="640" alt="forecast_error_over_time" src="https://github.com/user-attachments/assets/0a858a80-9b8d-4f89-8c10-8da69c441194" />

Sai số dự báo:

forecast_error = predicted_value - actual_value

Các đoạn âm sâu cho thấy:

model bị under-estimate
hệ thống có spike điện năng bất ngờ.
🧪 Evaluation Metrics

Project sử dụng:

MAE
RMSE
MAPE
Bias

Forecasting dùng regression metrics thay vì:

Precision
Recall
F1-score
🔒 Safety Design

Nguyên tắc quan trọng:

Forecast output KHÔNG phải actuator command.

Hệ thống:

dự báo
phân tích rủi ro
sinh recommendation
cần xác nhận trước khi điều khiển thiết bị thật

=> tránh AI tự động điều khiển sai.
