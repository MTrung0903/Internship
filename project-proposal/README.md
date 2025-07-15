# Hướng dẫn triển khai server backend Spring Boot trên AWS với Docker

## 1. Giới thiệu

### Vấn đề

Các doanh nghiệp vừa và nhỏ (SMEs) thường đối mặt với các thách thức khi sử dụng hạ tầng on-premises:

- **Chi phí cao**: Khoảng $50,000/năm cho phần cứng và bảo trì.
- **Thời gian triển khai lâu**: Mất khoảng 20 giờ để triển khai một ứng dụng mới.
- **Khó mở rộng**: Hạ tầng on-premises thiếu linh hoạt khi nhu cầu tăng.
- **Rủi ro bảo mật**: Khó đảm bảo các tiêu chuẩn bảo mật hiện đại.

### Giải pháp

Triển khai ứng dụng Spring Boot trên AWS sử dụng:

- **Amazon EC2**: Chạy container và Nginx làm reverse proxy.
- **Amazon RDS**: Cơ sở dữ liệu MySQL với Multi-AZ cho độ tin cậy 99.9%.
- **Docker và Docker Compose**: Quản lý container.
- **Docker Hub**: Lưu trữ Docker image thay vì Amazon ECR.
- **Nginx**: Chuyển tiếp yêu cầu HTTP từ cổng 80 đến ứng dụng Spring Boot.

### Lợi ích

- **Tiết kiệm chi phí**: Giảm 64% chi phí (từ $50K/năm xuống $18K/năm).
- **Tăng tốc triển khai**: Giảm thời gian triển khai 80% (từ 20 giờ xuống 4 giờ).
- **Bảo mật và độ tin cậy**: Đáp ứng các tiêu chuẩn bảo mật và đảm bảo uptime cao.
- **Khả năng mở rộng**: Dễ dàng chuyển sang ECS/EKS trong tương lai.

### Chi phí

| Thành phần | Chi phí hàng tháng (ước tính) |
| --- | --- |
| EC2 (t3.medium) | \~$16.37 |
| RDS (db.t3.micro) | \~$18.25 |
| Lưu trữ EBS, khác | \~$7.38 |
| **Tổng cộng** | \~$42 |

- **Chi phí phát triển một lần**: $2,000.
- **Thời gian hoàn vốn (ROI)**: 4 tháng.

### Kết quả mong đợi

- Thời gian phản hồi API dưới 200ms.
- Xử lý 1,000 yêu cầu đồng thời.
- Hệ thống ổn định, dễ bảo trì và sẵn sàng mở rộng.

## 2. Chuẩn bị ứng dụng

Trước khi triển khai trên AWS, bạn cần chuẩn bị ứng dụng bằng cách clone mã nguồn từ GitHub, xây dựng Docker image, và đẩy lên Docker Hub.

### 2.1. Clone project từ GitHub

- **Yêu cầu**: Cài đặt Git trên máy tính (Hướng dẫn cài Git).
- **Thực hiện**:

  ```bash
  git clone [invalid url, do not cite]
  cd <repo_name>
  ```

  Thay `<username>/<repo_name>` bằng URL thực tế của repository trên GitHub.

### 2.2. Xây dựng Docker image

- **Yêu cầu**: Cài đặt Docker Desktop hoặc Docker CLI (Hướng dẫn cài Docker).
- **Thực hiện**:
  - Đảm bảo có file `Dockerfile` trong thư mục gốc của project. Ví dụ:

    ```dockerfile
    FROM openjdk:17-jdk-slim
    WORKDIR /app
    COPY target/*.jar app.jar
    ENTRYPOINT ["java", "-jar", "app.jar"]
    ```
  - Xây dựng image:

    ```bash
    docker build -t my spring-boot-app .
    ```

### 2.3. Đẩy Docker image lên Docker Hub

- **Yêu cầu**: Có tài khoản Docker Hub (Đăng ký tại).
- **Thực hiện**:
  - Đăng nhập vào Docker Hub:

    ```bash
    docker login
    ```
  - Gắn thẻ image:

    ```bash
    docker tag my spring-boot-app <dockerhub_username>/my spring-boot-app:latest
    ```
  - Đẩy image lên Docker Hub:

    ```bash
    docker push <dockerhub_username>/my spring-boot-app:latest
    ```
- **Lưu ý**: Giả định repository trên Docker Hub là public. Nếu private, cần cấu hình xác thực trên EC2 (xem mục 4.2).

## 3. Triển khai hạ tầng AWS

### 3.1. Chuẩn bị hạ tầng (Ngày 1)

- **Tạo VPC**:
  - Tạo Virtual Private Cloud với ít nhất 2 subnet public và 2 subnet private (Hướng dẫn VPC).
