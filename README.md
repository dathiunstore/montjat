<div class="generator-container">
    <h2>☣️ لوحة تحكم DATHIUN لتوليد كروت المنتجات ☣️</h2>
    <p style="text-align: center; color: #888; margin-bottom: 25px;">ادخل البيانات لتوليد كارت مخصص، أو انسخ النظام الرباعي الجاهز فوراً</p>
    
    <div class="quick-actions">
        <button class="triple-btn" onclick="copyQuadCode()">📋 نسخ كود الـ 4 كروت الجاهزة (2 تحت 2 بالموبايل)</button>
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
        <label>3. اختر القسم:</label>
        <select id="prodCat" style="width: 100%; padding: 12px; background: #222; border: 1px solid #404040; border-radius: 8px; color: #fff;">
            <option value="اقنعة">اقنعة</option>
            <option value="اسلحة">اسلحة</option>
            <option value="ميداليات">ميداليات</option>
            <option value="ستاندات">ستاندات</option>
            <option value="مجسمات">مجسمات</option>
            <option value="ستيكرات">ستيكرات</option>
            <option value="اخرى">اخرى</option>
        </select>
    </div>
    
    <div class="form-group">
        <label>4. ارفع صورة المجسم (سيتم ضغطها تلقائياً):</label>
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

<canvas id="canvas" style="display:none;"></canvas>

<script>
let base64Image = "";

function previewImage(event) {
    const file = event.target.files[0];
    const reader = new FileReader();
    
    reader.onload = function(e) {
        const img = new Image();
        img.onload = function() {
            // ضغط الصورة: تقليل العرض إلى 500 بكسل كحد أقصى للحفاظ على الجودة والسرعة
            const canvas = document.getElementById('canvas');
            const ctx = canvas.getContext('2d');
            const scale = 500 / img.width;
            canvas.width = 500;
            canvas.height = img.height * scale;
            ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
            
            base64Image = canvas.toDataURL('image/jpeg', 0.7); // ضغط بنسبة 70%
            const output = document.getElementById('preview');
            output.src = base64Image;
            output.style.display = 'block';
        };
        img.src = e.target.result;
    };
    reader.readAsDataURL(file);
}

function generateProductCode() {
    const name = document.getElementById('prodName').value || "مجسم مخصص هيبة";
    let price = document.getElementById('prodPrice').value || "السعر حسب الطلب";
    const cat = document.getElementById('prodCat').value;
    
    if (price !== "السعر حسب الطلب" && !price.includes("د.ع") && !price.includes("دينار")) {
        price = price + " د.ع";
    }
    
    if(!base64Image) {
        alert("يا وحش ارفع صورة المجسم أولاً حتى يكتمل السحر!");
        return;
    }

    const generatedHTML = `<div class="product-card" data-category="${cat}" onmouseover="this.style.transform='translateY(-12px) scale(1.02)'; this.style.borderColor='#ff5100'; this.style.boxShadow='0 20px 40px rgba(255, 68, 0, 0.45), 0 0 25px rgba(255, 166, 0, 0.35), 0 0 50px rgba(255, 68, 0, 0.15)';" onmouseout="this.style.transform='none'; this.style.borderColor='#222'; this.style.boxShadow='0 10px 30px rgba(255, 68, 0, 0.25), 0 0 15px rgba(255, 136, 0, 0.15)';">
    <div class="img-container">
        <img src="${base64Image}" alt="${name}">
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

function copyQuadCode() {
    const quadHTML = `<div class="dathiun-container">
    <h2 class="dathiun-title">المعرض الفني لـ DATHIUN ☣️</h2>
    <div class="dathiun-gallery">
        </div>
</div>`;
    alert("استخدم زر توليد كرت واحد لإضافة الكروت داخل هذا الهيكل!");
}
</script>
