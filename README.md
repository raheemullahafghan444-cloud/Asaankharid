<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>آسان خرید - خرید آسان، زندگی بهتر</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: sans-serif; }
        :root { --primary: #2563eb; --success: #16a34a; --danger: #dc2626; --light: #f8fafc; --dark: #1e293b; }
        body { background: var(--light); color: var(--dark); }
        .page { display: none; min-height: 100vh; }
        .page.active { display: block; }
        
        /* === هدر === */
        header { background: white; box-shadow: 0 2px 8px rgba(0,0,0,0.08); position: sticky; top: 0; z-index: 100; }
        .nav { max-width: 1200px; margin: 0 auto; padding: 15px 20px; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; }
        .logo { font-size: 24px; font-weight: bold; color: var(--primary); text-decoration: none; }
        .nav-links a { margin-right: 15px; text-decoration: none; color: var(--dark); font-weight: 500; font-size: 15px; }
        .nav-links a:hover { color: var(--primary); }
        .seller-btn { background: var(--primary); color: white !important; padding: 8px 16px; border-radius: 6px; }
        .logout-btn { background: var(--danger); color: white !important; padding: 8px 16px; border-radius: 6px; }
        
        /* === صفحه اصلی === */
        .hero { text-align: center; padding: 50px 20px 30px; }
        .hero h1 { font-size: 32px; margin-bottom: 10px; color: var(--dark); }
        .hero p { font-size: 16px; color: #64748b; }
        .container { max-width: 1200px; margin: 0 auto; padding: 0 20px; }
        h2.section-title { text-align: center; margin: 40px 0 25px; font-size: 24px; color: var(--dark); }
        
        /* فیلتر دسته بندی */
        .filter-bar { display: flex; flex-wrap: wrap; gap: 10px; justify-content: center; margin-bottom: 30px; }
        .filter-btn { padding: 8px 18px; border-radius: 20px; border: none; background: white; color: var(--dark); cursor: pointer; font-size: 14px; box-shadow: 0 1px 3px rgba(0,0,0,0.05); }
        .filter-btn.active { background: var(--primary); color: white; }
        
        /* لیست محصولات */
        .products-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(260px, 1fr)); gap: 25px; }
        .product-card { background: white; border-radius: 12px; overflow: hidden; box-shadow: 0 2px 8px rgba(0,0,0,0.05); transition: transform 0.2s; }
        .product-card:hover { transform: translateY(-4px); }
        .product-img { width: 100%; height: 200px; background: #e2e8f0; display: flex; align-items: center; justify-content: center; overflow: hidden; }
        .product-img img { width: 100%; height: 100%; object-fit: cover; }
        .product-info { padding: 15px; }
        .product-name { font-size: 16px; font-weight: 600; margin-bottom: 6px; color: var(--dark); }
        .product-desc { font-size: 13px; color: #64748b; margin-bottom: 12px; }
        .product-price { display: flex; align-items: center; justify-content: space-between; }
        .price { font-size: 17px; font-weight: bold; color: var(--success); }
        .price.discounted { color: var(--danger); }
        .old-price { font-size: 13px; color: #94a3b8; text-decoration: line-through; margin-left: 6px; }
        .view-btn { background: var(--primary); color: white; border: none; padding: 7px 14px; border-radius: 6px; font-size: 14px; cursor: pointer; }
        
        footer { background: var(--dark); color: white; text-align: center; padding: 30px; margin-top: 60px; }
        
        /* === فرم‌ها === */
        .form-wrapper { min-height: 100vh; display: flex; align-items: center; justify-content: center; padding: 30px 20px; background: linear-gradient(135deg, #dbeafe 0%, #eff6ff 100%); }
        .form-box { background: white; padding: 30px; border-radius: 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.08); width: 100%; max-width: 480px; }
        .form-box h2 { text-align: center; color: var(--primary); margin-bottom: 25px; }
        input, textarea, select { width: 100%; padding: 12px; margin-bottom: 15px; border: 1px solid #e2e8f0; border-radius: 8px; font-size: 15px; }
        input:focus, textarea:focus, select:focus { outline: none; border-color: var(--primary); }
        button { padding: 12px 20px; border: none; border-radius: 8px; font-size: 16px; cursor: pointer; font-weight: 500; transition: 0.2s; }
        .btn-primary { background: var(--primary); color: white; width: 100%; }
        .btn-primary:hover { background: #1d4ed8; }
        .link-text { text-align: center; margin-top: 20px; font-size: 14px; color: #64748b; }
        .link-text span { color: var(--primary); cursor: pointer; font-weight: 500; }
        .link-text span:hover { text-decoration: underline; }
        .error-msg { color: var(--danger); text-align: center; margin-bottom: 15px; display: none; }
        
        /* === داشبورد فروشنده === */
        .dashboard-header { background: white; padding: 20px; box-shadow: 0 2px 8px rgba(0,0,0,0.05); display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 15px; }
        .dashboard-header h1 { font-size: 22px; color: var(--primary); }
        .welcome-box { background: #dbeafe; padding: 20px; border-radius: 10px; margin: 30px 20px; max-width: 1200px; margin-left: auto; margin-right: auto; }
        .welcome-box h3 { color: #1e40af; font-size: 17px; margin-bottom: 5px; }
        .grid { max-width: 1200px; margin: 0 auto 40px; padding: 0 20px; display: grid; grid-template-columns: 1fr 1fr; gap: 30px; }
        @media(max-width: 768px) { .grid { grid-template-columns: 1fr; } .nav-links { margin-top: 10px; } }
        .card { background: white; padding: 25px; border-radius: 12px; box-shadow: 0 2px 10px rgba(0,0,0,0.05); }
        .card h3 { color: var(--dark); margin-bottom: 20px; font-size: 18px; }
        .product-item { border-bottom: 1px solid #eee; padding: 15px 0; }
        .product-item h4 { color: var(--dark); margin-bottom: 5px; font-size: 15px; }
        .product-item p { font-size: 13px; color: #64748b; margin-bottom: 3px; }
        .prod-preview-img { width: 60px; height: 60px; border-radius: 6px; object-fit: cover; margin: 5px 8px 5px 0; }
        .del-btn { background: var(--danger); color: white; padding: 6px 12px; font-size: 13px; margin-top: 8px; }
        .del-btn:hover { background: #b91c1c; }
        .empty-state { text-align: center; color: #94a3b8; padding: 40px 20px; }
        .upload-preview { display: flex; flex-wrap: wrap; gap: 8px; margin: 10px 0; }
        .upload-preview img { width: 70px; height: 70px; object-fit: cover; border-radius: 6px; border: 2px solid #ddd; }
    </style>
</head>
<body>

    <!-- ================================== -->
    <!-- صفحه اصلی -->
    <!-- ================================== -->
    <div id="page-home" class="page active">
        <header>
            <div class="nav">
                <span class="logo">آسان خرید</span>
                <div class="nav-links">
                    <a href="#" onclick="showPage('home')">صفحه اصلی</a>
                    <a href="#products">محصولات</a>
                    <a class="seller-btn" href="#" onclick="showPage('login')">فروشنده هستید؟</a>
                </div>
            </div>
        </header>

        <section class="hero">
            <h1>خوش آمدید به آسان خرید</h1>
            <p>بهترین و مطمئن‌ترین بازار خرید و فروش در افغانستان</p>
        </section>

        <div class="container" id="products">
            <h2 class="section-title">محصولات</h2>
            
            <!-- فیلتر دسته‌بندی -->
            <div class="filter-bar">
                <button class="filter-btn active" onclick="filterProducts('all', this)">همه</button>
                <button class="filter-btn" onclick="filterProducts('زنانه', this)">لباس زنانه</button>
                <button class="filter-btn" onclick="filterProducts('مردانه', this)">لباس مردانه</button>
                <button class="filter-btn" onclick="filterProducts('کودک', this)">لباس کودک</button>
                <button class="filter-btn" onclick="filterProducts('برقی', this)">لوازم برقی</button>
                <button class="filter-btn" onclick="filterProducts('خانه', this)">لوازم خانه</button>
                <button class="filter-btn" onclick="filterProducts('تکنالوژی', this)">تکنالوژی</button>
            </div>

            <!-- لیست محصولات -->
            <div class="products-grid" id="productsContainer">
                <div class="empty-state" style="grid-column: 1/-1;">هنوز محصولی موجود نیست.</div>
            </div>
        </div>

        <footer>
            <p>© ۱۴۰۵ آسان خرید — همه حقوق محفوظ است</p>
        </footer>
    </div>

    <!-- ================================== -->
    <!-- صفحه ثبت‌نام فروشنده -->
    <!-- ================================== -->
    <div id="page-register" class="page">
        <div class="form-wrapper">
            <div class="form-box">
                <h2>ثبت‌نام فروشنده</h2>
                <form id="registerForm">
                    <input type="text" id="reg-name" placeholder="نام کامل" required>
                    <input type="tel" id="reg-whatsapp" placeholder="شماره واتساپ (مثال: ۰۷۰۰۱۲۳۴۵۶)" required>
                    <input type="email" id="reg-email" placeholder="آدرس ایمیل" required>
                    <input type="password" id="reg-pass" placeholder="رمز عبور" required>
                    <textarea id="reg-address" placeholder="آدرس کامل فروشگاه" rows="3" required></textarea>
                    <button type="submit" class="btn-primary">ثبت‌نام</button>
                </form>
                <div class="link-text">
                    قبلاً حساب دارید؟ <span onclick="showPage('login')">وارد شوید</span><br>
                    <span onclick="showPage('home')">بازگشت به صفحه اصلی</span>
                </div>
            </div>
        </div>
    </div>

    <!-- ================================== -->
    <!-- صفحه ورود فروشنده -->
    <!-- ================================== -->
    <div id="page-login" class="page">
        <div class="form-wrapper">
            <div class="form-box">
                <h2>ورود فروشنده</h2>
                <div class="error-msg" id="login-error">ایمیل یا رمز عبور اشتباه است!</div>
                <form id="loginForm">
                    <input type="email" id="login-email" placeholder="ایمیل خود را وارد کنید" required>
                    <input type="password" id="login-pass" placeholder="رمز عبور را وارد کنید" required>
                    <button type="submit" class="btn-primary">ورود</button>
                </form>
                <div class="link-text">
                    حساب ندارید؟ <span onclick="showPage('register')">ثبت‌نام کنید</span><br>
                    <span onclick="showPage('home')">بازگشت به صفحه اصلی</span>
                </div>
            </div>
        </div>
    </div>

    <!-- ================================== -->
    <!-- صفحه داشبورد فروشنده -->
    <!-- ================================== -->
    <div id="page-dashboard" class="page">
        <div class="dashboard-header">
            <h1>داشبورد فروشنده</h1>
            <button class="logout-btn" onclick="logout()">خروج از حساب</button>
        </div>

        <div class="welcome-box">
            <h3>سلام، خوش آمدید! 👋</h3>
            <p id="seller-details">لطفاً وارد حساب خود شوید.</p>
        </div>

        <div class="grid">
            <!-- فرم اضافه کردن محصول -->
            <div class="card">
                <h3>➕ اضافه کردن محصول جدید</h3>
                <form id="productForm">
                    <input type="text" id="p-name" placeholder="نام محصول" required>
                    <textarea id="p-desc" placeholder="توضیحات محصول" rows="2" required></textarea>
                    <input type="number" id="p-price" placeholder="قیمت اصلی (افغانی)" required>
                    <input type="number" id="p-discount" placeholder="قیمت تخفیفی (اختیاری)">
                    <select id="p-cat" required>
                        <option value="">انتخاب دسته‌بندی</option>
                        <option value="زنانه">لباس زنانه</option>
                        <option value="مردانه">لباس مردانه</option>
                        <option value="کودک">لباس کودک</option>
                        <option value="برقی">لوازم برقی</option>
                        <option value="خانه">لوازم خانه</option>
                        <option value="تکنالوژی">تکنالوژی</option>
                    </select>
                    
                    <!-- آپلود عکس -->
                    <label style="display:block; margin: 10px 0 5px; font-weight:500;">عکس محصول (حداکثر ۳ عکس):</label>
                    <input type="file" id="p-images" accept="image/*" multiple onchange="previewImages(this)">
                    <div class="upload-preview" id="imgPreviewContainer"></div>
                    
                    <button type="submit" class="btn-primary" style="margin-top: 15px;">ذخیره محصول</button>
                </form>
            </div>

            <!-- لیست محصولات -->
            <div class="card">
                <h3>📦 محصولات شما</h3>
                <div id="product-list">
                    <div class="empty-state">هنوز هیچ محصولی اضافه نکرده‌اید.</div>
                </div>
            </div>
        </div>
    </div>

    <!-- ================================== -->
    <!-- جاوا اسکریپت -->
    <!-- ================================== -->
    <script>
        let currentEmail = null;
        let seller = null;
        let uploadedImages = [];
        let allProducts = [];
        let currentFilter = 'all';

        // تغییر صفحه
        function showPage(pageName) {
            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
            document.getElementById('page-' + pageName).classList.add('active');
            
            if (pageName === 'dashboard') checkAuth();
            if (pageName === 'home') loadAllProducts();
            if (pageName !== 'login') document.getElementById('login-error').style.display = 'none';
        }

        // بررسی ورود
        function checkAuth() {
            currentEmail = localStorage.getItem('currentSeller');
            if (!currentEmail || !localStorage.getItem('seller_' + currentEmail)) {
                alert('⚠️ لطفاً ابتدا وارد حساب خود شوید!');
                showPage('login');
                return false;
            }
            seller = JSON.parse(localStorage.getItem('seller_' + currentEmail));
            document.getElementById('seller-details').innerHTML = 
                '<strong>نام:</strong> ' + seller.name + ' | <strong>ایمیل:</strong> ' + seller.email + ' | <strong>واتساپ:</strong> ' + seller.whatsapp;
            renderSellerProducts();
            return true;
        }

        // پیش‌نمایش عکس‌های انتخاب شده
        function previewImages(input) {
            uploadedImages = [];
            const container = document.getElementById('imgPreviewContainer');
            container.innerHTML = '';
            
            if (input.files.length > 3) {
                alert('⚠️ حداکثر ۳ عکس می‌توانید انتخاب کنید!');
                input.value = '';
                return;
            }
            
            for (let i = 0; i < input.files.length; i++) {
                const file = input.files[i];
                const reader = new FileReader();
                reader.onload = function(e) {
                    uploadedImages.push(e.target.result);
                    container.innerHTML += `<img src="${e.target.result}" alt="preview">`;
                };
                reader.readAsDataURL(file);
            }
        }

        // ثبت‌نام
        document.getElementById('registerForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const email = document.getElementById('reg-email').value;
            
            if (localStorage.getItem('seller_' + email)) {
                alert('❌ این ایمیل قبلاً ثبت شده است!');
                return;
            }

            seller = {
                name: document.getElementById('reg-name').value,
                whatsapp: document.getElementById('reg-whatsapp').value,
                email: email,
                password: document.getElementById('reg-pass').value,
                address: document.getElementById('reg-address').value,
                products: []
            };

            localStorage.setItem('seller_' + email, JSON.stringify(seller));
            localStorage.setItem('currentSeller', email);
            alert('✅ ثبت‌نام موفق! خوش آمدید ' + seller.name);
            showPage('dashboard');
            this.reset();
        });

        // ورود
        document.getElementById('loginForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const email = document.getElementById('login-email').value;
            const pass = document.getElementById('login-pass').value;
            const stored = localStorage.getItem('seller_' + email);
            
            if (stored) {
                const data = JSON.parse(stored);
                if (data.password === pass) {
                    localStorage.setItem('currentSeller', email);
                    showPage('dashboard');
                    document.getElementById('login-error').style.display = 'none';
                    this.reset();
                } else {
                    document.getElementById('login-error').style.display = 'block';
                }
            } else {
                document.getElementById('login-error').style.display = 'block';
            }
        });

        // اضافه کردن محصول
        document.getElementById('productForm').addEventListener('submit', function(e) {
            e.preventDefault();
            if (!checkAuth()) return;

            const product = {
                id: Date.now(),
                sellerEmail: currentEmail,
                name: document.getElementById('p-name').value,
                desc: document.getElementById('p-desc').value,
                price: document.getElementById('p-price').value,
                discount: document.getElementById('p-discount').value || null,
                category: document.getElementById('p-cat').value,
                images: [...uploadedImages],
                date: new Date().toLocaleDateString('fa-AF')
            };

            seller.products.unshift(product);
            localStorage.setItem('seller_' + currentEmail, JSON.stringify(seller));
            
            alert('✅ محصول با موفقیت اضافه شد!');
            this.reset();
            uploadedImages = [];
            document.getElementById('imgPreviewContainer').innerHTML = '';
            renderSellerProducts();
        });

        // نمایش محصولات فروشنده در داشبورد
        function renderSellerProducts() {
            const list = document.getElementById('product-list');
            if (!seller.products.length) {
                list.innerHTML = '<div class="empty-state">هنوز هیچ محصولی اضافه نکرده‌اید.</div>';
                return;
            }

            list.innerHTML = '';
            seller.products.forEach(prod => {
                let imgsHtml = '';
                if (prod.images && prod.images.length > 0) {
                    prod.images.forEach(src => {
                        imgsHtml += `<img src="${src}" class="prod-preview-img" alt="product">`;
                    });
                }
                list.innerHTML += `
                    <div class="product-item">
                        <h4>${prod.name}</h4>
                        <p>${prod.category} • ${prod.date}</p>
                        <p>${prod.desc}</p>
                        <p style="font-weight: bold; color: var(--success);">قیمت: ${prod.price} افغانی ${prod.discount ? '<span style="color:var(--danger)"> | تخفیف: ' + prod.discount + ' افغانی</span>' : ''}</p>
                        <div>${imgsHtml}</div>
                        <button class="del-btn" onclick="deleteProduct(${prod.id})">حذف محصول</button>
                    </div>
                `;
            });
        }

        // بارگذاری همه محصولات در صفحه اصلی
        function loadAllProducts() {
            allProducts = [];
            for (let key in localStorage) {
                if (key.startsWith('seller_')) {
                    const sellerData = JSON.parse(localStorage[key]);
                    if (sellerData.products && sellerData.products.length > 0) {
                        allProducts = allProducts.concat(sellerData.products);
                    }
                }
            }
            renderFilteredProducts();
        }

        // فیلتر محصولات
        function filterProducts(category, btn) {
            currentFilter = category;
            document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
            btn.classList.add('active');
            renderFilteredProducts();
        }

        function renderFilteredProducts() {
            const container = document.getElementById('productsContainer');
            let filtered = currentFilter === 'all' ? allProducts : allProducts.filter(p => p.category === currentFilter);
            
            if (!filtered.length) {
                container.innerHTML = '<div class="empty-state" style="grid-column: 1/-1;">محصولی در این دسته‌بندی موجود نیست.</div>';
                return;
            }

            container.innerHTML = '';
            filtered.forEach(prod => {
                const imgSrc = (prod.images && prod.images.length > 0) ? prod.images[0] : '';
                const priceDisplay = prod.discount 
                    ? `<span class="price discounted">${prod.discount} افغانی</span> <span class="old-price">${prod.price} افغانی</span>`
                    : `<span class="price">${prod.price} افغانی</span>`;

                container.innerHTML += `
                    <div class="product-card">
                        <div class="product-img">
                            ${imgSrc ? `<img src="${imgSrc}" alt="${prod.name}">` : '<span style="font-size:40px; color:#aaa;">📦</span>'}
                        </div>
                        <div class="product-info">
                            <div class="product-name">${prod.name}</div>
                            <div class="product-desc">${prod.desc}</div>
                            <div class="product-price">
                                ${priceDisplay}
                                <button class="view-btn">مشاهده</button>
                            </div>
                        </div>
                    </div>
                `;
            });
        }

        // حذف محصول
        window.deleteProduct = function(id) {
            if (confirm('آیا مطمئن هستید که این محصول را حذف کنید؟')) {
                seller.products = seller.products.filter(p => p.id !== id);
                localStorage.setItem('seller_' + currentEmail, JSON.stringify(seller));
                renderSellerProducts();
            }
        };

        // خروج
        window.logout = function() {
            localStorage.removeItem('currentSeller');
            showPage('home');
            alert('✅ از حساب خود خارج شدید.');
        };

        // بارگذاری محصولات هنگام باز شدن صفحه اصلی
        document.addEventListener('DOMContentLoaded', function() {
            loadAllProducts();
        });
    </script>
</body>
</html>
