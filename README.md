#  StockPriceVN – Phân tích giá cổ phiếu VN30 với Hadoop & Spark

##  1. Giới thiệu  
Dự án này thực hiện **phân tích dữ liệu giá cổ phiếu của rổ VN30** bằng công nghệ **Big Data**.  
Sử dụng **Apache Hadoop (HDFS)** để lưu trữ dữ liệu và **Apache Spark** để xử lý song song.  

 **Nguồn dữ liệu:**  
[Kaggle – Stock Prices VN30 Index Vietnam](https://www.kaggle.com/datasets/nguyenngocphung/stock-prices-vn30-indexvietnam/data)

---

##  2. Nội dung chính  
- **Tập dữ liệu:** Gồm giá mở cửa, cao, thấp, đóng cửa và khối lượng giao dịch của 30 mã cổ phiếu thuộc VN30.  
- **Hệ thống triển khai:** Cluster Docker gồm:
  - `namenode`, `datanode` (Hadoop HDFS)
  - `spark-master`, `spark-worker`
  - `jupyter` (PySpark notebook)
- **Các bước thực hiện:**  
  1. Dựng cluster với `docker-compose.yml`  
  2. Upload dữ liệu CSV lên HDFS  
  3. Xử lý và làm sạch dữ liệu bằng PySpark  
  4. Tính toán, thống kê và phân tích biến động giá  
  5. Trực quan hóa kết quả bằng Matplotlib và Seaborn  
  6. Ghi kết quả xử lý trở lại HDFS  

---

##  3. Cấu trúc thư mục  

```
StockPriceVN/
├── datack/                       ← Dữ liệu CSV gốc (VN30)
├── notebooks/                    ← Notebook Jupyter phân tích
│   └── VN30_Stock_Analysis.ipynb
├── screenshot/                   ← Ảnh minh chứng hệ thống
├── docker-compose.yml            ← Cấu hình Docker cluster
├── README.md                     ← Tệp mô tả này
└── report_Stock_Price_Bigdata.pdf← Báo cáo kết quả dự án
```

---

##  4. Yêu cầu hệ thống  
- **Docker & Docker Compose**  
- **Trình duyệt Web**  
  - HDFS UI: [http://localhost:9870](http://localhost:9870)  
  - Spark Master UI: [http://localhost:8080](http://localhost:8080)  
  - Jupyter Notebook: [http://localhost:8888](http://localhost:8888)  
- **Dữ liệu đầu vào:** các tệp `.csv` trong thư mục `datack/`

---

##  5. Hướng dẫn chạy  

### 🔹 Bước 1: Khởi động cluster
```bash
docker-compose up -d
```

### 🔹 Bước 2: Mở Jupyter Notebook
- Truy cập địa chỉ: `http://localhost:8888`
- Mở notebook `VN30_Stock_Analysis.ipynb`
- Chạy toàn bộ cells theo thứ tự

### 🔹 Bước 3: Kiểm tra kết quả trên HDFS
Truy cập:
```
http://localhost:9870/explorer.html#/user/jovyan/output/vn30_cleaned_final
```

### 🔹 Bước 4: Dừng hệ thống (sau khi hoàn tất)
```bash
docker-compose down
```

---

##  6. Kết quả nổi bật  
- **Dữ liệu đã xử lý** được ghi lại vào HDFS (`/user/jovyan/output/vn30_cleaned_final`)  
- **Các biểu đồ trực quan hóa:**
  - Xu hướng giá đóng cửa của các mã tiêu biểu (VCB, FPT, HPG, MWG, …)
  - Top 10 mã có khối lượng giao dịch cao nhất  
  - Biến động giá trung bình hàng ngày  
  - Xu hướng giá trung bình toàn VN30 theo năm  
  - Ngày có khối lượng giao dịch đột biến nhất  
- **Các bảng thống kê:**
  - Giá trung bình, cao nhất, thấp nhất  
  - Khối lượng giao dịch trung bình  
  - Ngày tăng/giảm mạnh nhất từng mã  

---

##  7. Báo cáo và minh chứng  
- Báo cáo chi tiết: `report_Stock_Price_Bigdata.pdf`  
- Ảnh chụp màn hình:
  - `docker ps` thể hiện toàn bộ container hoạt động  
  - Giao diện HDFS hiển thị dữ liệu và output  
  - Jupyter Notebook với các biểu đồ kết quả  

---

##  8. Liên hệ  
**Học viên:** Hoàng Mạnh Hùng  
**Email:** hungmklc2005@gmail.com  
**MSSV:** 23020371 
**Giảng viên hướng dẫn:** TS. Trần Hồng Việt

---

>  **Ghi chú:**  
> Mọi mã nguồn và hướng dẫn chạy đều được kiểm thử trên môi trường Docker (Spark 3.2.1 + Hadoop 3.2.1 + Python 3.11).  
> Nếu cần hỗ trợ, vui lòng mở *issue* trên repository hoặc liên hệ qua email.
