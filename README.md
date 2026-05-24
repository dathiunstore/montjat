// استبدل دالة generateProductCode بهذه الدالة الجديدة:
function generateProductCode() {
    const name = document.getElementById('prodName').value || "مجسم مخصص هيبة";
    let price = document.getElementById('prodPrice').value || "السعر حسب الطلب";
    const cat = document.getElementById('prodCat').value;
    
    if (price !== "السعر حسب الطلب" && !price.includes("د.ع")) price += " د.ع";
    
    if(!base64Image) {
        alert("يا وحش ارفع صورة المجسم أولاً!");
        return;
    }

    // كود خفيف جداً، مع إضافة loading="lazy" للسرعة، و class للستايل بدل الكود الطويل
    const generatedHTML = `<div class="product-card" data-category="${cat}">
    <div class="img-container">
        <img src="${base64Image}" alt="${name}" loading="lazy">
    </div>
    <div class="product-info">
        <h3>${name}</h3>
        <p class="price">${price}</p>
        <a href="https://wa.me/9647710705445?text=اريد_اطلب_${encodeURIComponent(name)}" target="_blank" class="whatsapp-btn">اطلب عبر الواتساب 💬</a>
    </div>
</div>`;

    document.getElementById('resultCode').value = generatedHTML;
    document.getElementById('outputArea').style.display = 'block';
}
