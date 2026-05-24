<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>مولد كروت DATHIUN النهائي</title>
    <style>
        body { font-family: sans-serif; background: #111; color: white; padding: 20px; }
        .container { max-width: 600px; margin: auto; background: #222; padding: 20px; border-radius: 10px; }
        input, select, button { width: 100%; padding: 12px; margin: 10px 0; border-radius: 5px; border: none; }
        button { background: #ff4500; color: white; font-weight: bold; cursor: pointer; }
        #copyBtn { background: #25d366; display: none; margin-top: 10px; }
    </style>
</head>
<body>
    <div class="container">
        <h2>مولد كروت DATHIUN (النسخة المتوافقة)</h2>
        <input type="file" id="imgInput" accept="image/*">
        <input type="text" id="nameInput" placeholder="اسم المنتج">
        <input type="text" id="priceInput" placeholder="السعر">
        <select id="categoryInput">
            <option value="figures">مجسمات</option>
            <option value="stands">ستاندات</option>
            <option value="weapons">أسلحة</option>
            <option value="keycaps">كيكابس</option>
            <option value="masks">أقنعة</option>
            <option value="keychains">ميداليات</option>
            <option value="stickers">ستيكرات</option>
            <option value="others">أخرى</option>
        </select>
        <button onclick="generateCard()">توليد الكود</button>
        <textarea id="output" rows="5" style="width:100%; margin-top:10px; background:#000; color:#0f0; border:none; padding:10px; display:none;"></textarea>
        <button id="copyBtn" onclick="copyCode()">📋 نسخ الكود</button>
    </div>

    <script>
        function convertToEnglishNumbers(str) {
            const arabicNumbers = ['٠', '١', '٢', '٣', '٤', '٥', '٦', '٧', '٨', '٩'];
            const englishNumbers = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'];
            let result = str;
            for (let i = 0; i < 10; i++) {
                result = result.replace(new RegExp(arabicNumbers[i], 'g'), englishNumbers[i]);
            }
            return result;
        }

        function generateCard() {
            const file = document.getElementById('imgInput').files[0];
            const name = document.getElementById('nameInput').value;
            const price = convertToEnglishNumbers(document.getElementById('priceInput').value);
            const cat = document.getElementById('categoryInput').value;
            
            if(!file) { alert("يرجى اختيار صورة!"); return; }

            const reader = new FileReader();
            reader.onload = function(e) {
                const img = new Image();
                img.onload = function() {
                    const canvas = document.createElement('canvas');
                    canvas.width = 300; canvas.height = 300;
                    const ctx = canvas.getContext('2d');
                    const size = Math.min(img.width, img.height);
                    ctx.drawImage(img, (img.width-size)/2, (img.height-size)/2, size, size, 0, 0, 300, 300);
                    const compressedUrl = canvas.toDataURL('image/jpeg', 0.6); 

                    // الكود المولد الآن متوافق تماماً مع كود المعرض الجديد
                    const fullHtml = `<div class="fire-card" data-category="${cat}">
    <img src="${compressedUrl}" loading="lazy">
    <h3>${name}</h3>
    <p>${price} د.ع</p>
    <a href="https://wa.me/9647710705445?text=اريد طلب ${name} بسعر ${price} د.ع" class="fire-btn">💬 اطلبه الآن من الواتساب</a>
</div>`;
                    
                    document.getElementById('output').style.display = 'block';
                    document.getElementById('output').value = fullHtml;
                    document.getElementById('copyBtn').style.display = 'block';
                    window.currentHtml = fullHtml;
                };
                img.src = e.target.result;
            };
            reader.readAsDataURL(file);
        }

        function copyCode() {
            document.getElementById('output').select();
            document.execCommand('copy');
            alert("تم نسخ الكود! اذهب لصفحة المعرض وألصقه داخل الـ product-gallery.");
        }
    </script>
</body>
</html>
