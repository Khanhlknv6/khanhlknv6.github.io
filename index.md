<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Công Cụ Tính Chỉ Số BMI</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            background-color: #f4f4f9;
        }

        .container {
            background-color: #fff;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 400px;
            text-align: center;
        }

        h1 {
            color: #333;
            margin-bottom: 25px;
            font-size: 1.8em;
        }

        .input-group {
            margin-bottom: 15px;
            text-align: left;
        }

        .input-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
            color: #555;
        }

        .input-group input {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 6px;
            box-sizing: border-box;
            font-size: 1em;
        }

        button {
            background-color: #007bff;
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 1.1em;
            width: 100%;
            margin-top: 10px;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #0056b3;
        }

        #result {
            margin-top: 25px;
            padding: 15px;
            border-radius: 8px;
            background-color: #e9ecef;
            min-height: 60px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            font-size: 1.1em;
        }

        #bmi-value {
            font-size: 1.8em;
            font-weight: bold;
            color: #28a745; /* Màu mặc định cho BMI */
            margin-bottom: 5px;
        }

        #bmi-status {
            font-weight: bold;
            color: #333;
        }
        
        .note {
            margin-top: 20px;
            font-size: 0.9em;
            color: #6c757d;
            border-top: 1px dashed #ccc;
            padding-top: 15px;
            text-align: left;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Công Cụ Tính BMI</h1>
        
        <div class="input-group">
            <label for="weight">Cân nặng (kg):</label>
            <input type="number" id="weight" min="1" step="0.1" placeholder="Ví dụ: 65.5">
        </div>

        <div class="input-group">
            <label for="height">Chiều cao (cm):</label>
            <input type="number" id="height" min="10" step="1" placeholder="Ví dụ: 170">
        </div>

        <button onclick="calculateBMI()">Tính BMI</button>

        <div id="result">
            <p>Nhập cân nặng và chiều cao để bắt đầu.</p>
        </div>

        <div class="note">
            <h3>Phân loại BMI (WHO):</h3>
            <ul>
                <li>Dưới 18.5: Gầy</li>
                <li>18.5 – 24.9: Bình thường</li>
                <li>25.0 – 29.9: Tiền béo phì/Thừa cân</li>
                <li>30.0 – 34.9: Béo phì độ I</li>
                <li>35.0 – 39.9: Béo phì độ II</li>
                <li>Trên 40.0: Béo phì độ III</li>
            </ul>
        </div>
    </div>

    <script>
        function calculateBMI() {
            // 1. Lấy giá trị từ các trường nhập liệu
            const weightInput = document.getElementById('weight').value;
            const heightInput = document.getElementById('height').value;
            const resultDiv = document.getElementById('result');

            // 2. Chuyển đổi sang số và kiểm tra giá trị hợp lệ
            const weight = parseFloat(weightInput);
            const heightCm = parseFloat(heightInput);

            if (isNaN(weight) || isNaN(heightCm) || weight <= 0 || heightCm <= 0) {
                resultDiv.innerHTML = '<p style="color: red; font-weight: bold;">Vui lòng nhập giá trị cân nặng và chiều cao hợp lệ.</p>';
                return;
            }

            // 3. Chuyển đổi chiều cao từ cm sang mét
            const heightM = heightCm / 100;

            // 4. Tính toán BMI: BMI = cân nặng (kg) / [chiều cao (m) * chiều cao (m)]
            const bmi = weight / (heightM * heightM);
            const roundedBmi = bmi.toFixed(2); // Làm tròn đến 2 chữ số thập phân

            // 5. Xác định tình trạng cơ thể và màu sắc tương ứng
            let status = '';
            let color = '';

            if (bmi < 18.5) {
                status = 'Gầy';
                color = '#ffc107'; // Vàng
            } else if (bmi >= 18.5 && bmi <= 24.9) {
                status = 'Bình thường';
                color = '#28a745'; // Xanh lá
            } else if (bmi >= 25.0 && bmi <= 29.9) {
                status = 'Tiền béo phì/Thừa cân';
                color = '#fd7e14'; // Cam
            } else { // bmi >= 30.0
                status = 'Béo phì';
                color = '#dc3545'; // Đỏ
            }

            // 6. Hiển thị kết quả
            resultDiv.innerHTML = `
                <p>Chỉ số BMI của bạn là:</p>
                <p id="bmi-value" style="color: ${color};">${roundedBmi}</p>
                <p id="bmi-status">Tình trạng: <strong>${status}</strong></p>
            `;
        }
    </script>
</body>
</html>
