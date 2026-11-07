<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أناقة | Anaqa Store</title>
    <!-- استدعاء خطوط جوجل الفاخرة -->
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&family=Playfair+Display:ital,wght@1,600&display=swap" rel="stylesheet">
    <style>
        /* === إعدادات عامة === */
        :root {
            --bg-color: #0f0f0f;       /* أسود فاخر */
            --card-bg: #1a1a1a;        /* رمادي داكن للبطاقات */
            --gold: #d4af37;           /* لون ذهبي */
            --text-main: #f5f5f5;      /* أبيض مائل للرمادي */
            --text-muted: #a3a3a3;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Cairo', sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            overflow-x: hidden;
        }

        /* === شريط التنقل === */
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 5%;
            background-color: rgba(15, 15, 15, 0.95);
            position: sticky;
            top: 0;
            z-index: 100;
            border-bottom: 1px solid #333;
        }

        .logo {
            font-family: 'Playfair Display', serif;
            font-size: 2rem;
            color: var(--gold);
            font-weight: bold;
            letter-spacing: 2px;
        }

        .cart-icon {
            position: relative;
            cursor: pointer;
            font-size: 1.5rem;
        }

        .cart-count {
            position: absolute;
            top: -8px;
            right: -12px;
            background-color: var(--gold);
            color: #000;
            font-size: 0.8rem;
            font-weight: bold;
            padding: 2px 6px;
            border-radius: 50%;
        }

        /* === القسم الرئيسي (Hero) === */
        .hero {
            height: 60vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.9)), url('https://images.unsplash.com/photo-1490481651871-ab68de25d43d?q=80&w=2070&auto=format&fit=crop') center/cover;
            padding: 20px;
        }

        .hero h1 {
            font-size: 3rem;
            margin-bottom: 15px;
            color: var(--gold);
        }

        .hero p {
            font-size: 1.2rem;
            color: var(--text-main);
            max-width: 600px;
        }

        /* === شبكة المنتجات === */
        .products-section {
            padding: 60px 5%;
        }

        .section-title {
            text-align: center;
            font-size: 2rem;
            margin-bottom: 40px;
            position: relative;
            display: inline-block;
            left: 50%;
            transform: translateX(-50%);
        }
        .section-title::after {
            content: '';
            width: 50%;
            height: 2px;
            background-color: var(--gold);
            position: absolute;
            bottom: -10px;
            left: 25%;
        }

        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 30px;
        }

        /* === بطاقة المنتج === */
        .product-card {
            background-color: var(--card-bg);
            border-radius: 10px;
            overflow: hidden;
            transition: transform 0.3s, box-shadow 0.3s;
            border: 1px solid #333;
            display: flex;
            flex-direction: column;
        }

        .product-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(212, 175, 55, 0.1);
            border-color: var(--gold);
        }

        .product-img {
            width: 100%;
            height: 250px;
            object-fit: cover;
        }

        .product-info {
            padding: 20px;
            text-align: center;
            display: flex;
            flex-direction: column;
            flex-grow: 1;
        }

        .product-title {
            font-size: 1.2rem;
            margin-bottom: 10px;
        }

        .product-price {
            color: var(--gold);
            font-size: 1.3rem;
            font-weight: bold;
            margin-bottom: 20px;
        }

        .add-to-cart {
            background-color: transparent;
            color: var(--gold);
            border: 1px solid var(--gold);
            padding: 10px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            font-family: 'Cairo', sans-serif;
            transition: all 0.3s;
            margin-top: auto;
        }

        .add-to-cart:hover {
            background-color: var(--gold);
            color: #000;
        }

        /* === سلة المشتريات الجانبية === */
        .cart-sidebar {
            position: fixed;
            top: 0;
            left: -400px; /* مخفية في البداية (يسار لأن الموقع RTL) */
            width: 350px;
            height: 100vh;
            background-color: var(--card-bg);
            box-shadow: 5px 0 15px rgba(0,0,0,0.5);
            transition: left 0.3s ease;
            z-index: 1000;
            display: flex;
            flex-direction: column;
            border-right: 1px solid #333;
        }

        .cart-sidebar.active {
            left: 0;
        }

        .cart-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px;
            border-bottom: 1px solid #333;
        }

        .close-cart {
            cursor: pointer;
            font-size: 1.5rem;
            color: var(--text-muted);
        }

        .cart-items {
            flex-grow: 1;
            overflow-y: auto;
            padding: 20px;
        }

        .cart-item {
            display: flex;
            align-items: center;
            margin-bottom: 20px;
            border-bottom: 1px solid #333;
            padding-bottom: 10px;
        }

        .cart-item img {
            width: 60px;
            height: 60px;
            object-fit: cover;
            border-radius: 5px;
            margin-left: 15px;
        }

        .cart-item-info {
            flex-grow: 1;
        }

        .cart-item-info h4 { margin-bottom: 5px; font-size: 1rem; }
        .cart-item-info p { color: var(--gold); font-size: 0.9rem; }

        .remove-item {
            background: none;
            border: none;
            color: #ff4d4d;
            cursor: pointer;
            font-size: 1.2rem;
        }

        .cart-footer {
            padding: 20px;
            border-top: 1px solid #333;
            background-color: #111;
        }

        .total-price {
            display: flex;
            justify-content: space-between;
            font-size: 1.2rem;
            font-weight: bold;
            margin-bottom: 15px;
        }

        .checkout-btn {
            width: 100%;
            padding: 15px;
            background-color: var(--gold);
            color: #000;
            border: none;
            border-radius: 5px;
            font-size: 1.1rem;
            font-weight: bold;
            font-family: 'Cairo', sans-serif;
            cursor: pointer;
            transition: opacity 0.3s;
        }

        .checkout-btn:hover { opacity: 0.8; }

        /* خلفية داكنة عند فتح السلة */
        .overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: rgba(0,0,0,0.7);
            z-index: 999;
            display: none;
        }
        .overlay.active { display: block; }

        /* === التذييل === */
        footer {
            text-align: center;
            padding: 30px;
            background-color: #111;
            color: var(--text-muted);
            border-top: 1px solid #333;
            margin-top: 50px;
        }

        /* === التجاوب مع الجوال === */
        @media (max-width: 768px) {
            .hero h1 { font-size: 2rem; }
            .cart-sidebar { width: 100%; left: -100%; }
            .products-grid { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>

    <!-- شريط التنقل -->
    <header>
        <div class="logo">أناقة | ANAQA</div>
        <div class="cart-icon" onclick="toggleCart()">
            🛒 <span class="cart-count" id="cartCount">0</span>
        </div>
    </header>

    <!-- القسم الرئيسي -->
    <section class="hero">
        <h1>اكتشف عالم الأناقة</h1>
        <p>تشكيلة حصرية من الملحقات والقطع الفاخرة التي تبرز جمالك وتفردك.</p>
    </section>

    <!-- قسم المنتجات -->
    <section class="products-section">
        <h2 class="section-title">أحدث القطع</h2>
        <div class="products-grid" id="productsGrid">
            <!-- سيتم إدراج المنتجات هنا عبر الجافا سكريبت -->
        </div>
    </section>

    <!-- سلة المشتريات الجانبية -->
    <div class="overlay" id="overlay" onclick="toggleCart()"></div>
    <div class="cart-sidebar" id="cartSidebar">
        <div class="cart-header">
            <h2>حقيبة التسوق</h2>
            <span class="close-cart" onclick="toggleCart()">×</span>
        </div>
        <div class="cart-items" id="cartItemsContainer">
            <!-- سيتم إدراج المنتجات المضافة هنا -->
            <p style="text-align:center; color:#888; margin-top:20px;">السلة فارغة حالياً</p>
        </div>
        <div class="cart-footer">
            <div class="total-price">
                <span>الإجمالي:</span>
                <span id="totalPrice">0 د.ج</span>
            </div>
            <button class="checkout-btn" onclick="checkout()">إتمام الطلب</button>
        </div>
    </div>

    <!-- التذييل -->
    <footer>
        <p>جميع الحقوق محفوظة &copy; 2026 - متجر أناقة</p>
    </footer>

    <!-- كود الجافا سكريبت -->
    <script>
        // 1. قاعدة بيانات المنتجات (يمكنك تعديلها وإضافة منتجاتك الخاصة)
        const products = [
            {
                id: 1,
                name: "ساعة يد كلاسيكية",
                price: 15000,
                image: "https://images.unsplash.com/photo-1523275335684-37898b6baf30?q=80&w=800&auto=format&fit=crop"
            },
            {
                id: 2,
                name: "عطر شرقي فاخر",
                price: 8500,
                image: "https://images.unsplash.com/photo-1594035910387-fea47794261f?q=80&w=800&auto=format&fit=crop"
            },
            {
                id: 3,
                name: "حقيبة جلدية أنيقة",
                price: 12000,
                image: "https://images.unsplash.com/photo-1584916201218-f4242ceb4809?q=80&w=800&auto=format&fit=crop"
            },
            {
                id: 4,
                name: "نظارات شمسية عصرية",
                price: 4500,
                image: "https://images.unsplash.com/photo-1511499767150-a48a237f0083?q=80&w=800&auto=format&fit=crop"
            }
        ];

        let cart = []; // مصفوفة لحفظ المنتجات التي تمت إضافتها

        // 2. عرض المنتجات في الصفحة
        const productsGrid = document.getElementById('productsGrid');
        
        function renderProducts() {
            productsGrid.innerHTML = products.map(product => `
                <div class="product-card">
                    <img src="${product.image}" alt="${product.name}" class="product-img">
                    <div class="product-info">
                        <h3 class="product-title">${product.name}</h3>
                        <p class="product-price">${product.price.toLocaleString()} د.ج</p>
                        <button class="add-to-cart" onclick="addToCart(${product.id})">أضف للسلة</button>
                    </div>
                </div>
            `).join('');
        }

        // 3. وظيفة إضافة منتج للسلة
        function addToCart(id) {
            const product = products.find(p => p.id === id);
            const existingItem = cart.find(item => item.id === id);

            if (existingItem) {
                existingItem.quantity += 1;
            } else {
                cart.push({ ...product, quantity: 1 });
            }
            
            updateCartUI();
            // تأثير بسيط لفتح السلة عند الإضافة
            document.getElementById('cartSidebar').classList.add('active');
            document.getElementById('overlay').classList.add('active');
        }

        // 4. وظيفة حذف منتج من السلة
        function removeFromCart(id) {
            cart = cart.filter(item => item.id !== id);
            updateCartUI();
        }

        // 5. تحديث واجهة السلة (المنتجات، الإجمالي، العداد)
        function updateCartUI() {
            const cartCount = document.getElementById('cartCount');
            const cartItemsContainer = document.getElementById('cartItemsContainer');
            const totalPriceElement = document.getElementById('totalPrice');

            // تحديث العداد
            const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
            cartCount.innerText = totalItems;

            // تحديث الإجمالي
            const totalPrice = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            totalPriceElement.innerText = totalPrice.toLocaleString() + ' د.ج';

            // تحديث قائمة المنتجات داخل السلة
            if (cart.length === 0) {
                cartItemsContainer.innerHTML = '<p style="text-align:center; color:#888; margin-top:20px;">السلة فارغة حالياً</p>';
            } else {
                cartItemsContainer.innerHTML = cart.map(item => `
                    <div class="cart-item">
                        <img src="${item.image}" alt="${item.name}">
                        <div class="cart-item-info">
                            <h4>${item.name} (x${item.quantity})</h4>
                            <p>${(item.price * item.quantity).toLocaleString()} د.ج</p>
                        </div>
                        <button class="remove-item" onclick="removeFromCart(${item.id})">×</button>
                    </div>
                `).join('');
            }
        }

        // 6. فتح وإغلاق السلة
        function toggleCart() {
            const sidebar = document.getElementById('cartSidebar');
            const overlay = document.getElementById('overlay');
            sidebar.classList.toggle('active');
            overlay.classList.toggle('active');
        }

        // 7. إتمام الطلب (وهمي)
        function checkout() {
            if (cart.length === 0) {
                alert('سلة المشتريات فارغة! أضف بعض المنتجات أولاً.');
                return;
            }
            alert('شكراً لتسوقك معنا! تم استلام طلبك بنجاح وسيتم التواصل معك قريباً.');
            cart = [];
            updateCartUI();
            toggleCart();
        }

        // تشغيل عرض المنتجات عند تحميل الصفحة
        renderProducts();
    </script>
</body>
</html>
