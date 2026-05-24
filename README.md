<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>مولد كروت DATHIUN - الستايل الناري</title>
    <style>
        body { font-family: sans-serif; background: #111; color: white; padding: 20px; }
        .container { max-width: 600px; margin: auto; background: #222; padding: 20px; border-radius: 10px; }
        input, button { width: 100%; padding: 10px; margin: 10px 0; border-radius: 5px; border: none; }
        button { background: #ff4500; color: white; font-weight: bold; cursor: pointer; }
        
        /* الستايل الناري للكارت */
        .fire-card {
            width: 250px;
            padding: 15px;
            background: #000;
            border: 2px solid #ff4500;
            border-radius: 15px;
            box-shadow: 0 0 20px #ff4500, 0 0 40px #ff8c00;
            text-align: center;
            color: #ffcc00;
            margin: 20px auto;
        }
        .fire-card img { width: 100%; border-radius: 10px; }
        .fire-btn { display: block; background: linear-gradient(to right, #ff4500, #ff8c00); color: white; padding: 10px; text-decoration: none; border-radius: 5px; margin-top: 10px; font-weight: bold; }
    </style>
</head>
<body>
    <div class="container">
        <h2>مولد الكروت الناري (DATHIUN)</h2>
        <input type="file" id="imgInput" accept="image/*">
        <input type="text" id="nameInput" placeholder="اسم المنتج">
        <input type="text" id="priceInput" placeholder="السعر">
        <button onclick="generateCard()">توليد الكود</button>
        <div id="output"></div>
    </div>

    <script>
        function generateCard() {
            const file = document.getElementById('imgInput').files[0];
            const name = document.getElementById('nameInput').value;
            const price = document.getElementById('priceInput').value;
            
            const reader = new FileReader();
            reader.onload = function(e) {
                const img = new Image();
                img.onload = function() {
                    const canvas = document.createElement('canvas');
                    canvas.width = 300; 
                    canvas.height = 300;
                    const ctx = canvas.getContext('2d');
                    ctx.drawImage(img, 0, 0, 300, 300);
                    const compressedUrl = canvas.toDataURL('image/jpeg', 0.6); 

                    const cardHtml = `
                    <div class="fire-card">
                        <img src="${compressedUrl}">
                        <h3>${name}</h3>
                        <p>السعر: ${price}</p>
                        <a href="https://wa.me/9647710705445?text=اريد طلب ${name}" class="fire-btn">اطلب واتساب</a>
                    </div>`;
                    
                    document.getElementById('output').innerHTML = cardHtml + '<textarea style="width:100%; height:100px; margin-top:20px;">' + cardHtml + '</textarea>';
                };
                img.src = e.target.result;
            };
            reader.readAsDataURL(file);
        }
    </script>
</body>
</html>
