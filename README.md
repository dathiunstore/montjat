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
        <label>3. القسم:</label>
        <select id="prodCat" style="width:100%; padding:12px; background:#222; border:1px solid #404040; border-radius:8px; color:#fff;">
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
        <label>4. ارفع صورة المجسم:</label>
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

function generateProductCode() {
    const name = document.getElementById('prodName').value || "مجسم مخصص هيبة";
    let price = document.getElementById('prodPrice').value || "السعر حسب الطلب";
    const cat = document.getElementById('prodCat').value;
    
    if (price !== "السعر حسب الطلب" && !price.includes("د.ع")) { price = price + " د.ع"; }
    
    if(!base64Image) { alert("ارفع الصورة أولاً!"); return; }

    const generatedHTML = `<div class="product-card" data-category="${cat}">
    <div class="img-container"><img src="${base64Image}" alt="${name}"></div>
    <div class="product-info">
        <h3>${name}</h3>
        <p class="price">${price}</p>
        <a href="https://wa.me/9647710705445?text=اريد_اطلب_${encodeURIComponent(name)}" target="_blank" class="whatsapp-btn">اطلب عبر الواتساب 💬</a>
    </div>
</div>`;

    document.getElementById('resultCode').value = generatedHTML;
    document.getElementById('outputArea').style.display = 'block';
}

function copyTheCode() {
    const copyText = document.getElementById("resultCode");
    copyText.select();
    document.execCommand("copy");
    alert("تم النسخ!");
}

function copyQuadCode() {
    alert("هذا الزر ينسخ القالب الأساسي. لاحقاً ستضع كود كل منتج بداخله.");
}
</script>
