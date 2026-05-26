<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบเช็คงานด้วยบาร์โค้ด</title>
    <script src="https://unpkg.com/html5-qrcode"></script>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            text-align: center;
            padding: 20px;
            background-color: #f9f9f9;
        }
        h2 {
            color: #333;
        }
        #reader {
            width: 100%;
            max-width: 500px;
            margin: 0 auto;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        #result-container {
            margin-top: 20px;
            padding: 15px;
            background: #e0f7fa;
            border: 1px solid #00acc1;
            border-radius: 8px;
            max-width: 500px;
            margin-left: auto;
            margin-right: auto;
            font-size: 1.2em;
            color: #006064;
        }
    </style>
</head>
<body>

    <h2>📷 ระบบสแกนบาร์โค้ดเช็คงาน</h2>
    
    <div id="reader"></div>

    <div id="result-container">
        <strong>ผลการสแกน: </strong> <span id="result">ยังไม่มีข้อมูล</span>
    </div>

    <script>
        // ฟังก์ชันที่จะทำงานเมื่อสแกนสำเร็จ
        function onScanSuccess(decodedText, decodedResult) {
            // แสดงผลรหัสที่สแกนได้บนหน้าเว็บ
            document.getElementById('result').innerText = decodedText;
            
            // 💡 ตรงนี้คุณสามารถเขียนโค้ดเพื่อส่งข้อมูลไปบันทึกที่ Database หรือ Google Sheets ได้
            // ตัวอย่างเช่น การใช้ fetch API ส่งข้อมูลไปยัง Backend ของคุณ
            /*
            fetch('https://your-api-url.com/check-in', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ barcode: decodedText, timestamp: new Date() })
            }).then(response => {
                alert("เช็คงานสำเร็จ!");
            });
            */
        }

        // ฟังก์ชันที่จะทำงานเมื่อสแกนไม่พบ (มักจะปล่อยว่างไว้เพื่อให้กล้องค้นหาต่อไป)
        function onScanFailure(error) {
            // console.warn(`Code scan error = ${error}`);
        }

        // ตั้งค่าตัวสแกน
        let html5QrcodeScanner = new Html5QrcodeScanner(
            "reader", 
            { 
                fps: 10, // ความเร็วในการสแกน (เฟรมต่อวินาที)
                qrbox: {width: 250, height: 150} // ขนาดของกรอบสแกน (ปรับให้เหมาะกับบาร์โค้ด)
            }, 
            false // verbose ล็อกการทำงานเชิงลึก
        );

        // เริ่มเปิดกล้อง
        html5QrcodeScanner.render(onScanSuccess, onScanFailure);
    </script>

</body>
</html>
