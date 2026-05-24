<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <style>
        .generator-container { background-color: #121212; border: 2px dashed #ff5100; border-radius: 16px; padding: 30px; max-width: 600px; margin: 40px auto; color: #fff; font-family: 'Segoe UI', sans-serif; direction: rtl; box-shadow: 0 10px 30px rgba(0,0,0,0.5); }
        .generator-container h2 { color: #ffaa00; text-align: center; }
        .form-group { margin-bottom: 15px; }
        input, select { width: 100%; padding: 12px; background: #222; border: 1px solid #444; border-radius: 8px; color: #fff; }
        .gen-btn, .triple-btn { width: 100%; padding: 15px; margin-top: 10px; border-radius: 8px; border: none; font-weight: bold; cursor: pointer; }
        .triple-btn { background: #ff5100; color: #000; }
        .gen-btn { background: #333; color: #fff; border: 1px solid #ff5100; }
        textarea { width: 100%; height: 120px; background: #000; color: #00ffcc; margin-top: 15px; border-radius: 8px; padding: 10px; }
    </style>
</head>
<body>

<div class="generator-container">
    <h2>☣️ لوحة تحكم DATHIUN ☣️</h2>
    
    <input type="text" id="prodName" placeholder="اسم المنتج">
    <input type="text" id="prodPrice" placeholder="السعر">
    <select id="prodCat">
        <option value="اقنعة">اقنعة</option>
        <option value="اسلحة">اسلحة</option>
        <option value="ستاندات">ستاندات</option>
        <option value="مجسمات">مجسمات</option>
        <option value="ستيكرات">ستيكرات</option>
        <option value="اخرى">اخرى</option>
    </select>
    <input type="file" id="prodImage" onchange="previewImage(event)">

    <button class="triple-btn" onclick="copyQuadCode()">📋 نسخ كود 4 كروت (متوافق موبايل)</button>
    <button class="gen-btn" onclick="generateProductCode()">🔥 توليد كرت واحد</button>

    <textarea id="resultCode" readonly onclick="this.select()"></textarea>
</div>

<script>
let base64Image = "";
function previewImage(event) {
    const reader = new FileReader();
    reader.onload = function() { base64Image = reader.result; }
    reader.readAsDataURL(event.target.files[0]);
}

// كرت واحد
function generateProductCode() {
    const cat = document.getElementById('prodCat').value;
    const code = `<div class="product-card" data-category="${cat}"><img src="${base64Image}" loading="lazy"><h3>${document.getElementById('prodName').value}</h3><p>${document.getElementById('prodPrice').value} د.ع</p><button>اطلب واتساب</button></div>`;
    document.getElementById('resultCode').value = code;
}

// 4 كروت (مع التنسيق الذي يحولها 2x2 في الموبايل)
function copyQuadCode() {
    const cat = document.getElementById('prodCat').value;
    const quadHTML = `
<div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 15px;" class="grid-container">
    <div class="product-card" data-category="${cat}">...كرت 1...</div>
    <div class="product-card" data-category="${cat}">...كرت 2...</div>
    <div class="product-card" data-category="${cat}">...كرت 3...</div>
    <div class="product-card" data-category="${cat}">...كرت 4...</div>
</div>
<style>
@media (max-width: 768px) { .grid-container { grid-template-columns: repeat(2, 1fr) !important; } }
</style>`;
    document.getElementById('resultCode').value = quadHTML;
    alert("تم تجهيز كود الـ 4 كروت بنجاح!");
}
</script>
</body>
</html>
