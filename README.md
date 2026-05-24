<!DOCTYPE html>
<html dir="rtl">
<body>
    <h3>صانع كروت المنتجات (النسخة المدمجة)</h3>
    
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

    <button onclick="generate()">توليد الكود</button>
    <textarea id="output" style="width:100%; height:150px; margin-top:10px;"></textarea>

    <script>
        function generate() {
            const name = document.getElementById('name').value;
            const price = document.getElementById('price').value;
            const img = document.getElementById('img').value;
            const cat = document.getElementById('category').value;

            const code = `<div class="product-item" data-category="${cat}">
    <img src="${img}" alt="${name}" loading="lazy">
    <h3>${name}</h3>
    <p>${price}</p>
    <button onclick="openAR()">معاينة AR</button>
</div>`;
            document.getElementById('output').value = code;
        }
    </script>
</body>
</html>
