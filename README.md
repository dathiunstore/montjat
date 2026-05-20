<div class="generator-container">
    <h2>☣️ لوحة تحكم DATHIUN لتوليد كروت المنتجات ☣️</h2>
    <p style="text-align: center; color: #888; margin-bottom: 25px;">ادخل البيانات لتوليد كارت مخصص، أو انسخ النظام الثلاثي الجاهز فوراً</p>
    
    <div class="quick-actions">
        <button class="triple-btn" onclick="copyTripleCode()">📋 نسخ كود الـ 3 كروت الجاهزة (كارتين بالموبايل)</button>
    </div>
    
    <hr style="border: 0; border-top: 1px solid #333; margin: 25px 0;">

    <div class="form-group">
        <label>1. اسم المجسم أو الستاند:</label>
        <input type="text" id="prodName" placeholder="مثال: ستاند ريزدنت إيفل مخصص">
    </div>
    
    <div class="form-group">
        <label>2. السعر (اكتب الرقم فقط):</label>
        <input type="text" id="prodPrice" placeholder="مثال: 25,000">
    </div>
    
    <div class="form-group">
        <label>3. ارفع صورة المجسم من جهازك:</label>
        <input type="file" id="prodImage" accept="image/*" onchange="previewImage(event)">
        <div class="img-preview-box">
            <img id="preview" src="#" alt="معاينة الصورة ستظهر هنا" style="display:none; max-width:100%; max-height:200px; border-radius:8px; margin-top:10px;">
        </div>
    </div>

    <button class="gen-btn" onclick="generateProductCode()">🔥 توليد كارت مخصص واحد</button>

    <div class="output-section" id="outputArea" style="display: none;">
        <h3>📋 انسخ هذا الكود المخصص:</h3>
        <textarea id="resultCode" readonly onclick="this.select()"></textarea>
        <button class="copy-btn" onclick="copyTheCode()">اضغط هنا لنسخ الكود بلمحة بصر 📑</button>
    </div>
</div>

<script>
let base64Image = "";

function previewImage(event) {
    const reader = new FileReader();
    reader.onload = function() {
        const output = document.getElementById('preview');
        output.src = reader.result;
        output.style.display = 'block';
        base64Image = reader.result;
    }
    reader.readAsDataURL(event.target.files[0]);
}

// توليد الكارت المفرد مع المظهر المتجاوب الجديد (كارتين بالموبايل)
function generateProductCode() {
    const name = document.getElementById('prodName').value || "مجسم مخصص هيبة";
    let price = document.getElementById('prodPrice').value || "السعر حسب الطلب";
    
    if (price !== "السعر حسب الطلب" && !price.includes("د.ع") && !price.includes("دينار")) {
        price = price + " د.ع";
    }
    
    if(!base64Image) {
        alert("يا وحش ارفع صورة المجسم أولاً حتى يكتمل السحر!");
        return;
    }

    // الكود هنا يستعمل الفئات (Classes) المدمجة بالـ Style الأساسي في الأسفل لضمان عمل الموبايل 100%
    const generatedHTML = `<div class="product-card" onmouseover="this.style.transform='translateY(-12px) scale(1.02)'; this.style.borderColor='#ff5100'; this.style.boxShadow='0 20px 40px rgba(255, 68, 0, 0.45), 0 0 25px rgba(255, 166, 0, 0.35), 0 0 50px rgba(255, 68, 0, 0.15)';" onmouseout="this.style.transform='none'; this.style.borderColor='#222'; this.style.boxShadow='0 10px 30px rgba(255, 68, 0, 0.25), 0 0 15px rgba(255, 136, 0, 0.15)';">
    <div class="img-container">
        <img src="${base64Image}" alt="Product">
    </div>
    <div class="product-info">
        <h3>${name}</h3>
        <p class="price">${price}</p>
        <a href="https://wa.me/9647710705445?text=مرحبا_داثيون_ستور_اريد_اطلب_${encodeURIComponent(name)}" target="_blank" class="whatsapp-btn">اطلب عبر الواتساب 💬</a>
    </div>
</div>`;

    document.getElementById('resultCode').value = generatedHTML;
    document.getElementById('outputArea').style.display = 'block';
}

