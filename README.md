<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>أداة DATHIUN Store الاحترافية</title>
    <style>
        body { font-family: sans-serif; background: #121212; color: #fff; padding: 20px; }
        .wrapper { max-width: 800px; margin: auto; background: #1e1e1e; padding: 25px; border-radius: 15px; border: 1px solid #ff4500; }
        textarea { width: 100%; height: 400px; background: #000; color: #0f0; border: 1px solid #444; padding: 15px; margin-top: 15px; font-family: monospace; border-radius: 8px; box-sizing: border-box; }
        .controls { display: flex; gap: 10px; margin-top: 15px; }
        button { flex: 1; padding: 15px; background: #ff4500; color: white; font-weight: bold; border: none; border-radius: 8px; cursor: pointer; transition: 0.3s; }
        button:hover { background: #e03e00; }
        h2 { color: #ff4500; text-align: center; }
    </style>
</head>
<body>
    <div class="wrapper">
        <h2>لوحة تحكم DATHIUN</h2>
        <p>هذه الأداة تحتوي على كود المعرض المتكامل (الستايل + الأزرار + الفلترة + ترتيب 4 كروت).</p>
        <div class="controls">
            <button onclick="copyFullCode()">📋 نسخ كود المعرض الكامل</button>
        </div>
        <textarea id="output" readonly placeholder="سيظهر كود المعرض هنا بعد الضغط على الزر..."></textarea>
    </div>

    <script>
        function copyFullCode() {
            const code = `<style>
    .filter-menu { text-align: center; margin-bottom: 30px; }
    .btn-all { font-size: 20px; font-weight: bold; color: #fff; background: linear-gradient(135deg, #ff4500, #ff8c00); border: none; padding: 12px 35px; cursor: pointer; border-radius: 30px; box-shadow: 0 4px 15px rgba(255,69,0,0.4); }
    .category-btns { display: flex; justify-content: center; gap: 10px; margin-top: 15px; flex-wrap: wrap; }
    .category-btns button { background: #222; color: #ffcc00; border: 2px solid #ff4500; padding: 8px 20px; cursor: pointer; border-radius: 20px; font-weight: bold; }
    .category-btns button:hover { background: #ff4500; color: #fff; }
    .product-gallery { display: flex; flex-wrap: wrap; justify-content: center; gap: 20px; padding: 15px; }
    .fire-card { width: calc(25% - 20px); min-width: 200px; padding: 15px; background: #000; border: 2px solid #ff4500; border-radius: 15px; text-align: center; box-sizing: border-box; transition: 0.3s; }
    @media (max-width: 768px) { .fire-card { width: calc(50% - 15px); } }
    .fire-card img { width: 100%; aspect-ratio: 1/1; object-fit: cover; border-radius: 10px; }
    .fire-btn { display: block; background: #ff4500; color: #fff; padding: 10px; text-decoration: none; border-radius: 5px; margin-top: 10px; font-weight: bold; }
</style>

<div class="filter-menu">
    <button class="btn-all" onclick="filterCards('all')">الكل</button>
    <div class="category-btns">
        <button onclick="filterCards('weapons')">أسلحة</button>
        <button onclick="filterCards('masks')">أقنعة</button>
        <button onclick="filterCards('figures')">مجسمات</button>
    </div>
</div>

<div class="product-gallery" id="productGrid">
    <!-- أضف كروت منتجاتك هنا -->
    <div class="fire-card" data-category="weapons"><img src="صورة_السلاح.jpg"><h3>سلاح</h3><a href="#" class="fire-btn">اطلب</a></div>
</div>

<script>
    function filterCards(c) {
        document.querySelectorAll('.fire-card').forEach(card => {
            card.style.display = (c === 'all' || card.dataset.category === c) ? 'block' : 'none';
        });
    }
</script>`;
            
            document.getElementById('output').value = code;
            document.getElementById('output').select();
            document.execCommand('copy');
            alert("تم نسخ كود المعرض الكامل! هو الآن في حافظة النسخ، يمكنك لصقه مباشرة.");
        }
    </script>
</body>
</html>