- **Cấu hình Security Groups**:
  - `ec2-sg`: Cho phép inbound traffic trên cổng 80 (HTTP) từ 0.0.0.0/0, cổng 22 (SSH) từ IP cụ thể.
  - `rds-sg`: Chỉ cho phép kết nối từ `ec2-sg` trên cổng 3306 (MySQL).
- **Tạo IAM Role**:
  - Tạo role `CustomRWECRRole` với quyền tối thiểu cho EC2 và RDS (Hướng dẫn IAM).
- **Tạo DB Subnet Group**:
  - Đặt RDS trong subnet private (Hướng dẫn DB Subnet Group).

### 3.2. Cung cấp EC2 và RDS (Ngày 3)

- **EC2 Instance**:
  - Type: `t3.medium`.
  - OS: Ubuntu 24.04.
  - Đặt trong subnet public với truy cập internet.
  - Gắn IAM Role `CustomRWECRRole`.
- **RDS Instance**:
  - Type: `db.t3.micro`.
  - Engine: MySQL.
  - Lưu trữ: 20 GB General Purpose SSD.
  - Multi-AZ: Enabled.
  - Database: `first_cloud_users`.
  - Lưu credentials trong AWS Secrets Manager (Hướng dẫn Secrets Manager).

## 4. Triển khai ứng dụng trên AWS

### 4.1. Cấu hình EC2 (Ngày 4)

- **Cài đặt phần mềm**:

  ```bash
  sudo apt update
  sudo apt install docker.io nginx mysql-client -y
  sudo usermod -aG docker ubuntu
  ```
- **Cấu hình Nginx**:
  - Tạo file `nginx.conf`:

    ```nginx
    server {
        listen 80;
        server_name # Your public IP
        location / {
            proxy_pass http://localhost:8080; # Your Spring Boot application URL
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;
        }
    }
    ```
  - Copy và khởi động Nginx:

    ```bash
    sudo cp nginx.conf /etc/nginx/nginx.conf
    sudo systemctl restart nginx
    ```

### 4.2. Kéo Docker image và chạy ứng dụng

- **T。上 Docker Hub**:

  - Tạo file `docker-compose.yml`:

    ```yaml
    version: '3'
    services:
      nginx:
        image: nginx:latest
        ports:
          - "80:80"
        volumes:
          - ./nginx.conf:/etc/nginx/nginx.conf
        depends_on:
          - spring-boot-app
      spring-boot-app:
        image: <dockerhub_username>/my spring-boot-app:latest
        ports:
          - "8080:8080"
        environment:
          - SPRING_DATASOURCE_URL=jdbc:mysql://<rds_endpoint>:3306/first_cloud_usersទ
          - SPRING_DATASOURCE_USERNAME=<db_username>
          - SPRING_DATASOURCE_PASSWORD=<db_password>
    ```
  - Thay `<dockerhub_username>` và các thông tin RDS.
  - Chạy ứng交叉

  ```bash
  docker compose up -d
  ```

- **Lưu ý về repository private**:

  - Nếu repository là private, cần chạy `docker login` trên EC2 và cung cấp credentials.

### 4.3. Kiểm tra và tối ưu (Ngày 5)

- **Kiểm tra API**:
  - Truy cập \`\[invalid url, do not cite\]
  - Đảm bảo phản hồi API &lt; 200ms và xử lý 1,000 yêu cầu đồng thời.
- **Kiểm tra tích hợp**:
  - Sử dụng Testcontainers để kiểm tra kết nối RDS (Hướng dẫn Testcontainers).
- **Kiểm tra hiệu suất**:
  - Sử dụng JMeter để kiểm tra hiệu suất (\[Hướng dẫn JMeter\](https://jmeter.apache.org/ Juno)).
- **Giám sát**:
  - Thiết lập CloudWatch để giám sát logs và thiết lập cảnh báo (Hướng dẫn CloudWatch).
- **Tối ưu hóa**:
  - Kiểm tra và điều chỉnh cấu hình nếu cần.

## 5. Bảo trì và các thực hành tốt nhất

### 5.1. Backup và khôi phục

- Thiết lập backup tự động cho RDS (Hướng dẫn RDS Backup).
- \*\*Lưu ýწ
- **Giám sát**:
  - Sử dụng CloudWatch để giám sát logs và thiết lập cảnh báo.
- **Cập nhật**:
  - Cập nhật image mới, chạy:

    ```bash
    docker compose pull
    docker compose up -d
    ```

### 5.2. Bảo mật

- **Mã hóa dữ liệu**:
  - Sử dụng EBS encryption cho EBS volumes (Hướng dẫn EBS Encryption).
- **Sử dụng Secrets Manager**:
  - Lưu trữ credentials trong Secrets Manager (Hướng dẫn Secrets Manager).
- **Cập nhật ứng dụng**:
  - Đẩy image mới lên Docker Hub và chạy lệnh trên.

