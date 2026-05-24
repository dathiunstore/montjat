<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <style>
        /* ستايل الأداة الخاص بك */
        .generator-container { background-color: #121212; border: 2px dashed #ff5100; border-radius: 16px; padding: 30px; max-width: 600px; margin: 40px auto; color: #fff; font-family: 'Segoe UI', sans-serif; direction: rtl; box-shadow: 0 10px 30px rgba(0,0,0,0.5); }
        .generator-container h2 { color: #ffaa00; text-align: center; font-size: 1.6rem; }
        .form-group { margin-bottom: 20px; }
        .form-group label { display: block; margin-bottom: 8px; font-weight: bold; }
        .form-group input, .form-group select { width: 100%; padding: 12px; background: #222; border: 1px solid #404040; border-radius: 8px; color: #fff; }
        .gen-btn { width: 100%; background: #ff5100; color: #000; border: none; padding: 15px; font-weight: bold; border-radius: 8px; cursor: pointer; }
        textarea { width: 100%; height: 150px; background: #000; color: #00ffcc; margin-top: 10px; border-radius: 8px; padding: 10px; }
    </style>
</head>
<body>

<div class="generator-container">
    <h2>☣️ لوحة تحكم DATHIUN ☣️</h2>
    
    <div class="form-group">
        <label>اسم المنتج:</label>
        <input type="text" id="prodName">
    </div>
    <div class="form-group">
        <label>السعر:</label>
        <input type="text" id="prodPrice">
    </div>
    <div class="form-group">
        <label>القسم:</label>
        <select id="prodCat">
            <option value="اقنعة">اقنعة</option>
            <option value="اسلحة">اسلحة</option>
            <option value="ستاندات">ستاندات</option>
        </select>
    </div>
    <div class="form-group">
        <label>صورة المنتج:</label>
        <input type="file" id="prodImage" accept="image/*" onchange="previewImage(event)">
    </div>

    <button class="gen-btn" onclick="generateProductCode()">توليد الكود</button>
    <textarea id="resultCode" readonly onclick="this.select()"></textarea>
</div>

<script>
let base64Image = "";

function previewImage(event) {
    const reader = new FileReader();
    reader.onload = function() { base64Image = reader.result; }
    reader.readAsDataURL(event.target.files[0]);
}

function generateProductCode() {
    const name = document.getElementById('prodName').value;
    const price = document.getElementById('prodPrice').value;
    const cat = document.getElementById('prodCat').value;
    
    if(!base64Image) { alert("ارفع الصورة أولاً!"); return; }

    const code = `<div class="product-card" data-category="${cat}">
    <img src="${base64Image}" loading="lazy">
    <h3>${name}</h3>
    <p>${price} د.ع</p>
    <button>اطلب عبر الواتساب</button>
</div>`;

    document.getElementById('resultCode').value = code;
}
</script>
</body>
</html>