function copyTheCode() {
    const copyText = document.getElementById("resultCode");
    copyText.select();
    document.execCommand("copy");
    alert("تم نسخ كود الكارت المخصص بنجاح!");
}

// كود الـ 3 كروت مع التعديل الجذري ليصبح كارتين بجانب بعض في شاشات الموبايل
function copyTripleCode() {
    const tripleHTML = `<div class="dathiun-container">
    <h2 class="dathiun-title">المعرض الفني لـ DATHIUN ☣️</h2>
    <div class="dathiun-gallery">
        
        <div class="product-card">
            <div class="img-container"><img src="https://images.unsplash.com/photo-1608889174637-3c44f6326f20?w=500" alt="Product 1"></div>
            <div class="product-info">
                <h3>ستاند ريزدنت إيفل مخصص ☣️</h3>
                <p class="price">25,000 د.ع</p>
                <a href="https://wa.me/9647710705445?text=مرحبا_داثيون_ستور_اريد_اطلب_ستاند_ريزدنت_ايفل" target="_blank" class="whatsapp-btn">اطلب عبر الواتساب 💬</a>
            </div>
        </div>

        <div class="product-card">
            <div class="img-container"><img src="https://images.unsplash.com/photo-1559136555-9303baea8ebd?w=500" alt="Product 2"></div>
            <div class="product-info">
                <h3>مجسم شخصية إنمي هيبة 🔥</h3>
                <p class="price">35,000 د.ع</p>
                <a href="https://wa.me/9647710705445?text=مرحبا_داثيون_ستور_اريد_اطلب_مجسم_الشخصية" target="_blank" class="whatsapp-btn">اطلب عبر الواتساب 💬</a>
            </div>
        </div>

        <div class="product-card">
            <div class="img-container"><img src="https://images.unsplash.com/photo-1612287230202-1bf1d85d1bdf?w=500" alt="Product 3"></div>
            <div class="product-info">
                <h3>قاعدة ألعاب تكتيكية 🎮</h3>
                <p class="price">18,000 د.ع</p>
                <a href="https://wa.me/9647710705445?text=مرحبا_داثيون_ستور_اريد_اطلب_القاعدة_التكتيكية" target="_blank" class="whatsapp-btn">اطلب عبر الواتساب 💬</a>
            </div>
        </div>

    </div>
</div>

<style>
.dathiun-container { background-color: #0d0d0d; padding: 40px 10px; font-family: 'Segoe UI', sans-serif; direction: rtl; width: 100%; box-sizing: border-box; }
.dathiun-title { text-align: center; color: #ffffff; font-size: 2rem; margin-bottom: 30px; font-weight: 800; text-shadow: 0 0 15px rgba(255, 81, 0, 0.5); }
.dathiun-gallery { display: flex; flex-wrap: wrap; justify-content: center; gap: 20px; max-width: 1200px; margin: 0 auto; }

/* التصميم الأساسي للكارت (الحاسبة) */
.product-card { background: #141414; border: 1px solid #222; border-radius: 16px; width: 320px; overflow: hidden; box-shadow: 0 10px 30px rgba(255, 68, 0, 0.25), 0 0 15px rgba(255, 136, 0, 0.15); transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275); display: flex; flex-direction: column; }
.product-card:hover { transform: translateY(-12px) scale(1.02); border-color: #ff5100; box-shadow: 0 20px 40px rgba(255, 68, 0, 0.45), 0 0 25px rgba(255, 166, 0, 0.35), 0 0 50px rgba(255, 68, 0, 0.15); }
.img-container { width: 100%; height: 280px; overflow: hidden; background: #000; }
.img-container img { width: 100%; height: 100%; object-fit: cover; }
.product-info { padding: 20px; text-align: center; color: #fff; flex-grow: 1; display: flex; flex-direction: column; justify-content: space-between; }
.product-info h3 { margin: 0 0 10px 0; font-size: 1.3rem; font-weight: 700; line-height: 1.4; }
.product-info class .price { color: #ffaa00; font-weight: bold; font-size: 1.2rem; margin-bottom: 15px; text-shadow: 0 0 10px rgba(255, 170, 0, 0.3); }
.whatsapp-btn { display: block; background: linear-gradient(45deg, #ff5100, #ffaa00); color: #000000 !important; text-decoration: none !important; padding: 12px; border-radius: 10px; font-weight: bold; font-size: 0.95rem; box-shadow: 0 4px 15px rgba(255, 81, 0, 0.2); }

/* السحر الحقيقي للموبايل: ترتيب كارتين بجانب بعض وتصغير متناسق */
@media (max-width: 768px) {
    .dathiun-gallery { gap: 10px; padding: 0 5px; }
    /* جعل العرض 47% لكي يجلس كارتين وبينهما مسافة */
    .product-card { width: 47%; border-radius: 12px; }
    .img-container { height: 160px; } /* تقليل ارتفاع الصورة لتناسب الموبايل */
    .product-info { padding: 12px; }
    .product-info h3 { font-size: 0.95rem; margin-bottom: 6px; }
    .product-info .price { font-size: 0.9rem; margin-bottom: 10px; }
    .whatsapp-btn { padding: 8px 5px; font-size: 0.8rem; border-radius: 6px; }
    .dathiun-title { font-size: 1.5rem; }
}
</style>`;

    const dummy = document.createElement("textarea");
    document.body.appendChild(dummy);
    dummy.value = tripleHTML;
    dummy.select();
    document.execCommand("copy");
    document.body.removeChild(dummy);
    alert("تم نسخ كود النظام المرن (كارتين بالموبايل وبجانب بعض) بنجاح! جربه الآن 🔥");
}
</script>

