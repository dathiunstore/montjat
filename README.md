<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>مولد DATHIUN الاحترافي</title>
    <style>
        body { font-family: sans-serif; background: #111; color: white; padding: 20px; }
        .container { max-width: 600px; margin: auto; background: #222; padding: 20px; border-radius: 10px; }
        input, select, button { width: 100%; padding: 12px; margin: 10px 0; border-radius: 5px; border: none; }
        button { background: #ff4500; color: white; font-weight: bold; cursor: pointer; }
        #copyBtn, #copyStyleBtn { display: block; margin-top: 10px; }
        #copyStyleBtn { background: #4a90e2; }
    </style>
</head>
<body>
    <div class="container">
        <h2>مولد DATHIUN</h2>
        <button id="copyStyleBtn" onclick="copyStyle()">🎨 نسخ كود الستايل (CSS المتوافق)</button>
        <hr style="border:0; border-top:1px solid #444; margin:20px 0;">

        <input type="file" id="imgInput" accept="image/*">
        <input type="text" id="nameInput" placeholder="اسم المنتج">
        <input type="text" id="priceInput" placeholder="السعر">
        <select id="categoryInput">
            <option value="figures">مجسمات</option>
            <option value="stands">ستاندات</option>
            <option value="weapons">أسلحة</option>
            <option value="keycaps">كيكابس</option>
            <option value="masks">أقنعة</option>
            <option value="keychains">ميداليات</option>
            <option value="stickers">ستيكرات</option>
            <option value="others">أخرى</option>
        </select>
        <button onclick="generateCard()">توليد الكود</button>
        
        <textarea id="output" rows="5" style="width:100%; margin-top:10px; background:#000; color:#0f0; border:none; padding:10px; display:none;"></textarea>
        <button id="copyBtn" style="display:none;" onclick="copyCode()">📋 نسخ كود الكارت</button>
    </div>

    <script>
        // هذا هو الستايل المحدث والمتوافق مع الجوال
        const styleCode = `<style>
    .filter-menu { text-align: center; margin-bottom: 40px; }
    .btn-all { font-size: 22px; font-weight: bold; color: #fff; background: linear-gradient(to right, #ff4500, #ff8c00); border: none; padding: 12px 40px; cursor: pointer; border-radius: 50px; box-shadow: 0 0 10px #ff4500; transition: 0.3s; }
    .category-btns { display: flex; justify-content: center; flex-wrap: wrap; gap: 12px; margin-top: 15px; }
    .category-btns button { background: #222; color: #ffcc00; border: 2px solid #ff4500; padding: 10px 20px; cursor: pointer; border-radius: 30px; font-weight: bold; transition: 0.3s; }
    .category-btns button:hover { background: #ff4500; color: #fff; box-shadow: 0 0 10px #ff4500; }
    .product-gallery { display: flex; flex-wrap: wrap; justify-content: center; gap: 15px; padding: 10px; }
    .fire-card { width: calc(50% - 15px); max-width: 250px; padding: 10px; background: #000; border: 2px solid #ff4500; border-radius: 15px; box-shadow: 0 0 10px rgba(255, 69, 0, 0.3); text-align: center; color: #ffcc00; transition: transform 0.4s ease, box-shadow 0.4s ease; box-sizing: border-box; }
    .fire-card:hover { transform: scale(1.03); box-shadow: 0 0 25px rgba(255, 69, 0, 0.7); }
    .fire-card img { width: 100%; height: 150px; object-fit: cover; border-radius: 10px; }
    .fire-card h3 { color: #ffffff; margin: 8px 0; font-size: 16px; }
    .fire-card p { font-size: 15px; color: #ffcc00; font-weight: bold; margin-bottom: 8px; }
    .fire-btn { display: block; background: linear-gradient(to right, #ff4500, #ff8c00); color: #000000 !important; padding: 8px; text-decoration: none; border-radius: 5px; margin-top: 5px; font-weight: bold; font-size: 13px; }
</style>`;

        function copyStyle() {
            navigator.clipboard.writeText(styleCode).then(() => alert("تم نسخ كود الستايل!"));
        }

        function convertToEnglishNumbers(str) {
            const arabicNumbers = ['٠', '١', '٢', '٣', '٤', '٥', '٦', '٧', '٨', '٩'];
            const englishNumbers = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'];
            let result = str;
            for (let i = 0; i < 10; i++) result = result.replace(new RegExp(arabicNumbers[i], 'g'), englishNumbers[i]);
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
                    ctx.drawImage(img, 0, 0, img.width, img.height, 0, 0, 300, 300);
                    const compressedUrl = canvas.toDataURL('image/jpeg', 0.6); 

                    const fullHtml = `<div class="fire-card" data-category="${cat}">
    <img src="${compressedUrl}" loading="lazy">
    <h3>${name}</h3>
    <p>${price} د.ع</p>
    <a href="https://wa.me/9647710705445?text=اريد طلب ${name} بسعر ${price} د.ع" class="fire-btn">💬 اطلبه الآن من الواتساب</a>
</div>`;
                    
                    document.getElementById('output').style.display = 'block';
                    document.getElementById('output').value = fullHtml;
                    document.getElementById('copyBtn').style.display = 'block';
                };
                img.src = e.target.result;
            };
            reader.readAsDataURL(file);
        }

        function copyCode() {
            document.getElementById('output').select();
            document.execCommand('copy');
            alert("تم نسخ كود الكارت!");
        }
    </script>
</body>
</html>
