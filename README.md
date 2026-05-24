<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>أداة DATHIUN النهائية</title>
    <style>
        /* ستايل الأداة نفسها */
        body { font-family: sans-serif; background: #111; color: white; padding: 20px; }
        .container { max-width: 600px; margin: auto; background: #222; padding: 20px; border-radius: 10px; }
        input, select, button { width: 100%; padding: 12px; margin: 10px 0; border-radius: 5px; border: none; }
        button { background: #ff4500; color: white; font-weight: bold; cursor: pointer; }
        textarea { width: 100%; height: 300px; background: #000; color: #0f0; border: none; padding: 10px; margin-top: 10px; font-family: monospace; }
    </style>
</head>
<body>
    <div class="container">
        <h2>مولد كروت DATHIUN الشامل</h2>
        <input type="file" id="imgInput" accept="image/*">
        <input type="text" id="nameInput" placeholder="اسم المنتج">
        <input type="text" id="priceInput" placeholder="السعر">
        <select id="categoryInput">
            <option value="figures">مجسمات</option>
            <option value="weapons">أسلحة</option>
            <option value="masks">أقنعة</option>
            <option value="others">أخرى</option>
        </select>
        <button onclick="generateFullCode()">توليد كود المعرض الكامل (ستايل + كرت)</button>
        <textarea id="output" readonly></textarea>
        <button onclick="copyToClipboard()">📋 نسخ الكود كاملاً</button>
    </div>

    <script>
        function generateFullCode() {
            const file = document.getElementById('imgInput').files[0];
            const name = document.getElementById('nameInput').value || "منتج";
            const price = document.getElementById('priceInput').value || "0";
            const cat = document.getElementById('categoryInput').value;

            const reader = new FileReader();
            reader.onload = function(e) {
                const fullCode = `<style>
    .product-gallery { display: flex; flex-wrap: wrap; justify-content: flex-start; gap: 5px; padding: 5px; }
    .fire-card { width: calc(25% - 5px); padding: 5px; background: #000; border: 1px solid #ff4500; border-radius: 5px; text-align: center; color: #ffcc00; box-sizing: border-box; }
    .fire-card img { width: 100%; aspect-ratio: 1/1; object-fit: cover; border-radius: 3px; }
    .fire-card h3 { color: #ffffff; margin: 5px 0; font-size: 12px; }
    .fire-card p { font-size: 11px; font-weight: bold; margin-bottom: 5px; }
    .fire-btn { display: block; background: #ff4500; color: #fff !important; padding: 4px; text-decoration: none; border-radius: 3px; font-size: 10px; font-weight: bold; }
</style>

<div class="product-gallery" id="productGrid">
    <div class="fire-card" data-category="${cat}">
        <img src="${e.target.result}" loading="lazy">
        <h3>${name}</h3>
        <p>${price} د.ع</p>
        <a href="#" class="fire-btn">اطلبه الآن</a>
    </div>
</div>`;
                document.getElementById('output').value = fullCode;
            };
            if(file) reader.readAsDataURL(file);
            else alert("يرجى اختيار صورة!");
        }

        function copyToClipboard() {
            const textarea = document.getElementById('output');
            textarea.select();
            document.execCommand('copy');
            alert("تم النسخ!");
        }
    </script>
</body>
</html>
