<div class="generator-container">
    <h2>☣️ لوحة تحكم DATHIUN لتوليد كروت المنتجات ☣️</h2>
    <p style="text-align: center; color: #888;">ادخل البيانات هنا، وانسخ الكود الناتج وضعه في أودو فوراً</p>
    
    <div class="form-group">
        <label>1. اسم المجسم أو الستاند:</label>
        <input type="text" id="prodName" placeholder="مثال: ستاند ريزدنت إيفل مخصص">
    </div>
    
    <div class="form-group">
        <label>2. السعر (بالدينار العراقي):</label>
        <input type="text" id="prodPrice" placeholder="مثال: 25,000 د.ع">
    </div>
    
    <div class="form-group">
        <label>3. ارفع صورة المجسم من جهازك:</label>
        <input type="file" id="prodImage" accept="image/*" onchange="previewImage(event)">
        <div class="img-preview-box">
            <img id="preview" src="#" alt="معاينة الصورة ستظهر هنا" style="display:none; max-width:100%; max-height:200px; border-radius:8px; margin-top:10px;">
        </div>
    </div>

    <button class="gen-btn" onclick="generateProductCode()">🔥 توليد الكود الناري</button>

    <div class="output-section" id="outputArea" style="display: none;">
        <h3>📋 انسخ هذا الكود وضعه في بلوك أودو:</h3>
        <textarea id="resultCode" readonly onclick="this.select()"></textarea>
        <button class="copy-btn" onclick="copyTheCode()">اضغط هنا لنسخ الكود بلمحة بصر 📑</button>
    </div>
</div>

<script>
let base64Image = "";

// تحويل الصورة المرفوعة من الـ PC إلى Base64 حتى تشتغل بداخل الكود مباشرة بدون روابط!
function previewImage(event) {
    const reader = new FileReader();
    reader.onload = function() {
        const output = document.getElementById('preview');
        output.src = reader.result;
        output.style.display = 'block';
        base64Image = reader.result; // خزن الصورة ككود
    }
    reader.readAsDataURL(event.target.files[0]);
}

// دالة توليد كود الكارت الفخم بالملي
function generateProductCode() {
    const name = document.getElementById('prodName').value || "مجسم مخصص هيبة";
    const price = document.getElementById('prodPrice').value || "السعر حسب الطلب";
    
    if(!base64Image) {
        alert("يا وحش ارفع صورة المجسم أولاً حتى يكتمل السحر!");
        return;
    }

    // هنا نقوم بصناعة كود الـ HTML والـ CSS المظلم تلقائياً بالبيانات الجديدة
    const generatedHTML = `<div class="product-card" style="background: #141414; border: 1px solid #252525; border-radius: 16px; width: 320px; overflow: hidden; box-shadow: 0 15px 35px rgba(0,0,0,0.7); transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275); font-family: 'Segoe UI', sans-serif; direction: rtl; margin: 15px;">
    <div class="img-container" style="width: 100%; height: 280px; overflow: hidden; background: #000;">
        <img src="${base64Image}" style="width: 100%; height: 100%; object-fit: cover;" alt="Product">
    </div>
    <div class="product-info" style="padding: 25px; text-align: center; color: #fff;">
        <h3 style="margin: 0 0 12px 0; font-size: 1.4rem; font-weight: 700;">${name}</h3>
        <p class="price" style="color: #ffaa00; font-weight: bold; font-size: 1.3rem; margin-bottom: 22px;">${price}</p>
        <a href="https://wa.me/9647710705445?text=مرحبا_داثيون_ستور_اريد_اطلب_${encodeURIComponent(name)}" target="_blank" style="display: block; background: linear-gradient(45deg, #ff5100, #ffaa00); color: #000000 !important; text-decoration: none !important; padding: 14px; border-radius: 10px; font-weight: bold; font-size: 1rem; box-shadow: 0 4px 15px rgba(255, 81, 0, 0.2);">اطلب عبر الواتساب السريع 💬</a>
    </div>
</div>`;

    document.getElementById('resultCode').value = generatedHTML;
    document.getElementById('outputArea').style.display = 'block';
}

function copyTheCode() {
    const copyText = document.getElementById("resultCode");
    copyText.select();
    document.execCommand("copy");
    alert("تم نسخ الكود بنجاح يا وحش! اذهب الآن لـ أودو وبسوي لصق (Paste) في بلوك الـ Embed.");
}
</script>

<style>
.generator-container {
    background-color: #121212;
    border: 2px dashed #ff5100;
    border-radius: 16px;
    padding: 30px;
    max-width: 600px;
    margin: 40px auto;
    color: #fff;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    direction: rtl;
    box-shadow: 0 10px 30px rgba(0,0,0,0.5);
}
.generator-container h2 {
    color: #ffaa00;
    text-align: center;
    font-size: 1.6rem;
    margin-bottom: 20px;
}
.form-group {
    margin-bottom: 20px;
}
.form-group label {
    display: block;
    margin-bottom: 8px;
    font-weight: bold;
    color: #ddd;
}
.form-group input[type="text"] {
    width: 100%;
    padding: 12px;
    background: #222;
    border: 1px solid #404040;
    border-radius: 8px;
    color: #fff;
    font-size: 1rem;
}
.form-group input[type="file"] {
    background: #222;
    padding: 10px;
    border-radius: 8px;
    width: 100%;
    border: 1px solid #404040;
    color: #ccc;
}
.gen-btn {
    width: 100%;
    background: linear-gradient(45deg, #ff5100, #ffaa00);
    color: #000;
    border: none;
    padding: 15px;
    font-size: 1.1rem;
    font-weight: bold;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.3s ease;
}
.gen-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 5px 20px rgba(255, 81, 0, 0.4);
}
.output-section {
    margin-top: 30px;
    background: #050505;
    padding: 20px;
    border-radius: 10px;
    border: 1px solid #333;
}
.output-section textarea {
    width: 100%;
    height: 150px;
    background: #111;
    color: #00ffcc;
    border: 1px solid #444;
    border-radius: 8px;
    padding: 10px;
    font-family: monospace;
    font-size: 0.9rem;
    resize: none;
    margin-top: 10px;
}
.copy-btn {
    width: 100%;
    background: #00ffcc;
    color: #000;
    border: none;
    padding: 12px;
    font-weight: bold;
    border-radius: 6px;
    margin-top: 10px;
    cursor: pointer;
}
</style>
