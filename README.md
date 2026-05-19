<div class="dathiun-products-grid">

    <div class="product-card">
        <div class="img-container">
            <img src="ضع_هنا_كود_الصورة_الأولى_Base64_أو_الرابط" alt="Product 1">
        </div>
        <div class="product-info">
            <h3>اسم المنتج الأول ☣️</h3>
            <p class="price">25,000 د.ع</p>
            <a href="https://wa.me/9647710705445?text=اريد_طلب_المنتج_الأول" target="_blank" class="whatsapp-btn">
                اطلب عبر الواتساب 💬
            </a>
        </div>
    </div>

    <div class="product-card">
        <div class="img-container">
            <img src="ضع_هنا_كود_الصورة_الثانية_Base64_أو_الرابط" alt="Product 2">
        </div>
        <div class="product-info">
            <h3>اسم المنتج الثاني 🔥</h3>
            <p class="price">30,000 د.ع</p>
            <a href="https://wa.me/9647710705445?text=اريد_طلب_المنتج_الثاني" target="_blank" class="whatsapp-btn">
                اطلب عبر الواتساب 💬
            </a>
        </div>
    </div>

    <div class="product-card">
        <div class="img-container">
            <img src="ضع_هنا_كود_الصورة_الثالثة_Base64_أو_الرابط" alt="Product 3">
        </div>
        <div class="product-info">
            <h3>اسم المنتج الثالث ⚡</h3>
            <p class="price">15,000 د.ع</p>
            <a href="https://wa.me/9647710705445?text=اريد_طلب_المنتج_الثالث" target="_blank" class="whatsapp-btn">
                اطلب عبر الواتساب 💬
            </a>
        </div>
    </div>

</div>

<style>
.dathiun-products-grid {
    display: flex; /* هذا السطر السحري هو المسؤول عن جعلهم واحد جنب الثاني */
    flex-wrap: wrap; /* إذا زادت الكروت عن عرض الشاشة تنزل للسطر الثاني تلقائياً بدون مشاكل */
    justify-content: center; /* تملأ المنتجات وسط الشاشة بالتساوي */
    gap: 25px; /* المسافة الفاصلة بين كارت وكارت */
    padding: 40px 10px;
    background-color: #0d0d0d; /* خلفية المتجر المظلمة */
    direction: rtl;
    width: 100%;
}

/* تصميم الكارت الفردي */
.product-card {
    background: #141414;
    border: 1px solid #252525;
    border-radius: 16px;
    width: 300px; /* عرض الكارت المناسب ليظهر 3 أو 4 كروت جنب بعض على الشاشة الكبيرة */
    overflow: hidden;
    box-shadow: 0 15px 35px rgba(0,0,0,0.6);
    transition: all 0.4s ease;
    font-family: 'Segoe UI', sans-serif;
}

.product-card:hover {
    transform: translateY(-10px);
    border-color: #ff5100; /* التوهج البرتقالي مالتنا عند الهوفر */
    box-shadow: 0 20px 40px rgba(255, 81, 0, 0.2);
}

.img-container {
    width: 100%;
    height: 260px;
    background: #000;
}

.img-container img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.product-info {
    padding: 20px;
    text-align: center;
    color: #fff;
}

.product-info h3 {
    margin: 0 0 10px 0;
    font-size: 1.25rem;
    font-weight: 700;
}

.product-info .price {
    color: #ffaa00;
    font-weight: bold;
    font-size: 1.2rem;
    margin-bottom: 18px;
}

.whatsapp-btn {
    display: block;
    background: linear-gradient(45deg, #ff5100, #ffaa00);
    color: #000000 !important;
    text-decoration: none !important;
    padding: 12px;
    border-radius: 10px;
    font-weight: bold;
    font-size: 0.95rem;
    transition: all 0.3s ease;
}

.whatsapp-btn:hover {
    box-shadow: 0 5px 15px rgba(255, 81, 0, 0.4);
}
</style>
