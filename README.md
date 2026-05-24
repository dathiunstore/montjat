<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <style>
        body { font-family: sans-serif; padding: 20px; background: #f4f4f4; text-align: center; }
        .box { background: #fff; padding: 20px; border-radius: 15px; max-width: 500px; margin: auto; box-shadow: 0 4px 10px rgba(0,0,0,0.1); }
        input, select, button { width: 100%; padding: 10px; margin: 5px 0; border-radius: 8px; border: 1px solid #ddd; }
        button { background: #ff5100; color: white; border: none; cursor: pointer; font-weight: bold; }
        .btn-group { display: flex; gap: 5px; margin-top: 10px; }
        .btn-group button { background: #333; }
        textarea { width: 100%; height: 120px; margin-top: 15px; border-radius: 8px; }
    </style>
</head>
<body>
    <div class="box">
        <h3>صانع الكروت الاحترافي</h3>
        <input type="text" id="name" placeholder="اسم المنتج">
        <input type="text" id="price" placeholder="السعر">
        <input type="text" id="img" placeholder="رابط الصورة">
        <select id="category">
            <option value="اقنعة">اقنعة</option>
            <option value="اسلحة">اسلحة</option>
            <option value="ميداليات">ميداليات</option>
            <option value="ستاندات">ستاندات</option>
            <option value="مجسمات">مجسمات</option>
            <option value="ستيكرات">ستيكرات</option>
            <option value="اخرى">اخرى</option>
        </select>

        <div class="btn-group">
            <button onclick="generate(4)">نسخ 4 كروت</button>
            <button onclick="generate(2)">نسخ 2 كروت</button>
        </div>
        <textarea id="output" readonly></textarea>
    </div>

    <script>
        function generate(count) {
            const name = document.getElementById('name').value;
            const price = document.getElementById('price').value;
            const img = document.getElementById('img').value;
            const cat = document.getElementById('category').value;
            let cards = "";
            for(let i=0; i<count; i++) {
                cards += `<div class="product-item" data-category="${cat}">\n  <img src="${img}" loading="lazy">\n  <h3>${name}</h3>\n  <p>${price}</p>\n  <button>معاينة AR</button>\n</div>\n`;
            }
            document.getElementById('output').value = cards;
        }
    </script>
</body>
</html>
