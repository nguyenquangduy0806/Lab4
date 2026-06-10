# LAB 4: FORECASTING & PREDICTIVE ANALYTICS CHO DỮ LIỆU IOT

### Hệ thống dự báo và phân tích xu hướng dữ liệu IoT

---

## 1. Giới thiệu

Đề tài xây dựng hệ thống AIoT giúp:

* Thu thập và phân tích dữ liệu cảm biến IoT.
* Dự báo giá trị dữ liệu trong tương lai bằng Machine Learning.
* Đánh giá mức độ rủi ro vận hành.
* Sinh cảnh báo và khuyến nghị tự động.
* Deploy mô hình dự báo bằng FastAPI.

---

## Pipeline hệ thống

```text
Raw Telemetry Data
   ↓
Data Cleaning
   ↓
Time-Series Feature Engineering
   ↓
Lag & Rolling Features
   ↓
Train Forecast Model
   ↓
Forecast Prediction
   ↓
Risk Evaluation
   ↓
Recommendation Generation
   ↓
Forecast Log
   ↓
FastAPI Deployment
```

---

## Cấu trúc project

```text
lab4_aiot_forecasting_predictive_analytics_uci_appliances/
│
├── data/
│   └── sample_energydata_complete.csv
│
├── notebooks/
│   └── 01_forecasting_predictive_analytics.ipynb
│
├── src/
│   ├── download_data.py
│   ├── train_forecast.py
│   ├── plot_results.py
│   ├── app.py
│   ├── test_api.py
│   ├── test_api_local.py
│   └── utils.py
│
├── models/
│
├── outputs/
│
├── figures/
│
├── diagrams/
│
└── requirements.txt
```

---

## 2. Dataset

### File dữ liệu chính

```text
data/energydata_complete.csv
```

### Các trường dữ liệu

* Date
* Appliances
* Lights
* Temperature
* Humidity
* Weather Variables
* Indoor Environment Data

### Nguồn dữ liệu

Bộ dữ liệu sử dụng trong bài thực hành là UCI Appliances Energy Prediction Dataset, ghi nhận mức tiêu thụ điện năng và các thông số môi trường trong nhà theo chu kỳ 10 phút.

---

## 3. Xử lý dữ liệu

Hệ thống thực hiện:

* Loại bỏ dữ liệu thiếu và dữ liệu không hợp lệ.
* Chuẩn hóa dữ liệu thời gian.
* Xây dựng đặc trưng chuỗi thời gian.
* Tạo Lag Features.
* Tính Rolling Mean.
* Tính Rolling Standard Deviation.
* Chuẩn bị dữ liệu đầu vào cho mô hình dự báo.

### Output sinh ra

```text
outputs/feature_dataset.csv
outputs/forecast_dataset.csv
```

---

## 4. AI Model

### Model sử dụng

```text
Baseline Forecasting
Machine Learning Regression
Advanced Boosting Model
```

### Train/Test Split

* 75% Train
* 25% Test

### Output model

```text
models/forecast_model_bundle_v1.joblib
```

### File đánh giá

```text
outputs/forecast_metrics.json
```

---

## 5. Forecasting Analytics

Hệ thống sử dụng:

* Time Series Forecasting
* Regression Prediction
* Forecast Error Analysis
* Risk Classification

### Mục đích

* Dự báo mức tiêu thụ điện năng.
* Phân tích xu hướng dữ liệu IoT.
* Đánh giá rủi ro vận hành.
* Hỗ trợ ra quyết định cho hệ thống.

---

## 6. FastAPI Deployment

### Chạy API

```bash
uvicorn src.app:app --reload
```

### Swagger Docs

```text
http://127.0.0.1:8000/docs
```

### API Endpoints

| Endpoint      | Chức năng                |
| ------------- | ------------------------ |
| `/health`     | Kiểm tra API             |
| `/model-info` | Thông tin mô hình        |
| `/forecast`   | Dự báo dữ liệu tương lai |

---

## 7. Output Files

```text
outputs/
├── forecast_metrics.json
├── forecast_test_predictions.csv
├── forecast_log.csv
└── api_test_result.json

models/
└── forecast_model_bundle_v1.joblib

figures/
├── forecast_vs_actual.png
├── forecast_error_over_time.png
└── model_comparison_mae.png
```

---

## 8. Decision Rule

### Rule 1

```text
forecast_error < 20
```

→ LOW_RISK

---

### Rule 2