<style>
.generator-container { background-color: #121212; border: 2px dashed #ff5100; border-radius: 16px; padding: 30px; max-width: 600px; margin: 40px auto; color: #fff; font-family: 'Segoe UI', sans-serif; direction: rtl; box-shadow: 0 10px 30px rgba(0,0,0,0.5); }
.generator-container h2 { color: #ffaa00; text-align: center; font-size: 1.6rem; margin-bottom: 10px; }
.quick-actions { display: flex; justify-content: center; margin-top: 15px; }
.triple-btn { background: linear-gradient(45deg, #111, #222); color: #ffaa00; border: 1px solid #ff5100; padding: 12px 20px; font-weight: bold; border-radius: 8px; cursor: pointer; width: 100%; transition: all 0.3s ease; }
.triple-btn:hover { background: linear-gradient(45deg, #ff5100, #ffaa00); color: #000; box-shadow: 0 0 15px rgba(255, 81, 0, 0.4); }
.form-group { margin-bottom: 20px; }
.form-group label { display: block; margin-bottom: 8px; font-weight: bold; color: #ddd; }
.form-group input[type="text"] { width: 100%; padding: 12px; background: #222; border: 1px solid #404040; border-radius: 8px; color: #fff; font-size: 1rem; }
.form-group input[type="file"] { background: #222; padding: 10px; border-radius: 8px; width: 100%; border: 1px solid #404040; color: #ccc; }
.gen-btn { width: 100%; background: linear-gradient(45deg, #222, #333); color: #fff; border: 1px solid #444; padding: 15px; font-size: 1.1rem; font-weight: bold; border-radius: 8px; cursor: pointer; transition: all 0.3s ease; }
.gen-btn:hover { background: linear-gradient(45deg, #ff5100, #ffaa00); color: #000; border-color: transparent; transform: translateY(-2px); box-shadow: 0 5px 20px rgba(255, 81, 0, 0.4); }
.output-section { margin-top: 30px; background: #050505; padding: 20px; border-radius: 10px; border: 1px solid #333; }
.output-section textarea { width: 100%; height: 150px; background: #111; color: #00ffcc; border: 1px solid #444; border-radius: 8px; padding: 10px; font-family: monospace; font-size: 0.9rem; resize: none; margin-top: 10px; }
.copy-btn { width: 100%; background: #00ffcc; color: #000; border: none; padding: 12px; font-weight: bold; border-radius: 6px; margin-top: 10px; cursor: pointer; }
</style>
