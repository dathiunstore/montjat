<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>DATHIUN — لوحة إدارة المنتجات</title>
<style>
:root{--orange:#ff6a00;--yellow:#ffc400;--bg:#090909;--panel:#111;--panel2:#181818;--muted:#999;--danger:#ff4444}
*{box-sizing:border-box}
body{margin:0;background:radial-gradient(circle at top,#1b1005 0,#090909 42%);color:#fff;font-family:Arial,Tahoma,sans-serif}
.wrap{max-width:1100px;margin:auto;padding:22px}
h1{margin:0 0 6px;color:var(--yellow);text-align:center}
.sub{text-align:center;color:#aaa;margin-bottom:22px}
.grid{display:grid;grid-template-columns:360px 1fr;gap:18px}
.panel{background:#0e0e0e;border:2px solid #333;border-radius:16px;padding:18px}
.panel h2{margin-top:0;color:var(--orange)}
label{display:block;margin:13px 0 6px;color:#ddd;font-weight:bold}
input,select{width:100%;padding:12px;border:1px solid #444;border-radius:9px;background:#181818;color:#fff;font-size:15px}
button{border:0;border-radius:9px;padding:11px 14px;cursor:pointer;font-weight:bold}
.primary{width:100%;background:linear-gradient(135deg,#ff8a00,#ff4b00);color:#fff;font-size:16px;margin-top:16px}
.secondary{background:#242424;color:#fff}.danger{background:#8e2020;color:#fff}.ghost{background:#191919;color:#ddd;border:1px solid #444}
.preview{height:190px;border:1px dashed #555;border-radius:10px;display:flex;align-items:center;justify-content:center;overflow:hidden;background:#080808;color:#777}
.preview img{width:100%;height:100%;object-fit:cover}
.small{font-size:12px;color:#888;margin-top:6px}
.toolbar{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:12px}
.toolbar input{flex:1;min-width:180px}
.product{display:grid;grid-template-columns:80px 1fr auto;gap:12px;align-items:center;background:#151515;border:1px solid #333;border-radius:12px;padding:9px;margin-bottom:9px}
.product img{width:80px;height:65px;object-fit:cover;border-radius:8px}
.product h3{margin:0 0 5px;font-size:16px}.meta{font-size:13px;color:#aaa}
.actions{display:flex;gap:6px;flex-wrap:wrap;justify-content:flex-end}
.status{font-size:12px;margin-top:8px;text-align:center;color:#aaa}
.badge{display:inline-block;padding:3px 7px;border-radius:99px;background:#2b1a0a;color:#ffb000}
.hidden{opacity:.45}
@media(max-width:800px){.grid{grid-template-columns:1fr}.product{grid-template-columns:65px 1fr}.product img{width:65px;height:58px}.actions{grid-column:1/-1;justify-content:stretch}.actions button{flex:1}}
</style>
</head>
<body>
<div class="wrap">
<h1>☣️ DATHIUN — لوحة إدارة المنتجات ☣️</h1>
<div class="sub">إضافة وتعديل وإخفاء وحذف المنتجات — مع ضغط الصور تلقائياً</div>

<div class="grid">
<section class="panel">
<h2 id="formTitle">➕ إضافة منتج</h2>
<label>اسم المنتج</label>
<input id="name" placeholder="مثلاً: ميدالية رزدنت ايفل">
<label>السعر</label>
<input id="price" placeholder="مثلاً: 15,000 د.ع">
<label>التصنيف</label>
<select id="category">
<option value="weapons">أسلحة</option><option value="masks">أقنعة</option><option value="stands">ستاندات</option>
<option value="keycaps">Keycaps</option><option value="figures">مجسمات</option><option value="stickers">ستيكرات</option>
<option value="keychains">ميداليات مفاتيح</option><option value="Paintings">لوحات</option><option value="others">أخرى</option>
</select>
<label>الصورة</label>
<input id="image" type="file" accept="image/*">
<div class="preview" id="preview">اختر صورة للمنتج</div>
<div class="small" id="sizeInfo"></div>
<button class="primary" id="saveBtn">💾 حفظ المنتج</button>
<button class="ghost" id="cancelBtn" style="display:none;width:100%;margin-top:8px">إلغاء التعديل</button>
<div class="status" id="status"></div>
</section>

<section class="panel">
<h2>📦 المنتجات</h2>
<div class="toolbar">
<input id="search" placeholder="🔍 ابحث عن منتج...">
<button class="secondary" id="exportBtn">⬇️ تصدير</button>
<button class="secondary" id="importBtn">⬆️ استيراد</button>
<input id="importFile" type="file" accept=".json" style="display:none">
</div>
<div id="list"></div>
</section>
</div>
</div>

<script>
const KEY='dathiun_products_v1';
let products=JSON.parse(localStorage.getItem(KEY)||'[]');
let editId=null, imageData='';

const $=id=>document.getElementById(id);
function save(){localStorage.setItem(KEY,JSON.stringify(products));render()}
function escapeHTML(s=''){return s.replace(/[&<>"']/g,m=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#039;'}[m]))}
function compress(file,max=1200,quality=.82){
 return new Promise((resolve,reject)=>{
  const r=new FileReader();
  r.onload=e=>{
   const img=new Image();
   img.onload=()=>{
    const scale=Math.min(1,max/img.width),c=document.createElement('canvas');
    c.width=Math.round(img.width*scale);c.height=Math.round(img.height*scale);
    c.getContext('2d').drawImage(img,0,0,c.width,c.height);
    resolve(c.toDataURL('image/jpeg',quality));
   };img.onerror=reject;img.src=e.target.result;
  };r.onerror=reject;r.readAsDataURL(file);
 })
}
$('image').onchange=async e=>{
 const f=e.target.files[0];if(!f)return;
 $('status').textContent='جاري ضغط الصورة...';
 imageData=await compress(f);
 $('preview').innerHTML='<img src="'+imageData+'">';
 $('sizeInfo').textContent='الحجم الأصلي: '+(f.size/1024/1024).toFixed(2)+' MB — الصورة مضغوطة وجاهزة';
 $('status').textContent='تم ضغط الصورة ✅';
};
$('saveBtn').onclick=()=>{
 const name=$('name').value.trim(),price=$('price').value.trim(),category=$('category').value;
 if(!name||!price){$('status').textContent='اكتب اسم المنتج والسعر أولاً';return}
 if(editId){
  const p=products.find(x=>x.id===editId);p.name=name;p.price=price;p.category=category;if(imageData)p.image=imageData;
  $('status').textContent='تم تعديل المنتج ✅';
 }else{
  if(!imageData){$('status').textContent='اختر صورة المنتج أولاً';return}
  products.unshift({id:Date.now().toString(),name,price,category,image:imageData,visible:true});
  $('status').textContent='تمت إضافة المنتج ✅';
 }
 save();resetForm();
};
$('cancelBtn').onclick=resetForm;
function resetForm(){editId=null;imageData='';$('name').value='';$('price').value='';$('image').value='';$('preview').textContent='اختر صورة للمنتج';$('sizeInfo').textContent='';$('formTitle').textContent='➕ إضافة منتج';$('saveBtn').textContent='💾 حفظ المنتج';$('cancelBtn').style.display='none'}
function edit(id){
 const p=products.find(x=>x.id===id);if(!p)return;editId=id;$('name').value=p.name;$('price').value=p.price;$('category').value=p.category;imageData=p.image;$('preview').innerHTML='<img src="'+p.image+'">';$('formTitle').textContent='✏️ تعديل منتج';$('saveBtn').textContent='💾 حفظ التعديل';$('cancelBtn').style.display='block';scrollTo({top:0,behavior:'smooth'})
}
function toggle(id){const p=products.find(x=>x.id===id);p.visible=!p.visible;save()}
function del(id){if(confirm('حذف هذا المنتج نهائياً؟')){products=products.filter(x=>x.id!==id);save()}}
function render(){
 const q=$('search').value.toLowerCase();const arr=products.filter(p=>(p.name+' '+p.price).toLowerCase().includes(q));
 $('list').innerHTML=arr.length?arr.map(p=>`<div class="product ${p.visible?'':'hidden'}">
 <img src="${p.image}" alt=""><div><h3>${escapeHTML(p.name)}</h3><div class="meta">${escapeHTML(p.price)} · <span class="badge">${escapeHTML(p.category)}</span> · ${p.visible?'ظاهر':'مخفي'}</div></div>
 <div class="actions"><button class="secondary" onclick="edit('${p.id}')">✏️</button><button class="secondary" onclick="toggle('${p.id}')">${p.visible?'👁️ إخفاء':'👁️ إظهار'}</button><button class="danger" onclick="del('${p.id}')">🗑️</button></div></div>`).join(''):'<div style="text-align:center;color:#777;padding:35px">لا توجد منتجات محفوظة بعد</div>';
}
$('search').oninput=render;
$('exportBtn').onclick=()=>{const a=document.createElement('a');a.href=URL.createObjectURL(new Blob([JSON.stringify(products)],{type:'application/json'}));a.download='dathiun-products.json';a.click()}
$('importBtn').onclick=()=>$('importFile').click();
$('importFile').onchange=e=>{const f=e.target.files[0];if(!f)return;const r=new FileReader();r.onload=()=>{try{products=JSON.parse(r.result);save();$('status').textContent='تم الاستيراد ✅'}catch{$('status').textContent='ملف غير صالح'}};r.readAsText(f)}
render();
</script>
</body>
</html>