```text
20 ≤ forecast_error < 50
```

→ MEDIUM_RISK

---

### Rule 3

```text
forecast_error ≥ 50
```

→ HIGH_RISK

---

## 9. Kết quả đạt được

Hệ thống đã:

* Xây dựng pipeline Forecasting hoàn chỉnh cho dữ liệu IoT.
* Huấn luyện thành công mô hình dự báo.
* Đánh giá mô hình bằng MAE, RMSE và MAPE.
* Sinh forecast log và recommendation log.
* Triển khai API bằng FastAPI.
* Hỗ trợ dự báo và đánh giá rủi ro vận hành.

---

## 10. Kết quả huấn luyện mô hình

Sau khi thực hiện quá trình tiền xử lý dữ liệu và xây dựng đặc trưng chuỗi thời gian, hệ thống đã tạo thành công mô hình:

```text
models/forecast_model_bundle_v1.joblib
```

Mô hình sử dụng các đặc trưng:

```text
Giá trị tiêu thụ hiện tại
Lag Features
Rolling Mean
Rolling Standard Deviation
Nhiệt độ môi trường
Độ ẩm môi trường
Thông tin thời gian
```

---

## 11. Kết quả đánh giá mô hình

Hệ thống sinh file:

```text
outputs/forecast_metrics.json
```

Các chỉ số đánh giá:

* MAE (Mean Absolute Error)
* RMSE (Root Mean Squared Error)
* MAPE (Mean Absolute Percentage Error)

### Ý nghĩa

* MAE càng nhỏ thì mô hình càng chính xác.
* RMSE phản ánh mức độ sai số lớn.
* MAPE cho biết tỷ lệ sai số theo phần trăm.

---

## 12. Kết quả dự báo

Hệ thống tạo file:

```text
outputs/forecast_test_predictions.csv
```

Ví dụ:

```text
Actual Value    Predicted Value    Error
120             118                2
135             130                5
110             113                3
145             140                5
160             158                2
```

### Nhận xét

* Giá trị dự báo gần với giá trị thực tế.
* Sai số dự báo thấp.
* Mô hình học được xu hướng tiêu thụ điện năng theo thời gian.

---

## 13. Kết quả ghi log dự báo

File:

```text
outputs/forecast_log.csv
```

Bao gồm:

```text
actual_value predicted_value forecast_error risk_level recommendation
120 118 2 Low Continue Monitoring
200 240 40 Medium Check Equipment
300 380 80 High Immediate Inspection
```

### Ý nghĩa

```text
Low Risk
Hệ thống hoạt động bình thường.
Không cần hành động đặc biệt.

Medium Risk
Xuất hiện dấu hiệu tiêu thụ điện bất thường.
Cần kiểm tra thiết bị.

High Risk
Dự báo mức tiêu thụ tăng mạnh.
Có nguy cơ mất ổn định hệ thống.
Cần kiểm tra ngay.
```

---

## 14. Kết quả triển khai API

### Endpoint Health Check

```text
API:

GET /health
```

Kết quả:

```json
{
  "status": "ok",
  "model_loaded": true
}
```

Ý nghĩa:

```text
Server hoạt động bình thường.
Model được load thành công.
```

---

### Endpoint Forecast

```text
API:

POST /forecast
```

Ví dụ kết quả:

```json
{
  "predicted_value": 245.6,
  "risk_level": "Medium",
  "recommendation": "Check Equipment",
  "safety_note": "Human verification required"
}
```

Ý nghĩa:

```text
Trả về giá trị dự báo.
Đánh giá mức độ rủi ro.
Đưa ra khuyến nghị phù hợp.
Yêu cầu xác nhận của người vận hành trước khi thực hiện hành động.
```

---

## KẾT LUẬN

Lab 4 đã xây dựng thành công hệ thống Forecasting & Predictive Analytics cho dữ liệu IoT. Hệ thống có khả năng:

* Thu thập dữ liệu cảm biến.
* Xây dựng đặc trưng chuỗi thời gian.
* Huấn luyện mô hình dự báo.
* Đánh giá bằng MAE, RMSE và MAPE.
* Sinh cảnh báo rủi ro.
* Đề xuất hành động vận hành.
* Triển khai thành công bằng FastAPI.

Hệ thống có thể được áp dụng trong các bài toán thực tế như quản lý năng lượng, nhà thông minh, nhà máy thông minh, kho lạnh thông minh và các hệ thống AIoT quy mô lớn.
