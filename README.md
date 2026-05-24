<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <style>
        .generator-container { background-color: #121212; border: 2px dashed #ff5100; border-radius: 16px; padding: 30px; max-width: 600px; margin: 40px auto; color: #fff; font-family: 'Segoe UI', sans-serif; direction: rtl; box-shadow: 0 10px 30px rgba(0,0,0,0.5); }
        .generator-container h2 { color: #ffaa00; text-align: center; }
        .form-group { margin-bottom: 15px; }
        input, select { width: 100%; padding: 12px; background: #222; border: 1px solid #444; border-radius: 8px; color: #fff; box-sizing: border-box; }
        .gen-btn, .triple-btn { width: 100%; padding: 15px; margin-top: 10px; border-radius: 8px; border: none; font-weight: bold; cursor: pointer; }
        .triple-btn { background: #ff5100; color: #000; }
        .gen-btn { background: #333; color: #fff; border: 1px solid #ff5100; }
        textarea { width: 100%; height: 120px; background: #000; color: #00ffcc; margin-top: 15px; border-radius: 8px; padding: 10px; font-family: monospace; }
    </style>
</head>
<body>

<div class="generator-container">
    <h2>☣️ لوحة تحكم DATHIUN ☣️</h2>
    
    <div class="form-group"><input type="text" id="prodName" placeholder="اسم المنتج"></div>
    <div class="form-group"><input type="text" id="prodPrice" placeholder="السعر"></div>
    <div class="form-group">
        <select id="prodCat">
            <option value="اقنعة">اقنعة</option>
            <option value="اسلحة">اسلحة</option>
            <option value="ميداليات">ميداليات</option>
            <option value="ستاندات">ستاندات</option>
            <option value="مجسمات">مجسمات</option>
            <option value="ستيكرات">ستيكرات</option>
            <option value="اخرى">اخرى</option>
        </select>
    </div>
    <div class="form-group"><input type="file" id="prodImage" onchange="previewImage(event)"></div>

    <button class="triple-btn" onclick="copyQuadCode()">📋 نسخ هيكل 4 كروت (عام)</button>
    <button class="gen-btn" onclick="generateProductCode()">🔥 توليد كرت بـ قسم خاص</button>

    <textarea id="resultCode" readonly onclick="this.select()"></textarea>
</div>

<script>
let base64Image = "";
function previewImage(event) {
    const reader = new FileReader();
    reader.onload = function() { base64Image = reader.result; }
    reader.readAsDataURL(event.target.files[0]);
}

// كرت واحد (يحمل القسم المختار)
function generateProductCode() {
    const cat = document.getElementById('prodCat').value;
    const code = `<div class="product-card" data-category="${cat}"><div class="img-container"><img src="${base64Image}" loading="lazy"></div><div class="product-info"><h3>${document.getElementById('prodName').value}</h3><p class="price">${document.getElementById('prodPrice').value} د.ع</p><a href="#" class="whatsapp-btn">اطلب واتساب 💬</a></div></div>`;
    document.getElementById('resultCode').value = code;
}

// هيكل الـ 4 كروت (عام)
function copyQuadCode() {
    const quadHTML = `
<div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 15px;" class="grid-container">
    <div class="product-card">...كرت 1...</div>
    <div class="product-card">...كرت 2...</div>
    <div class="product-card">...كرت 3...</div>
    <div class="product-card">...كرت 4...</div>
</div>
<style>
@media (max-width: 768px) { .grid-container { grid-template-columns: repeat(2, 1fr) !important; } }
</style>`;
    document.getElementById('resultCode').value = quadHTML;
    alert("تم نسخ هيكل الـ 4 كروت (العام) جاهز للتعبيئة!");
}
</script>
</body>
</html>
