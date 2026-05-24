<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>أداة DATHIUN النهائية</title>
    <style>
        body { font-family: sans-serif; background: #111; color: white; padding: 20px; }
        .container { max-width: 700px; margin: auto; background: #222; padding: 20px; border-radius: 10px; text-align: center; }
        textarea { width: 100%; height: 350px; background: #000; color: #0f0; border: none; padding: 10px; margin-top: 15px; font-family: monospace; }
        button { width: 100%; padding: 15px; margin-top: 10px; background: #ff4500; color: white; font-weight: bold; border: none; border-radius: 5px; cursor: pointer; font-size: 18px; }
    </style>
</head>
<body>
    <div class="container">
        <h2>مولد DATHIUN المتكامل</h2>
        <p>اضغط الزر لنسخ كود "المعرض الكامل" (ستايل + أزرار + 4 كروت) دفعة واحدة</p>
        <button onclick="copyFullGallery()">📋 نسخ كود المعرض الكامل</button>
        <textarea id="output" readonly></textarea>
    </div>

    <script>
        const fullGalleryCode = `<style>
    .filter-menu { text-align: center; margin-bottom: 40px; }
    .btn-all { font-size: 22px; font-weight: bold; color: #fff; background: linear-gradient(to right, #ff4500, #ff8c00); border: none; padding: 12px 40px; cursor: pointer; border-radius: 50px; box-shadow: 0 0 10px #ff4500; transition: 0.3s; }
    .category-btns { display: flex; justify-content: center; flex-wrap: wrap; gap: 12px; margin-top: 15px; }
    .category-btns button { background: #222; color: #ffcc00; border: 2px solid #ff4500; padding: 10px 20px; cursor: pointer; border-radius: 30px; font-weight: bold; transition: 0.3s; }
    .category-btns button:hover { background: #ff4500; color: #fff; box-shadow: 0 0 10px #ff4500; }
    .product-gallery { display: flex; flex-wrap: wrap; justify-content: center; gap: 15px; padding: 10px; }
    .fire-card { width: calc(25% - 20px); max-width: 250px; padding: 10px; background: #000; border: 2px solid #ff4500; border-radius: 15px; box-shadow: 0 0 10px rgba(255, 69, 0, 0.3); text-align: center; color: #ffcc00; transition: transform 0.4s ease, box-shadow 0.4s ease; box-sizing: border-box; }
    @media (max-width: 768px) { .fire-card { width: calc(50% - 15px); } }
    .fire-card:hover { transform: scale(1.03); box-shadow: 0 0 25px rgba(255, 69, 0, 0.7); }
    .fire-card img { width: 100%; aspect-ratio: 1 / 1; object-fit: cover; border-radius: 10px; }
    .fire-card h3 { color: #ffffff; margin: 8px 0; font-size: 16px; }
    .fire-card p { font-size: 15px; color: #ffcc00; font-weight: bold; margin-bottom: 8px; }
    .fire-btn { display: block; background: linear-gradient(to right, #ff4500, #ff8c00); color: #000000 !important; padding: 8px; text-decoration: none; border-radius: 5px; margin-top: 5px; font-weight: bold; font-size: 13px; }
</style>

<div class="filter-menu">
    <button class="btn-all" onclick="filterCards('all')">الكل</button>
    <div class="category-btns">
        <button onclick="filterCards('weapons')">أسلحة</button>
        <button onclick="filterCards('masks')">أقنعة</button>
        <button onclick="filterCards('figures')">مجسمات</button>
        <button onclick="filterCards('others')">أخرى</button>
    </div>
</div>

<div class="product-gallery" id="productGrid">
    <div class="fire-card" data-category="weapons"><img src="https://via.placeholder.com/300" loading="lazy"><h3>منتج 1</h3><p>5000 د.ع</p><a href="#" class="fire-btn">💬 اطلبه الآن</a></div>
    <div class="fire-card" data-category="masks"><img src="https://via.placeholder.com/300" loading="lazy"><h3>منتج 2</h3><p>5000 د.ع</p><a href="#" class="fire-btn">💬 اطلبه الآن</a></div>
    <div class="fire-card" data-category="figures"><img src="https://via.placeholder.com/300" loading="lazy"><h3>منتج 3</h3><p>15000 د.ع</p><a href="#" class="fire-btn">💬 اطلبه الآن</a></div>
    <div class="fire-card" data-category="others"><img src="https://via.placeholder.com/300" loading="lazy"><h3>منتج 4</h3><p>2000 د.ع</p><a href="#" class="fire-btn">💬 اطلبه الآن</a></div>
</div>

<script>
    function filterCards(cat) {
        document.querySelectorAll('.fire-card').forEach(card => {
            card.style.display = (cat === 'all' || card.getAttribute('data-category') === cat) ? 'block' : 'none';
        });
    }
</script>`;

        function copyFullGallery() {
            const textarea = document.getElementById('output');
            textarea.value = fullGalleryCode;
            textarea.select();
            document.execCommand('copy');
            alert("تم نسخ كود المعرض الكامل بنجاح! الآن ألصقه في صفحة متجرك.");
        }
    </script>
</body>
</html>
