<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>مولد كروت DATHIUN الاحترافي</title>
    <style>
        body { font-family: sans-serif; background: #111; color: white; padding: 20px; }
        .container { max-width: 600px; margin: auto; background: #222; padding: 20px; border-radius: 10px; }
        input, select, button { width: 100%; padding: 12px; margin: 10px 0; border-radius: 5px; border: none; }
        button { background: #ff4500; color: white; font-weight: bold; cursor: pointer; }
        #copyBtn { background: #25d366; display: none; margin-top: 10px; }
        
        /* تنسيق الكارت */
        .fire-card { width: 250px; padding: 15px; background: #000; border: 2px solid #ff4500; border-radius: 15px; box-shadow: 0 0 20px #ff4500, 0 0 40px #ff8c00; text-align: center; color: #ffcc00; margin: 20px auto; }
        .fire-card img { width: 100%; height: 250px; object-fit: cover; border-radius: 10px; }
        .fire-card h3 { color: #ffffff; margin: 10px 0; font-size: 20px; } /* الاسم أبيض */
        .fire-card p { font-size: 16px; color: #fff; margin-bottom: 10px; }
        .fire-btn { display: block; background: linear-gradient(to right, #ff4500, #ff8c00); color: #000000 !important; padding: 10px; text-decoration: none; border-radius: 5px; margin-top: 10px; font-weight: bold; }
    </style>
</head>
<body>
    <div class="container">
        <h2>مولد كروت DATHIUN</h2>
        <input type="file" id="imgInput" accept="image/*">
        <input type="text" id="nameInput" placeholder="اسم المنتج">
        <input type="text" id="priceInput" placeholder="السعر">
        <select id="categoryInput">
            <option value="figures">مجسمات</option>
            <option value="stands">ستاندات</option>
            <option value="weapons">أسلحة</option>
            <option value="masks">أقنعة</option>
            <option value="keychains">ميداليات</option>
            <option value="stickers">ستيكرات</option>
            <option value="others">أخرى</option>
        </select>
        <button onclick="generateCard()">توليد الكود</button>
        
        <div id="output"></div>
        <button id="copyBtn" onclick="copyCode()">📋 نسخ الكود</button>
    </div>

    <script>
        function convertToEnglishNumbers(str) {
            const arabicNumbers = ['٠', '١', '٢', '٣', '٤', '٥', '٦', '٧', '٨', '٩'];
            const englishNumbers = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'];
            let result = str;
            for (let i = 0; i < 10; i++) {
                result = result.replace(new RegExp(arabicNumbers[i], 'g'), englishNumbers[i]);
            }
            return result;
        }

        function generateCard() {
            const file = document.getElementById('imgInput').files[0];
            const name = document.getElementById('nameInput').value;
            const price = convertToEnglishNumbers(document.getElementById('priceInput').value);
            const cat = document.getElementById('categoryInput').value;
            
            if(!file) { alert("يرجى اختيار صورة!"); return; }

            const reader = new FileReader();
            reader.onload = function(e) {
                const img = new Image();
                img.onload = function() {
                    const canvas = document.createElement('canvas');
                    canvas.width = 300; canvas.height = 300;
                    const ctx = canvas.getContext('2d');
                    const size = Math.min(img.width, img.height);
                    ctx.drawImage(img, (img.width-size)/2, (img.height-size)/2, size, size, 0, 0, 300, 300);
                    const compressedUrl = canvas.toDataURL('image/jpeg', 0.6); 

                    const fullHtml = `<style>
                        .fire-card { width: 250px; padding: 15px; background: #000; border: 2px solid #ff4500; border-radius: 15px; box-shadow: 0 0 20px #ff4500, 0 0 40px #ff8c00; text-align: center; color: #ffcc00; margin: 20px auto; }
                        .fire-card img { width: 100%; height: 250px; object-fit: cover; border-radius: 10px; }
                        .fire-card h3 { color: #ffffff; margin: 10px 0; font-size: 20px; }
                        .fire-card p { font-size: 16px; color: #fff; margin-bottom: 10px; }
                        .fire-btn { display: block; background: linear-gradient(to right, #ff4500, #ff8c00); color: #000000 !important; padding: 10px; text-decoration: none; border-radius: 5px; margin-top: 10px; font-weight: bold; }
                    </style>
                    <div class="fire-card" data-category="${cat}">
                        <img src="${compressedUrl}">
                        <h3>${name}</h3>
                        <p>السعر: ${price} د.ع</p>
                        <a href="https://wa.me/9647710705445?text=اريد طلب ${name} بسعر ${price} د.ع" class="fire-btn">💬 اطلبه الآن من الواتساب</a>
                    </div>`;
                    
                    document.getElementById('output').innerHTML = fullHtml;
                    document.getElementById('copyBtn').style.display = 'block';
                    window.currentHtml = fullHtml;
                };
                img.src = e.target.result;
            };
            reader.readAsDataURL(file);
        }

        function copyCode() {
            navigator.clipboard.writeText(window.currentHtml).then(() => {
                alert("تم نسخ الكود! اذهب للموقع وألصقه داخل بلوك HTML.");
            });
        }
    </script>
</body>
</html>
