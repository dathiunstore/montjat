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
button:disabled{opacity:.55;cursor:not-allowed}
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
.status{font-size:12px;margin-top:8px;text-align:center;color:#aaa;min-height:18px}
.badge{display:inline-block;padding:3px 7px;border-radius:99px;background:#2b1a0a;color:#ffb000}
.hidden{opacity:.45}
.auth{max-width:430px;margin:80px auto;background:#0e0e0e;border:2px solid #333;border-radius:16px;padding:24px}
.auth h2{text-align:center;color:var(--orange);margin-top:0}
.auth .primary{margin-top:18px}
.logout{float:left}
.connection{font-size:12px;text-align:center;color:#777;margin-top:8px}
.price-note{color:#ffb000;font-size:12px;margin-top:5px}
@media(max-width:800px){
 .grid{grid-template-columns:1fr}
 .product{grid-template-columns:65px 1fr}
 .product img{width:65px;height:58px}
 .actions{grid-column:1/-1;justify-content:stretch}
 .actions button{flex:1}
}
</style>
</head>
<body>

<div id="loginView" class="auth">
  <h2>☣️ DATHIUN ADMIN ☣️</h2>
  <div class="sub">تسجيل دخول لوحة إدارة المنتجات</div>
  <label>الإيميل</label>
  <input id="email" type="email" autocomplete="username" placeholder="admin@email.com">
  <label>كلمة المرور</label>
  <input id="password" type="password" autocomplete="current-password" placeholder="••••••••">
  <button class="primary" id="loginBtn">🔐 تسجيل الدخول</button>
  <div class="status" id="loginStatus"></div>
  <div class="connection">Supabase متصل — البيانات محفوظة أونلاين</div>
</div>

<div id="adminView" style="display:none">
<div class="wrap">
  <button class="ghost logout" id="logoutBtn">خروج</button>
  <h1>☣️ DATHIUN — لوحة إدارة المنتجات ☣️</h1>
  <div class="sub">إضافة وتعديل وإخفاء وحذف المنتجات — مع ضغط الصور تلقائياً</div>

  <div class="grid">
    <section class="panel">
      <h2 id="formTitle">➕ إضافة منتج</h2>

      <label>اسم المنتج</label>
      <input id="name" placeholder="مثلاً: لوحة مفاتيح رزدنت ايفل">

      <label>السعر</label>
      <input id="price" inputmode="numeric" placeholder="مثلاً: 60000">
      <div class="price-note">اكتب الرقم فقط، مثلاً 60000 ← يتحول إلى 60,000 د.ع</div>

      <label>التصنيف</label>
      <select id="category">
        <option value="weapons">أسلحة</option>
        <option value="masks">أقنعة</option>
        <option value="stands">ستاندات</option>
        <option value="keycaps">Keycaps</option>
        <option value="figures">مجسمات</option>
        <option value="stickers">ستيكرات</option>
        <option value="keychains">ميداليات مفاتيح</option>
        <option value="Paintings">لوحات</option>
        <option value="others">أخرى</option>
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
        <button class="secondary" id="refreshBtn">🔄 تحديث</button>
      </div>
      <div id="list"></div>
    </section>
  </div>
</div>
</div>

<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
<script>
const SUPABASE_URL='https://sxnsqbsdtnhaiootnrcx.supabase.co';
const SUPABASE_PUBLISHABLE_KEY='sb_publishable_RgzROER9zDcoMIceT95FPw_P5czLDqL';
const BUCKET='product-images';
const WHATSAPP_NUMBER='9647710705445';

const db=window.supabase.createClient(SUPABASE_URL,SUPABASE_PUBLISHABLE_KEY);

let products=[];
let editId=null;
let imageFile=null;
let oldImageUrl='';

const $=id=>document.getElementById(id);

function escapeHTML(s=''){
 return String(s).replace(/[&<>"']/g,m=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#039;'}[m]));
}

/* 60000 -> 60,000 د.ع */
function formatPrice(value){
 const digits=String(value??'').replace(/[^\d]/g,'');
 if(!digits)return '';
 return Number(digits).toLocaleString('en-US')+' د.ع';
}

function setStatus(msg,ok=false){
 $('status').textContent=msg;
 $('status').style.color=ok?'#7dff8a':'#aaa';
}

function setLoginStatus(msg,ok=false){
 $('loginStatus').textContent=msg;
 $('loginStatus').style.color=ok?'#7dff8a':'#ff7777';
}

/* السعر يظهر مهيأ أثناء الكتابة */
$('price').addEventListener('input',()=>{
 const digits=$('price').value.replace(/[^\d]/g,'');
 if(digits){
   $('price').value=Number(digits).toLocaleString('en-US');
 }
});

function compressImage(file,max=1200,quality=.82){
 return new Promise((resolve,reject)=>{
  const r=new FileReader();
  r.onload=e=>{
   const img=new Image();
   img.onload=()=>{
    const scale=Math.min(1,max/img.width);
    const c=document.createElement('canvas');
    c.width=Math.max(1,Math.round(img.width*scale));
    c.height=Math.max(1,Math.round(img.height*scale));
    c.getContext('2d').drawImage(img,0,0,c.width,c.height);
    c.toBlob(blob=>{
      if(!blob){reject(new Error('تعذر ضغط الصورة'));return;}
      resolve(blob);
    },'image/jpeg',quality);
   };
   img.onerror=()=>reject(new Error('الصورة غير صالحة'));
   img.src=e.target.result;
  };
  r.onerror=()=>reject(new Error('تعذر قراءة الصورة'));
  r.readAsDataURL(file);
 });
}

function filePathFromPublicUrl(url){
 const marker='/storage/v1/object/public/'+BUCKET+'/';
 const i=(url||'').indexOf(marker);
 return i>=0?url.slice(i+marker.length):null;
}

async function uploadImage(file){
 const blob=await compressImage(file);
 const path='products/'+crypto.randomUUID()+'.jpg';

 const {error}=await db.storage.from(BUCKET).upload(path,blob,{
   contentType:'image/jpeg',
   upsert:false,
   cacheControl:'31536000'
 });
 if(error)throw error;

 const {data}=db.storage.from(BUCKET).getPublicUrl(path);
 return {url:data.publicUrl,path};
}

async function deleteImage(url){
 const path=filePathFromPublicUrl(url);
 if(!path)return;
 const {error}=await db.storage.from(BUCKET).remove([path]);
 if(error)console.warn('Image delete:',error.message);
}

$('loginBtn').onclick=async()=>{
 const email=$('email').value.trim();
 const password=$('password').value;

 if(!email||!password){
   setLoginStatus('اكتب الإيميل وكلمة المرور');
   return;
 }

 $('loginBtn').disabled=true;
 setLoginStatus('جاري تسجيل الدخول...',true);

 const {error}=await db.auth.signInWithPassword({email,password});

 $('loginBtn').disabled=false;

 if(error){
   setLoginStatus('فشل تسجيل الدخول: '+error.message);
   return;
 }

 setLoginStatus('تم الدخول ✅',true);
};

$('password').addEventListener('keydown',e=>{
 if(e.key==='Enter')$('loginBtn').click();
});

$('logoutBtn').onclick=async()=>{
 await db.auth.signOut();
};

$('image').onchange=async e=>{
 const f=e.target.files[0];
 if(!f)return;

 try{
   imageFile=f;
   setStatus('جاري ضغط الصورة...');
   const blob=await compressImage(f);
   const previewUrl=URL.createObjectURL(blob);

   $('preview').innerHTML='<img src="'+previewUrl+'">';
   $('sizeInfo').textContent=
     'الحجم الأصلي: '+(f.size/1024/1024).toFixed(2)+' MB — بعد الضغط: '+(blob.size/1024/1024).toFixed(2)+' MB';

   setStatus('الصورة جاهزة للرفع ✅',true);
 }catch(e){
   setStatus('خطأ بالصورة: '+e.message);
 }
};

$('saveBtn').onclick=async()=>{
 const name=$('name').value.trim();
 const price=formatPrice($('price').value);
 const category=$('category').value;

 if(!name||!price){
   setStatus('اكتب اسم المنتج والسعر أولاً');
   return;
 }

 $('saveBtn').disabled=true;

 try{
   let imageUrl=oldImageUrl;
   let newImagePath=null;

   if(imageFile){
     setStatus('جاري ضغط ورفع الصورة...');
     const up=await uploadImage(imageFile);
     imageUrl=up.url;
     newImagePath=up.path;
   }

   if(editId){
     const {error}=await db.from('products').update({
       name:name,
       price:price,
       category:category,
       image:imageUrl
     }).eq('id',editId);

     if(error){
       if(newImagePath)await deleteImage(imageUrl);
       throw error;
     }

     if(imageFile&&oldImageUrl)await deleteImage(oldImageUrl);

     setStatus('تم تعديل المنتج وحفظه أونلاين ✅',true);

   }else{
     if(!imageUrl){
       setStatus('اختر صورة المنتج أولاً');
       $('saveBtn').disabled=false;
       return;
     }

     const {error}=await db.from('products').insert({
       name:name,
       price:price,
       category:category,
       image:imageUrl,
       visible:true
     });

     if(error){
       if(newImagePath)await deleteImage(imageUrl);
       throw error;
     }

     setStatus('تمت إضافة المنتج وحفظه أونلاين ✅',true);
   }

   resetForm();
   await loadProducts();

 }catch(e){
   setStatus('حدث خطأ: '+(e.message||e));
 }

 $('saveBtn').disabled=false;
};

$('cancelBtn').onclick=resetForm;

function resetForm(){
 editId=null;
 imageFile=null;
 oldImageUrl='';

 $('name').value='';
 $('price').value='';
 $('category').value='weapons';
 $('image').value='';

 $('preview').textContent='اختر صورة للمنتج';
 $('sizeInfo').textContent='';

 $('formTitle').textContent='➕ إضافة منتج';
 $('saveBtn').textContent='💾 حفظ المنتج';
 $('cancelBtn').style.display='none';
}

function editProduct(id){
 const p=products.find(x=>String(x.id)===String(id));
 if(!p)return;

 editId=p.id;
 imageFile=null;
 oldImageUrl=p.image||'';

 $('name').value=p.name||'';
 $('price').value=String(p.price||'').replace(/[^\d]/g,'');
 $('price').dispatchEvent(new Event('input'));
 $('category').value=p.category||'others';
 $('image').value='';

 $('preview').innerHTML=p.image?'<img src="'+escapeHTML(p.image)+'">':'لا توجد صورة';
 $('sizeInfo').textContent='اترك الصورة كما هي إذا لا تريد تغييرها';

 $('formTitle').textContent='✏️ تعديل منتج';
 $('saveBtn').textContent='💾 حفظ التعديل';
 $('cancelBtn').style.display='block';

 scrollTo({top:0,behavior:'smooth'});
}

async function toggleProduct(id){
 const p=products.find(x=>String(x.id)===String(id));
 if(!p)return;

 const {error}=await db.from('products')
   .update({visible:!p.visible})
   .eq('id',id);

 if(error){
   setStatus('تعذر تغيير الظهور: '+error.message);
   return;
 }

 await loadProducts();
}

async function deleteProduct(id){
 const p=products.find(x=>String(x.id)===String(id));
 if(!p)return;

 if(!confirm('حذف هذا المنتج نهائياً؟'))return;

 setStatus('جاري الحذف...');

 const {error}=await db.from('products').delete().eq('id',id);

 if(error){
   setStatus('تعذر حذف المنتج: '+error.message);
   return;
 }

 if(p.image)await deleteImage(p.image);

 await loadProducts();
 setStatus('تم حذف المنتج ✅',true);
}

async function loadProducts(){
 $('list').innerHTML=
   '<div style="text-align:center;color:#777;padding:35px">جاري تحميل المنتجات...</div>';

 const {data,error}=await db.from('products')
   .select('*')
   .order('created_at',{ascending:false});

 if(error){
   $('list').innerHTML=
     '<div style="text-align:center;color:#ff7777;padding:35px">تعذر تحميل المنتجات<br>'+
     escapeHTML(error.message)+'</div>';
   return;
 }

 products=data||[];
 render();
}

function render(){
 const q=$('search').value.toLowerCase().trim();

 const arr=products.filter(p=>
   (String(p.name||'')+' '+String(p.price||'')+' '+String(p.category||''))
   .toLowerCase().includes(q)
 );

 $('list').innerHTML=arr.length?arr.map(p=>`
   <div class="product ${p.visible?'':'hidden'}">
     <img src="${escapeHTML(p.image||'')}" alt="">
     <div>
       <h3>${escapeHTML(p.name)}</h3>
       <div class="meta">
         ${escapeHTML(p.price||'')} ·
         <span class="badge">${escapeHTML(p.category||'others')}</span> ·
         ${p.visible?'ظاهر':'مخفي'}
       </div>
     </div>
     <div class="actions">
       <button class="secondary" onclick="editProduct('${String(p.id).replace(/'/g,"\\'")}')">✏️</button>
       <button class="secondary" onclick="toggleProduct('${String(p.id).replace(/'/g,"\\'")}')">
         ${p.visible?'👁️ إخفاء':'👁️ إظهار'}
       </button>
       <button class="danger" onclick="deleteProduct('${String(p.id).replace(/'/g,"\\'")}')">🗑️</button>
     </div>
   </div>
 `).join(''):
 '<div style="text-align:center;color:#777;padding:35px">لا توجد منتجات محفوظة بعد</div>';
}

$('search').oninput=render;
$('refreshBtn').onclick=loadProducts;

db.auth.onAuthStateChange((event,session)=>{
 if(session){
   $('loginView').style.display='none';
   $('adminView').style.display='block';
   loadProducts();
 }else{
   $('adminView').style.display='none';
   $('loginView').style.display='block';
 }
});

(async()=>{
 const {data:{session}}=await db.auth.getSession();

 if(session){
   $('loginView').style.display='none';
   $('adminView').style.display='block';
   await loadProducts();
 }
})();
</script>
</body>
</html>
