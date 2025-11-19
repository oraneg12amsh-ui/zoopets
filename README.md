<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ZOOTPETS | Tu Mundo Animal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800&display=swap');
        body { font-family: 'Outfit', sans-serif; }
        
        /* Nuevo Gradiente Naranja/Ámbar para ZOOTPETS */
        .gradient-bg { background: linear-gradient(135deg, #f59e0b 0%, #ea580c 100%); }
        
        .card-hover { transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1); }
        .card-hover:hover { transform: translateY(-5px); box-shadow: 0 15px 30px -5px rgba(0, 0, 0, 0.1); }
        
        .modal { display: none; position: fixed; z-index: 1000; left: 0; top: 0; width: 100%; height: 100%; background-color: rgba(0,0,0,0.5); backdrop-filter: blur(4px); }
        .modal.show { display: flex; align-items: center; justify-content: center; animation: fadeIn 0.2s ease-out; }
        
        .cart-sidebar { transform: translateX(100%); transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1); }
        .cart-open .cart-sidebar { transform: translateX(0); }
        .cart-open .cart-overlay { opacity: 1; pointer-events: auto; }
        .cart-overlay { transition: opacity 0.3s ease; opacity: 0; pointer-events: none; }

        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        @keyframes slideUp { from { transform: translateY(20px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
        
        /* Loader Personalizado */
        #loader { position: fixed; inset: 0; background: white; z-index: 9999; display: flex; flex-direction: column; align-items: center; justify-content: center; transition: opacity 0.5s; }
    </style>
</head>
<body class="bg-orange-50 flex flex-col min-h-screen">

    <!-- Loader de Carga -->
    <div id="loader">
        <div class="animate-spin rounded-full h-16 w-16 border-t-4 border-orange-600 mb-4"></div>
        <h2 class="text-2xl font-extrabold text-gray-800 tracking-widest">ZOOTPETS</h2>
        <p class="text-orange-500 text-sm font-medium">Cargando el mundo de tu mascota...</p>
    </div>

    <!-- Header -->
    <header class="gradient-bg text-white shadow-xl sticky top-0 z-40 bg-opacity-95 backdrop-blur">
        <div class="container mx-auto px-4 py-3">
            <div class="flex justify-between items-center">
                <div class="flex items-center space-x-2 group cursor-pointer" onclick="window.scrollToSection('hero')">
                    <div class="w-10 h-10 bg-white text-orange-600 rounded-full flex items-center justify-center shadow-md group-hover:rotate-12 transition-transform">
                        <span class="text-2xl">🦊</span>
                    </div>
                    <h1 class="text-2xl font-extrabold tracking-tighter">ZOOTPETS</h1>
                </div>
                
                <nav class="hidden md:flex space-x-8 font-semibold text-sm uppercase tracking-wide">
                    <a href="#productos" onclick="window.scrollToSection('productos')" class="hover:text-yellow-200 transition-colors">Tienda</a>
                    <a href="#citas" onclick="window.scrollToSection('citas')" class="hover:text-yellow-200 transition-colors">Clínica</a>
                    <a href="#seguimiento" onclick="window.scrollToSection('seguimiento')" class="hover:text-yellow-200 transition-colors">Rastreo</a>
                    <a href="#admin" onclick="window.scrollToSection('admin')" class="hover:text-yellow-200 transition-colors">Staff</a>
                </nav>

                <div class="flex items-center space-x-4">
                    <button onclick="window.toggleCart()" class="relative p-2 hover:bg-white hover:bg-opacity-20 rounded-full transition-all group">
                        <span class="text-xl group-hover:scale-110 inline-block">🛒</span>
                        <span id="cart-count" class="absolute -top-1 -right-1 bg-white text-orange-600 text-xs font-bold rounded-full w-5 h-5 flex items-center justify-center shadow-sm">0</span>
                    </button>
                    <button onclick="window.toggleMobileMenu()" class="md:hidden p-2 hover:bg-white hover:bg-opacity-20 rounded-lg">
                        <span class="text-xl">☰</span>
                    </button>
                </div>
            </div>
            
            <div id="mobile-menu" class="md:hidden hidden mt-4 pb-2 border-t border-white/20 pt-2 animate-[fadeIn_0.3s_ease]">
                <a href="#productos" onclick="window.scrollToSection('productos'); window.toggleMobileMenu();" class="block py-3 px-2 hover:bg-white/10 rounded font-bold">Tienda</a>
                <a href="#citas" onclick="window.scrollToSection('citas'); window.toggleMobileMenu();" class="block py-3 px-2 hover:bg-white/10 rounded font-bold">Clínica</a>
                <a href="#admin" onclick="window.scrollToSection('admin'); window.toggleMobileMenu();" class="block py-3 px-2 hover:bg-white/10 rounded font-bold">Acceso Staff</a>
            </div>
        </div>
    </header>

    <!-- Hero Section -->
    <section id="hero" class="relative bg-gray-900 text-white py-24 overflow-hidden">
        <!-- Imagen de fondo diferente para Zootpets -->
        <div class="absolute inset-0 opacity-40 bg-[url('https://images.unsplash.com/photo-1583337130417-3346a1be7dee?ixlib=rb-4.0.3&auto=format&fit=crop&w=1920&q=80')] bg-cover bg-center"></div>
        <div class="absolute inset-0 bg-gradient-to-r from-orange-600/80 to-red-600/60"></div>
        
        <div class="container mx-auto px-4 text-center relative z-10">
            <div class="inline-block bg-white text-orange-600 px-4 py-1 rounded-full text-sm font-bold mb-6 animate-[slideUp_0.4s_ease-out]">NUEVA APERTURA</div>
            <h2 class="text-5xl md:text-7xl font-extrabold mb-6 leading-tight animate-[slideUp_0.6s_ease-out]">Felicidad para<br>tu mascota</h2>
            <p class="text-xl text-orange-50 mb-10 max-w-2xl mx-auto animate-[slideUp_0.8s_ease-out]">En ZOOTPETS combinamos la mejor tecnología veterinaria con los productos más divertidos.</p>
            <div class="flex flex-col sm:flex-row gap-4 justify-center animate-[slideUp_1s_ease-out]">
                <button onclick="window.scrollToSection('productos')" class="bg-white text-orange-600 px-8 py-4 rounded-full font-extrabold hover:bg-yellow-300 hover:text-orange-800 transition-all shadow-xl transform hover:scale-105">VER TIENDA</button>
                <button onclick="window.scrollToSection('citas')" class="bg-transparent border-2 border-white text-white px-8 py-4 rounded-full font-extrabold hover:bg-white hover:text-orange-600 transition-all">AGENDAR CITA</button>
            </div>
        </div>
    </section>

    <!-- Productos Section -->
    <section id="productos" class="py-20 bg-white">
        <div class="container mx-auto px-4">
            <div class="text-center mb-12">
                <span class="text-orange-600 font-bold tracking-wider uppercase text-sm">Catálogo</span>
                <h2 class="text-4xl font-extrabold text-gray-900 mb-4">Favoritos de Zootpets</h2>
                <div class="w-24 h-1.5 bg-orange-500 mx-auto rounded-full"></div>
            </div>

            <div class="flex flex-col md:flex-row justify-between items-center gap-4 mb-8 bg-orange-50 p-4 rounded-2xl shadow-inner border border-orange-100">
                <div class="flex flex-wrap justify-center gap-2">
                    <button onclick="window.filterProducts('todos', this)" class="filter-btn bg-orange-600 text-white px-5 py-2 rounded-full text-sm font-bold transition-all shadow-md">Todo</button>
                    <button onclick="window.filterProducts('alimento', this)" class="filter-btn bg-white text-gray-600 hover:bg-orange-100 px-5 py-2 rounded-full text-sm font-bold transition-all border">Alimento</button>
                    <button onclick="window.filterProducts('juguetes', this)" class="filter-btn bg-white text-gray-600 hover:bg-orange-100 px-5 py-2 rounded-full text-sm font-bold transition-all border">Juguetes</button>
                    <button onclick="window.filterProducts('medicamentos', this)" class="filter-btn bg-white text-gray-600 hover:bg-orange-100 px-5 py-2 rounded-full text-sm font-bold transition-all border">Salud</button>
                    <button onclick="window.filterProducts('accesorios', this)" class="filter-btn bg-white text-gray-600 hover:bg-orange-100 px-5 py-2 rounded-full text-sm font-bold transition-all border">Accesorios</button>
                </div>
                <div class="relative w-full md:w-auto">
                    <input type="text" id="search-product" oninput="window.searchProducts()" placeholder="¿Qué busca tu amigo?" class="w-full md:w-64 pl-10 pr-4 py-2 rounded-full border border-gray-300 focus:ring-2 focus:ring-orange-500 outline-none">
                    <span class="absolute left-3 top-2.5 text-gray-400">🔍</span>
                </div>
            </div>

            <div id="products-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8"></div>
        </div>
    </section>

    <!-- Citas Section -->
    <section id="citas" class="py-20 bg-orange-50">
        <div class="container mx-auto px-4">
            <div class="max-w-5xl mx-auto bg-white rounded-[2rem] shadow-2xl overflow-hidden flex flex-col md:flex-row">
                <div class="md:w-2/5 bg-gradient-to-br from-orange-500 to-red-600 p-10 text-white flex flex-col justify-center relative overflow-hidden">
                    <div class="relative z-10">
                        <span class="text-orange-200 font-bold tracking-wider uppercase text-sm">Veterinaria</span>
                        <h3 class="text-3xl font-extrabold mb-6">Agenda tu visita</h3>
                        <p class="mb-8 text-orange-50 text-lg leading-relaxed">Nuestros expertos en ZOOTPETS están listos para dar el mejor trato a tu compañero.</p>
                        <div class="space-y-4 font-medium">
                            <div class="flex items-center gap-3"><span class="bg-white text-orange-600 rounded-full w-8 h-8 flex items-center justify-center">✓</span> Check-up General</div>
                            <div class="flex items-center gap-3"><span class="bg-white text-orange-600 rounded-full w-8 h-8 flex items-center justify-center">✓</span> Vacunación</div>
                            <div class="flex items-center gap-3"><span class="bg-white text-orange-600 rounded-full w-8 h-8 flex items-center justify-center">✓</span> Spa & Estética</div>
                        </div>
                    </div>
                    <!-- Decorative Circle -->
                    <div class="absolute -bottom-20 -right-20 w-64 h-64 bg-white opacity-10 rounded-full"></div>
                </div>
                
                <div class="md:w-3/5 p-10">
                    <form id="appointment-form" class="space-y-5">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-5">
                            <div>
                                <label class="text-xs font-bold text-gray-500 uppercase ml-1">Dueño</label>
                                <input type="text" id="owner-name" placeholder="Tu nombre" required class="input-field w-full px-4 py-3 bg-gray-50 border border-gray-200 rounded-xl focus:border-orange-500 focus:ring-1 focus:ring-orange-500 outline-none transition-all">
                            </div>
                            <div>
                                <label class="text-xs font-bold text-gray-500 uppercase ml-1">Teléfono</label>
                                <input type="tel" id="owner-phone" placeholder="Whatsapp" required class="input-field w-full px-4 py-3 bg-gray-50 border border-gray-200 rounded-xl focus:border-orange-500 focus:ring-1 focus:ring-orange-500 outline-none transition-all">
                            </div>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-5">
                            <div>
                                <label class="text-xs font-bold text-gray-500 uppercase ml-1">Mascota</label>
                                <input type="text" id="pet-name" placeholder="Nombre de mascota" required class="input-field w-full px-4 py-3 bg-gray-50 border border-gray-200 rounded-xl focus:border-orange-500 focus:ring-1 focus:ring-orange-500 outline-none transition-all">
                            </div>
                            <div>
                                <label class="text-xs font-bold text-gray-500 uppercase ml-1">Especie</label>
                                <select id="pet-type" required class="input-field w-full px-4 py-3 bg-gray-50 border border-gray-200 rounded-xl focus:border-orange-500 outline-none">
                                    <option value="Perro">Perro 🐶</option>
                                    <option value="Gato">Gato 🐱</option>
                                    <option value="Exótico">Exótico 🦎</option>
                                    <option value="Otro">Otro</option>
                                </select>
                            </div>
                        </div>
                        
                        <div>
                            <label class="text-xs font-bold text-gray-500 uppercase ml-1">Servicio</label>
                            <select id="appointment-reason" onchange="window.handleReasonChange()" required class="input-field w-full px-4 py-3 bg-gray-50 border border-gray-200 rounded-xl focus:border-orange-500 outline-none">
                                <option value="Consulta General - $300">Consulta General - $300</option>
                                <option value="Vacunación - $400">Vacunación - $400</option>
                                <option value="Estética Completa - $250">Estética Completa - $250</option>
                                <option value="Urgencia - $500">Urgencia - $500</option>
                                <option value="Domicilio - $450">Visita a Domicilio - $450</option>
                            </select>
                        </div>

                        <div id="address-container" class="hidden animate-[fadeIn_0.3s_ease]">
                            <label class="text-xs font-bold text-gray-500 uppercase ml-1">Dirección</label>
                            <textarea id="appointment-address" class="w-full px-4 py-3 bg-gray-50 border border-gray-200 rounded-xl focus:border-orange-500 outline-none" placeholder="Calle, Número, Colonia..."></textarea>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-2 gap-5">
                            <div>
                                <label class="text-xs font-bold text-gray-500 uppercase ml-1">Fecha</label>
                                <input type="date" id="appointment-date" required class="input-field w-full px-4 py-3 bg-gray-50 border border-gray-200 rounded-xl focus:border-orange-500 outline-none">
                            </div>
                            <div>
                                <label class="text-xs font-bold text-gray-500 uppercase ml-1">Hora</label>
                                <select id="appointment-time" required class="input-field w-full px-4 py-3 bg-gray-50 border border-gray-200 rounded-xl focus:border-orange-500 outline-none">
                                    <option value="09:00">09:00 AM</option>
                                    <option value="10:00">10:00 AM</option>
                                    <option value="11:00">11:00 AM</option>
                                    <option value="12:00">12:00 PM</option>
                                    <option value="16:00">04:00 PM</option>
                                    <option value="17:00">05:00 PM</option>
                                    <option value="18:00">06:00 PM</option>
                                </select>
                            </div>
                        </div>
                        <button type="submit" class="w-full bg-gray-900 text-white py-4 px-6 rounded-xl font-bold hover:bg-orange-600 transform hover:-translate-y-1 transition-all shadow-lg text-lg">Confirmar Cita</button>
                    </form>
                </div>
            </div>
        </div>
    </section>

    <!-- Seguimiento Section -->
    <section id="seguimiento" class="py-20 bg-white border-t border-gray-100">
        <div class="container mx-auto px-4 text-center">
            <span class="text-orange-600 font-bold uppercase text-sm tracking-widest">Logística</span>
            <h2 class="text-3xl font-extrabold mb-8 text-gray-900">Rastrea tu Pedido ZOOT</h2>
            <div class="max-w-xl mx-auto bg-orange-50 p-2 rounded-2xl border border-orange-100">
                <div class="flex gap-2">
                    <input type="text" id="order-search" placeholder="Ingresa tu ID (Ej: ZOOT999)" class="flex-1 px-6 py-4 border-none bg-white rounded-xl shadow-sm focus:ring-2 focus:ring-orange-400 outline-none text-gray-700">
                    <button onclick="window.searchOrder()" class="bg-orange-600 text-white px-8 py-4 rounded-xl font-bold hover:bg-orange-700 shadow-md transition-colors">Buscar</button>
                </div>
            </div>
            <div id="order-result" class="max-w-xl mx-auto mt-6 bg-white rounded-2xl shadow-xl border border-gray-100 overflow-hidden hidden p-8 animate-[slideUp_0.3s_ease]"></div>
        </div>
    </section>

    <!-- Admin Section -->
    <section id="admin" class="py-20 bg-gray-900 text-gray-100">
        <div class="container mx-auto px-4">
            <div id="admin-login" class="max-w-md mx-auto bg-gray-800 p-10 rounded-3xl shadow-2xl border border-gray-700">
                 <div class="text-center mb-10">
                    <div class="w-16 h-16 bg-gray-700 rounded-2xl flex items-center justify-center mx-auto mb-4 text-3xl">🔐</div>
                    <h3 class="text-2xl font-bold text-white">ZOOTPETS Staff</h3>
                    <p class="text-gray-400 text-sm mt-2">Ingresa tus credenciales administrativas</p>
                </div>
                <form id="admin-login-form" class="space-y-5">
                    <input type="text" id="admin-username" placeholder="Usuario" required class="w-full px-5 py-4 bg-gray-700 border border-gray-600 rounded-xl text-white focus:border-orange-500 outline-none">
                    <input type="password" id="admin-password" placeholder="Contraseña" required class="w-full px-5 py-4 bg-gray-700 border border-gray-600 rounded-xl text-white focus:border-orange-500 outline-none">
                    <button type="submit" class="w-full gradient-bg text-white py-4 rounded-xl font-bold hover:brightness-110 shadow-lg">Entrar al Sistema</button>
                </form>
            </div>

            <div id="admin-panel" class="max-w-7xl mx-auto hidden">
                <div class="bg-gray-800 rounded-2xl shadow-xl p-6 mb-8 flex justify-between items-center border border-gray-700">
                    <div>
                        <h3 class="text-xl font-bold text-white">Panel de Control</h3>
                        <span class="text-xs text-orange-400 font-mono">SYSTEM: ONLINE</span>
                    </div>
                    <button onclick="window.logoutAdmin()" class="text-red-400 font-bold hover:bg-red-400/10 px-4 py-2 rounded-lg transition-colors">Cerrar Sesión</button>
                </div>

                <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-8">
                    <button onclick="window.showAdminTab('productos', this)" class="admin-tab bg-orange-600 text-white p-4 rounded-xl shadow-lg font-bold">📦 Productos</button>
                    <button onclick="window.showAdminTab('envios', this)" class="admin-tab bg-gray-800 text-gray-400 hover:bg-gray-700 p-4 rounded-xl shadow-sm font-medium border border-gray-700">🚚 Pedidos</button>
                    <button onclick="window.showAdminTab('citas', this)" class="admin-tab bg-gray-800 text-gray-400 hover:bg-gray-700 p-4 rounded-xl shadow-sm font-medium border border-gray-700">📅 Agenda</button>
                    <button onclick="window.showAdminTab('seguridad', this)" class="admin-tab bg-gray-800 text-gray-400 hover:bg-gray-700 p-4 rounded-xl shadow-sm font-medium border border-gray-700">🛡️ Config</button>
                </div>

                <div class="bg-white text-gray-800 rounded-2xl shadow-xl border border-gray-200 p-8 min-h-[500px]">
                    <div id="admin-productos" class="admin-content"></div>
                    <div id="admin-envios" class="admin-content hidden"></div>
                    <div id="admin-citas" class="admin-content hidden"></div>
                    <div id="admin-seguridad" class="admin-content hidden"></div>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-900 text-white pt-20 pb-10 mt-auto border-t border-gray-800">
        <div class="container mx-auto px-4 text-center">
            <div class="flex justify-center items-center space-x-2 mb-6">
                <span class="text-3xl">🦊</span>
                <span class="text-2xl font-bold">ZOOTPETS</span>
            </div>
            <p class="text-gray-500 max-w-md mx-auto mb-8">Cuidamos lo que más amas con productos de calidad y atención veterinaria de primera clase.</p>
            <p class="text-gray-600 text-sm">&copy; 2025 ZOOTPETS Inc. Todos los derechos reservados.</p>
        </div>
    </footer>

    <!-- UI Elements -->
    <div id="cart-overlay" class="fixed inset-0 bg-gray-900 bg-opacity-60 z-50 cart-overlay flex justify-end backdrop-blur-sm" onclick="window.toggleCart()">
        <div class="cart-sidebar w-full max-w-md bg-white h-full shadow-2xl flex flex-col" onclick="event.stopPropagation()">
            <div class="p-6 border-b flex justify-between items-center bg-orange-50">
                <h2 class="text-xl font-extrabold text-gray-800 flex items-center gap-2">🛒 Tu Canasta</h2>
                <button onclick="window.toggleCart()" class="w-8 h-8 hover:bg-gray-200 rounded-full flex items-center justify-center font-bold text-gray-500">✕</button>
            </div>
            <div id="cart-items-container" class="flex-1 overflow-y-auto p-6 space-y-4"></div>
            <div id="cart-footer" class="p-6 border-t bg-gray-50"></div>
        </div>
    </div>

    <div id="checkout-modal" class="modal"></div>
    <div id="confirm-modal" class="modal"></div>
    <div id="edit-product-modal" class="modal"></div>

    <!-- FIREBASE MODULE -->
    <script type="module">
        // Import the functions you need from the SDKs you need
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAnalytics } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-analytics.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, doc, addDoc, updateDoc, deleteDoc, onSnapshot, query, orderBy } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // TODO: Add SDKs for Firebase products that you want to use
        // https://firebase.google.com/docs/web/setup#available-libraries

        // Your web app's Firebase configuration
        // For Firebase JS SDK v7.20.0 and later, measurementId is optional
        const firebaseConfig = {
          apiKey: "AIzaSyAR3LsumI0TL0BgzckHV4CYc_VoxMH00rs",
          authDomain: "zoopets-31dec.firebaseapp.com",
          projectId: "zoopets-31dec",
          storageBucket: "zoopets-31dec.firebasestorage.app",
          messagingSenderId: "1038605311322",
          appId: "1:1038605311322:web:c7b560f16741374d4be763",
          measurementId: "G-N19T5XM9BW"
        };

        // Initialize Firebase
        const app = initializeApp(firebaseConfig);
        const analytics = getAnalytics(app); // Analytics inicializado
        const auth = getAuth(app);
        const db = getFirestore(app);
        
        const appId = 'zoopets-production'; 

        // State
        let cart = JSON.parse(localStorage.getItem('zootpetsCart')) || [];
        let currentFilter = 'todos';
        let isAdminLoggedIn = localStorage.getItem('isAdmin') === 'true';
        
        // MODO OFFLINE / LOCAL VARIABLES
        let isOffline = false;
        let products = [];
        let orders = [];
        let appointments = [];

        // Helper para guardar localmente
        const saveLocalData = () => {
            localStorage.setItem('zootpetsProducts', JSON.stringify(products));
            localStorage.setItem('zootpetsOrders', JSON.stringify(orders));
            localStorage.setItem('zootpetsAppointments', JSON.stringify(appointments));
        };

        // Load local data if exists
        const loadLocalData = () => {
            const p = localStorage.getItem('zootpetsProducts');
            const o = localStorage.getItem('zootpetsOrders');
            const a = localStorage.getItem('zootpetsAppointments');
            if(p) products = JSON.parse(p);
            if(o) orders = JSON.parse(o);
            if(a) appointments = JSON.parse(a);
        };

        // --- AUTH & INIT ---
        const initAuth = async () => {
            try {
                await signInAnonymously(auth);
                console.log("ZOOTPETS Cloud: Conectado 🟢");
            } catch (error) {
                console.warn("Firebase Auth falló, cambiando a modo local 🟠", error);
                isOffline = true;
                
                // Eliminar loader manualmente porque Auth falló
                const loader = document.getElementById('loader');
                if(loader) {
                    loader.innerHTML = `<div class="text-center px-4"><h2 class="text-2xl font-bold text-gray-800 mb-2">Modo Local</h2><p class="text-orange-600 mb-4 font-medium">Conectando sin nube...</p></div>`;
                    setTimeout(() => loader.remove(), 1500);
                }
                
                // Cargar datos locales
                loadLocalData();
                
                // Si no hay datos locales, sembrar datos de prueba
                if (products.length === 0) {
                    await seedDataLocal();
                } else {
                    window.renderProducts();
                    window.renderAdminPanel();
                }
                
                window.showNotification("Modo Demo Local Activado", "info");
            }
        };
        
        // Helper para quitar loader en éxito
        const removeLoader = () => {
            const loader = document.getElementById('loader');
            if(loader) {
                loader.style.opacity = '0';
                setTimeout(() => loader.remove(), 500);
            }
        };

        initAuth();

        onAuthStateChanged(auth, (user) => {
            if (user) {
                setupListeners();
            }
        });

        // --- FIRESTORE LISTENERS (REAL-TIME) ---
        const setupListeners = () => {
            const productsRef = collection(db, 'artifacts', appId, 'public', 'data', 'products');
            const ordersRef = collection(db, 'artifacts', appId, 'public', 'data', 'orders');
            const apptsRef = collection(db, 'artifacts', appId, 'public', 'data', 'appointments');

            // Escuchar Productos
            onSnapshot(productsRef, (snapshot) => {
                products = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                window.renderProducts();
                if(isAdminLoggedIn) window.renderAdminProducts();
                removeLoader();
                
                if (products.length === 0 && !localStorage.getItem('zootSeeded')) {
                    seedData();
                }
            }, (error) => {
                console.error("Error productos:", error);
                // Fallback a local si el listener falla
                isOffline = true;
                loadLocalData();
                if(products.length === 0) seedDataLocal();
                window.renderProducts();
                removeLoader();
            });

            onSnapshot(ordersRef, (snapshot) => {
                orders = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                if(isAdminLoggedIn) window.renderAdminOrders();
            });

            onSnapshot(apptsRef, (snapshot) => {
                appointments = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                if(isAdminLoggedIn) window.renderAdminAppointments();
            });
        };

        // --- DATA OPERATIONS (HYBRID CLOUD/LOCAL) ---
        
        window.addProductToDB = async (productData) => {
            if (isOffline) {
                const newProd = { id: 'loc_'+Date.now(), ...productData };
                products.push(newProd);
                saveLocalData();
                window.renderProducts();
                if(isAdminLoggedIn) window.renderAdminProducts();
                window.showNotification("Guardado en Demo (Local)", "success");
                return;
            }
            try {
                if(!auth.currentUser) return;
                await addDoc(collection(db, 'artifacts', appId, 'public', 'data', 'products'), productData);
                window.showNotification("Producto añadido a la nube", "success");
            } catch (e) { console.error(e); window.showNotification("Error al guardar", "error"); }
        };

        window.updateProductInDB = async (id, data) => {
            if (isOffline) {
                const idx = products.findIndex(p => p.id === id);
                if(idx >= 0) { products[idx] = { ...products[idx], ...data }; saveLocalData(); }
                window.renderProducts();
                if(isAdminLoggedIn) window.renderAdminProducts();
                window.showNotification("Actualizado (Local)", "success");
                return;
            }
            try {
                if(!auth.currentUser) return;
                await updateDoc(doc(db, 'artifacts', appId, 'public', 'data', 'products', id), data);
                window.showNotification("Inventario actualizado", "success");
            } catch (e) { window.showNotification("Error al actualizar", "error"); }
        };

        window.deleteProductFromDB = async (id) => {
            if (isOffline) {
                products = products.filter(p => p.id !== id);
                saveLocalData();
                window.renderProducts();
                if(isAdminLoggedIn) window.renderAdminProducts();
                window.showNotification("Eliminado (Local)", "info");
                return;
            }
            try {
                if(!auth.currentUser) return;
                await deleteDoc(doc(db, 'artifacts', appId, 'public', 'data', 'products', id));
                window.showNotification("Producto eliminado", "info");
            } catch (e) { window.showNotification("Error al eliminar", "error"); }
        };

        window.addOrderToDB = async (orderData) => {
             if (isOffline) {
                 const newOrder = { id: 'loc_ord_'+Date.now(), ...orderData };
                 orders.push(newOrder);
                 saveLocalData();
                 if(isAdminLoggedIn) window.renderAdminOrders();
                 // Simular delay
                 setTimeout(() => window.showNotification("Pedido simulado (Offline)", "success"), 500);
                 return;
             }
             if(!auth.currentUser) return;
             await addDoc(collection(db, 'artifacts', appId, 'public', 'data', 'orders'), orderData);
        };

        window.addAppointmentToDB = async (apptData) => {
             if (isOffline) {
                 const newAppt = { id: 'loc_apt_'+Date.now(), ...apptData };
                 appointments.push(newAppt);
                 saveLocalData();
                 if(isAdminLoggedIn) window.renderAdminAppointments();
                 return;
             }
             if(!auth.currentUser) return;
             await addDoc(collection(db, 'artifacts', appId, 'public', 'data', 'appointments'), apptData);
        };
        
        window.updateOrderInDB = async (id, status) => {
            if (isOffline) {
                const o = orders.find(x => x.id === id);
                if(o) { o.status = status; saveLocalData(); if(isAdminLoggedIn) window.renderAdminOrders(); }
                return;
            }
            if(!auth.currentUser) return;
            await updateDoc(doc(db, 'artifacts', appId, 'public', 'data', 'orders', id), { status });
        };

        window.deleteOrderFromDB = async (id) => {
            if (isOffline) {
                orders = orders.filter(x => x.id !== id);
                saveLocalData();
                if(isAdminLoggedIn) window.renderAdminOrders();
                return;
            }
            if(!auth.currentUser) return;
            await deleteDoc(doc(db, 'artifacts', appId, 'public', 'data', 'orders', id));
        };

        window.deleteAppointmentFromDB = async (id) => {
            if (isOffline) {
                appointments = appointments.filter(x => x.id !== id);
                saveLocalData();
                if(isAdminLoggedIn) window.renderAdminAppointments();
                return;
            }
            if(!auth.currentUser) return;
            await deleteDoc(doc(db, 'artifacts', appId, 'public', 'data', 'appointments', id));
        };

        // --- UTILS ---
        
        window.renderProducts = () => {
            const grid = document.getElementById('products-grid');
            const searchTerm = document.getElementById('search-product')?.value.toLowerCase() || '';
            let filtered = currentFilter === 'todos' ? products : products.filter(p => p.category === currentFilter);
            if (searchTerm) filtered = filtered.filter(p => p.name.toLowerCase().includes(searchTerm));

            grid.innerHTML = filtered.length ? filtered.map(product => `
                <div class="bg-white rounded-3xl shadow-sm hover:shadow-xl border border-gray-100 overflow-hidden card-hover flex flex-col h-full group">
                    <div class="relative pt-[90%] bg-gray-50 overflow-hidden">
                        <img src="${product.image}" onerror="this.src='https://placehold.co/400x300?text=ZOOTPETS'" class="absolute top-0 left-0 w-full h-full object-cover group-hover:scale-110 transition-transform duration-500">
                        <span class="absolute top-4 right-4 bg-white/90 backdrop-blur px-3 py-1 rounded-full text-xs font-extrabold text-orange-600 uppercase shadow-sm tracking-wider">${product.category}</span>
                    </div>
                    <div class="p-6 flex flex-col flex-grow">
                        <h3 class="text-lg font-extrabold text-gray-800 mb-2 leading-tight">${product.name}</h3>
                        <p class="text-gray-500 text-sm mb-5 line-clamp-2 flex-grow font-medium">${product.description}</p>
                        <div class="flex items-center justify-between mt-auto pt-4 border-t border-gray-50">
                            <span class="text-2xl font-black text-orange-600">$${product.price}</span>
                            <button onclick="window.addToCart('${product.id}')" class="bg-gray-900 text-white w-12 h-12 rounded-full flex items-center justify-center hover:bg-orange-500 hover:rotate-90 transition-all shadow-lg"><span class="text-xl font-bold">+</span></button>
                        </div>
                    </div>
                </div>`).join('') : '<div class="col-span-full py-20 text-center text-gray-400 bg-gray-50 rounded-3xl border border-dashed border-gray-300"><p class="text-xl">No encontramos productos con esa búsqueda 🐾</p></div>';
        };

        window.filterProducts = (cat, btn) => {
            currentFilter = cat;
            document.querySelectorAll('.filter-btn').forEach(b => { b.classList.remove('bg-orange-600', 'text-white'); b.classList.add('bg-white', 'text-gray-600'); });
            btn.classList.remove('bg-white', 'text-gray-600'); btn.classList.add('bg-orange-600', 'text-white');
            window.renderProducts();
        };
        
        window.searchProducts = () => window.renderProducts();

        // Cart
        window.toggleCart = () => document.body.classList.toggle('cart-open');
        
        window.addToCart = (id) => {
            const prod = products.find(p => p.id === id);
            const item = cart.find(i => i.id === id);
            if(item) item.quantity++; else cart.push({...prod, quantity: 1});
            saveCart(); window.renderCart(); window.showNotification("¡Añadido a la canasta! 🦴", "success");
        };

        window.removeFromCart = (id) => { cart = cart.filter(i => i.id !== id); saveCart(); window.renderCart(); };
        window.updateQuantity = (id, chg) => {
            const item = cart.find(i => i.id === id);
            if(item) { item.quantity += chg; if(item.quantity <= 0) window.removeFromCart(id); else { saveCart(); window.renderCart(); } }
        };
        
        function saveCart() { localStorage.setItem('zootpetsCart', JSON.stringify(cart)); }

        window.renderCart = () => {
            const container = document.getElementById('cart-items-container');
            const footer = document.getElementById('cart-footer');
            document.getElementById('cart-count').textContent = cart.reduce((s, i) => s + i.quantity, 0);
            
            if(cart.length === 0) {
                container.innerHTML = '<div class="text-center text-gray-400 py-20 flex flex-col items-center"><span class="text-5xl mb-4">🕸️</span><p>Tu canasta está vacía</p></div>';
                footer.innerHTML = '';
            } else {
                container.innerHTML = cart.map(i => `
                    <div class="flex gap-4 items-center bg-white p-3 rounded-xl border border-gray-100 shadow-sm">
                        <img src="${i.image}" class="w-16 h-16 rounded-lg object-cover border">
                        <div class="flex-1">
                            <div class="font-bold text-sm text-gray-800">${i.name}</div>
                            <div class="text-xs text-orange-600 font-bold mt-1">$${i.price} x ${i.quantity}</div>
                        </div>
                        <div class="flex items-center gap-2 bg-gray-100 rounded-lg p-1">
                            <button onclick="window.updateQuantity('${i.id}', -1)" class="w-6 h-6 hover:bg-white rounded font-bold text-gray-600">-</button>
                            <span class="font-medium text-sm">${i.quantity}</span>
                            <button onclick="window.updateQuantity('${i.id}', 1)" class="w-6 h-6 hover:bg-white rounded font-bold text-gray-600">+</button>
                        </div>
                    </div>`).join('');
                const total = cart.reduce((s, i) => s + (i.price * i.quantity), 0);
                footer.innerHTML = `
                    <div class="flex justify-between font-bold mb-6 text-lg text-gray-800"><span>Total</span><span>$${total.toFixed(2)}</span></div>
                    <button onclick="window.showCheckoutForm()" class="w-full gradient-bg text-white py-4 rounded-xl font-bold hover:shadow-lg hover:brightness-110 transition-all">Proceder al Pago</button>
                `;
            }
        };

        // Admin Logic
        window.renderAdminPanel = () => {
            if(!isAdminLoggedIn) { document.getElementById('admin-login').classList.remove('hidden'); document.getElementById('admin-panel').classList.add('hidden'); return; }
            document.getElementById('admin-login').classList.add('hidden'); document.getElementById('admin-panel').classList.remove('hidden');
            window.renderAdminProducts();
        };

        window.renderAdminProducts = () => {
            document.getElementById('admin-productos').innerHTML = `
            <div class="grid lg:grid-cols-3 gap-8">
                <div class="lg:col-span-1 bg-gray-50 p-6 rounded-2xl border border-gray-200 h-fit sticky top-4">
                    <h4 class="font-extrabold text-xl mb-4 text-gray-800">Nuevo Item ZOOT</h4>
                    <form id="add-prod-form" class="space-y-4">
                        <input id="np-name" placeholder="Nombre del producto" class="w-full p-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-orange-500 outline-none" required>
                        <input id="np-price" type="number" placeholder="Precio ($)" class="w-full p-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-orange-500 outline-none" required>
                        <select id="np-cat" class="w-full p-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-orange-500 outline-none bg-white">
                            <option value="alimento">Alimento</option>
                            <option value="juguetes">Juguetes</option>
                            <option value="medicamentos">Medicamentos</option>
                            <option value="accesorios">Accesorios</option>
                        </select>
                        <div>
                            <label class="block text-xs font-bold text-gray-500 mb-1 uppercase">Imagen</label>
                            <input type="file" id="np-file" accept="image/*" class="w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-full file:border-0 file:text-sm file:font-semibold file:bg-orange-50 file:text-orange-700 hover:file:bg-orange-100">
                        </div>
                        <textarea id="np-desc" placeholder="Descripción corta" class="w-full p-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-orange-500 outline-none"></textarea>
                        <button type="submit" class="w-full bg-gray-900 text-white py-3 rounded-xl hover:bg-orange-600 transition-colors font-bold">Guardar ${isOffline ? '(Local)' : ''}</button>
                    </form>
                </div>
                <div class="lg:col-span-2 space-y-3">
                    ${products.map(p => `
                        <div class="flex justify-between items-center bg-white p-4 rounded-xl border border-gray-100 shadow-sm hover:shadow-md transition-shadow">
                            <div class="flex gap-4 items-center">
                                <img src="${p.image}" class="w-14 h-14 rounded-lg object-cover border">
                                <div>
                                    <div class="font-bold text-gray-800">${p.name}</div>
                                    <div class="text-xs font-mono text-gray-500 bg-gray-100 inline-block px-2 py-1 rounded mt-1">$${p.price} | ${p.category}</div>
                                </div>
                            </div>
                            <div class="flex gap-3">
                                <button onclick="window.editProduct('${p.id}')" class="w-8 h-8 rounded-full bg-blue-50 text-blue-600 hover:bg-blue-100 flex items-center justify-center">✎</button>
                                <button onclick="window.deleteProductFromDB('${p.id}')" class="w-8 h-8 rounded-full bg-red-50 text-red-600 hover:bg-red-100 flex items-center justify-center">🗑</button>
                            </div>
                        </div>`).join('')}
                </div>
            </div>`;
            document.getElementById('add-prod-form').addEventListener('submit', async e => {
                e.preventDefault();
                const file = document.getElementById('np-file').files[0];
                const img = file ? await processImage(file) : 'https://placehold.co/400?text=ZOOTPETS';
                await window.addProductToDB({
                    name: document.getElementById('np-name').value,
                    price: Number(document.getElementById('np-price').value),
                    category: document.getElementById('np-cat').value,
                    description: document.getElementById('np-desc').value,
                    image: img
                });
                e.target.reset();
            });
        };

        window.renderAdminOrders = () => {
            document.getElementById('admin-envios').innerHTML = orders.length ? orders.map(o => `
                <div class="bg-white p-5 rounded-xl shadow-sm mb-3 border-l-4 ${o.status === 'nuevo' ? 'border-green-500' : 'border-blue-500'}">
                    <div class="flex justify-between font-bold text-lg mb-2">
                        <span class="flex items-center gap-2">📦 #${o.orderId || 'ID'}</span>
                        <span class="text-orange-600">$${o.total}</span>
                    </div>
                    <div class="text-sm text-gray-600 mb-3 bg-gray-50 p-3 rounded-lg">
                        <p><strong>Cliente:</strong> ${o.customer} (${o.phone})</p>
                        <p><strong>Dirección:</strong> ${o.address}</p>
                    </div>
                    <div class="flex justify-between items-center mt-2">
                        <span class="uppercase text-xs font-bold px-3 py-1 rounded-full ${o.status === 'nuevo' ? 'bg-green-100 text-green-700' : 'bg-blue-100 text-blue-700'}">${o.status || 'nuevo'}</span>
                        <div class="flex gap-2">
                            <button onclick="window.updateOrderInDB('${o.id}', 'en-camino')" class="text-xs bg-blue-600 text-white px-3 py-2 rounded-lg font-bold hover:bg-blue-700">Marcar Enviado</button>
                            <button onclick="window.deleteOrderFromDB('${o.id}')" class="text-xs bg-red-100 text-red-700 px-3 py-2 rounded-lg hover:bg-red-200">Borrar</button>
                        </div>
                    </div>
                </div>`).join('') : '<div class="text-center py-10 text-gray-400">No hay pedidos pendientes.</div>';
        };

        window.renderAdminAppointments = () => {
             document.getElementById('admin-citas').innerHTML = appointments.length ? appointments.map(a => `
                <div class="bg-white p-5 rounded-xl shadow-sm mb-3 border-l-4 border-purple-500 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4">
                    <div>
                        <div class="font-bold text-lg text-gray-800">${a.pet} <span class="text-sm font-normal text-gray-500">(${a.owner})</span></div>
                        <div class="text-sm font-medium text-purple-600 bg-purple-50 px-2 py-1 rounded inline-block mt-1">${a.date} - ${a.time}</div>
                        <div class="text-xs text-gray-500 mt-2 italic">${a.reason}</div>
                    </div>
                    <button onclick="window.deleteAppointmentFromDB('${a.id}')" class="text-red-500 text-xs font-bold hover:bg-red-50 px-3 py-2 rounded border border-red-100">Cancelar Cita</button>
                </div>`).join('') : '<div class="text-center py-10 text-gray-400">Agenda libre hoy.</div>';
        };

        window.showAdminTab = (tab, btn) => {
            document.querySelectorAll('.admin-content').forEach(e => e.classList.add('hidden'));
            document.getElementById(`admin-${tab}`).classList.remove('hidden');
            document.querySelectorAll('.admin-tab').forEach(b => { b.classList.remove('bg-orange-600','text-white'); b.classList.add('bg-gray-800','text-gray-400'); });
            btn.classList.remove('bg-gray-800','text-gray-400'); btn.classList.add('bg-orange-600','text-white');
            if(tab === 'productos') window.renderAdminProducts();
            if(tab === 'envios') window.renderAdminOrders();
            if(tab === 'citas') window.renderAdminAppointments();
        };

        window.editProduct = (id) => {
            const p = products.find(x => x.id === id);
            if(!p) return;
            const modal = document.getElementById('edit-product-modal');
            
            modal.innerHTML = `
            <div class="bg-white p-8 rounded-3xl max-w-md w-full mx-4 animate-[slideUp_0.3s_ease] shadow-2xl">
                <h3 class="font-extrabold text-2xl mb-6 text-gray-800">Editar Item ZOOT</h3>
                <form id="edit-form" class="space-y-4">
                    <div class="text-center mb-4 bg-gray-50 p-4 rounded-xl border border-dashed border-gray-300">
                        <img src="${p.image}" class="h-24 w-24 object-cover rounded-lg mx-auto mb-3 shadow-sm">
                        <label class="block text-sm font-bold text-orange-600 cursor-pointer hover:underline">
                            Cambiar Imagen
                            <input type="file" id="ep-file" accept="image/*" class="hidden">
                        </label>
                    </div>
                    <input id="ep-name" value="${p.name}" placeholder="Nombre" class="w-full p-3 border rounded-xl outline-none focus:border-orange-500" required>
                    <input id="ep-price" type="number" value="${p.price}" placeholder="Precio" class="w-full p-3 border rounded-xl outline-none focus:border-orange-500" required>
                    <select id="ep-cat" class="w-full p-3 border rounded-xl outline-none focus:border-orange-500 bg-white">
                        <option value="alimento" ${p.category === 'alimento' ? 'selected' : ''}>Alimento</option>
                        <option value="juguetes" ${p.category === 'juguetes' ? 'selected' : ''}>Juguetes</option>
                        <option value="medicamentos" ${p.category === 'medicamentos' ? 'selected' : ''}>Medicamentos</option>
                        <option value="accesorios" ${p.category === 'accesorios' ? 'selected' : ''}>Accesorios</option>
                    </select>
                    <textarea id="ep-desc" placeholder="Descripción" class="w-full p-3 border rounded-xl outline-none focus:border-orange-500 h-24 resize-none">${p.description}</textarea>
                    <div class="flex justify-end gap-3 pt-2">
                        <button type="button" onclick="document.getElementById('edit-product-modal').classList.remove('show')" class="px-5 py-2 border border-gray-300 rounded-xl font-bold text-gray-600 hover:bg-gray-50">Cancelar</button>
                        <button type="submit" class="px-5 py-2 bg-orange-600 text-white rounded-xl font-bold hover:bg-orange-700 shadow-lg">Guardar Cambios</button>
                    </div>
                </form>
            </div>`;
            
            modal.classList.add('show');
            
            document.getElementById('edit-form').addEventListener('submit', async e => {
                e.preventDefault();
                const fileInput = document.getElementById('ep-file');
                let imageToSave = p.image;

                if (fileInput.files && fileInput.files[0]) {
                    try {
                        imageToSave = await processImage(fileInput.files[0]);
                    } catch (err) {
                        console.error("Error processing image", err);
                    }
                }

                await window.updateProductInDB(id, { 
                    name: document.getElementById('ep-name').value, 
                    price: Number(document.getElementById('ep-price').value),
                    category: document.getElementById('ep-cat').value, 
                    description: document.getElementById('ep-desc').value,
                    image: imageToSave
                });
                modal.classList.remove('show');
            });
        };

        // Checkout Logic
        window.showCheckoutForm = () => {
            const modal = document.getElementById('checkout-modal');
            modal.innerHTML = `
            <div class="bg-white p-8 rounded-3xl max-w-md w-full mx-4 animate-[slideUp_0.3s_ease] shadow-2xl relative overflow-hidden">
                <div class="absolute top-0 left-0 w-full h-2 gradient-bg"></div>
                <h3 class="font-extrabold text-2xl mb-6 text-gray-800">Finalizar Compra</h3>
                <form id="checkout-form" class="space-y-4">
                    <input id="c-name" placeholder="Tu Nombre" class="w-full p-3 bg-gray-50 border border-gray-200 rounded-xl outline-none focus:border-orange-500" required>
                    <input id="c-phone" placeholder="Teléfono de contacto" class="w-full p-3 bg-gray-50 border border-gray-200 rounded-xl outline-none focus:border-orange-500" required>
                    <textarea id="c-addr" placeholder="Dirección de entrega completa" class="w-full p-3 bg-gray-50 border border-gray-200 rounded-xl outline-none focus:border-orange-500 h-24 resize-none" required></textarea>
                    <div class="bg-orange-50 p-4 rounded-xl flex justify-between items-center">
                        <span class="text-sm font-bold text-gray-500">Total a Pagar:</span>
                        <span class="text-xl font-black text-orange-600">$${cart.reduce((s,i)=>s+(i.price*i.quantity),0)}</span>
                    </div>
                    <button type="submit" class="w-full gradient-bg text-white py-4 rounded-xl font-bold text-lg hover:brightness-110 shadow-xl transition-all">Confirmar Pedido</button>
                </form>
                <button onclick="document.getElementById('checkout-modal').classList.remove('show')" class="mt-4 text-gray-400 text-sm font-medium hover:text-gray-600 w-full text-center">Cancelar operación</button>
            </div>`;
            modal.classList.add('show');
            document.getElementById('checkout-form').addEventListener('submit', async e => {
                e.preventDefault();
                const order = { orderId: 'ZOOT'+Date.now().toString().slice(-4), customer: document.getElementById('c-name').value, phone: document.getElementById('c-phone').value, address: document.getElementById('c-addr').value, total: cart.reduce((s,i)=>s+(i.price*i.quantity),0), status: 'nuevo', items: cart };
                
                // Send Whatsapp ZOOTPETS Style
                let msg = `🐶 *NUEVO PEDIDO ZOOTPETS* 🐱\n\n🆔 ID: ${order.orderId}\n👤 Cliente: ${order.customer}\n📞 Tel: ${order.phone}\n📍 Dirección: ${order.address}\n💰 Total: $${order.total}\n\n📝 *Detalle:*\n${order.items.map(i => `- ${i.name} x${i.quantity}`).join('\n')}`;
                window.open(`https://wa.me/5212452070033?text=${encodeURIComponent(msg)}`, '_blank');
                
                await window.addOrderToDB(order);
                cart = []; saveCart(); window.renderCart(); document.getElementById('checkout-modal').classList.remove('show'); window.toggleCart();
                window.showNotification("¡Gracias! Tu pedido está en camino 🚚", "success");
            });
        };
        
        // Appointment Logic
        document.getElementById('appointment-form').addEventListener('submit', async e => {
            e.preventDefault();
            const appt = {
                owner: document.getElementById('owner-name').value,
                phone: document.getElementById('owner-phone').value,
                pet: document.getElementById('pet-name').value,
                reason: document.getElementById('appointment-reason').value,
                date: document.getElementById('appointment-date').value,
                time: document.getElementById('appointment-time').value
            };
            let msg = `🏥 *CITA VETERINARIA ZOOTPETS* 🩺\n\n👤 Dueño: ${appt.owner}\n🐾 Mascota: ${appt.pet}\n📋 Motivo: ${appt.reason}\n📅 Fecha: ${appt.date}\n⏰ Hora: ${appt.time}`;
            window.open(`https://wa.me/5212452070033?text=${encodeURIComponent(msg)}`, '_blank');
            await window.addAppointmentToDB(appt);
            e.target.reset();
            window.showNotification("Cita agendada correctamente 📅", "success");
        });

        // Admin Login
        document.getElementById('admin-login-form').addEventListener('submit', e => {
            e.preventDefault();
            if(document.getElementById('admin-username').value === 'admin' && document.getElementById('admin-password').value === 'password123') {
                isAdminLoggedIn = true; localStorage.setItem('isAdmin', 'true'); window.renderAdminPanel();
            } else window.showNotification('Credenciales inválidas 🔒', 'error');
        });
        window.logoutAdmin = () => { isAdminLoggedIn = false; localStorage.removeItem('isAdmin'); window.renderAdminPanel(); };

        // Helpers
        window.showNotification = (msg, type) => {
            const div = document.createElement('div'); 
            div.className = `fixed top-24 right-6 px-6 py-4 rounded-xl shadow-2xl text-white font-bold z-[2000] animate-[slideUp_0.3s_ease] flex items-center gap-3 ${type === 'error' ? 'bg-red-500' : (type === 'info' ? 'bg-blue-600' : 'bg-gray-900')}`; 
            div.innerHTML = type === 'error' ? `<span>⚠️</span> ${msg}` : `<span>✅</span> ${msg}`;
            document.body.appendChild(div); 
            setTimeout(() => div.remove(), 3000);
        };
        window.scrollToSection = (id) => document.getElementById(id)?.scrollIntoView({behavior: 'smooth'});
        window.toggleMobileMenu = () => document.getElementById('mobile-menu').classList.toggle('hidden');
        window.searchOrder = () => {
             const id = document.getElementById('order-search').value; 
             const o = orders.find(x => x.orderId == id || x.id == id);
             const res = document.getElementById('order-result');
             res.classList.remove('hidden');
             res.innerHTML = o ? `
                <div class="text-center">
                    <div class="text-4xl mb-2">${o.status === 'en-camino' ? '🚚' : '📦'}</div>
                    <h3 class="font-bold text-xl text-gray-800">Pedido #${o.orderId}</h3>
                    <div class="my-4">
                        <div class="w-full bg-gray-200 rounded-full h-2.5">
                          <div class="bg-orange-600 h-2.5 rounded-full" style="width: ${o.status === 'en-camino' ? '80%' : '20%'}"></div>
                        </div>
                        <p class="text-xs text-gray-500 mt-2 uppercase tracking-widest font-bold">${o.status}</p>
                    </div>
                    <p class="font-medium text-gray-600">Total: $${o.total}</p>
                </div>` : '<p class="text-gray-500 text-center italic">No encontramos ese pedido. Revisa el ID.</p>';
        };
        window.handleReasonChange = () => {
             const val = document.getElementById('appointment-reason').value;
             document.getElementById('address-container').classList.toggle('hidden', !val.includes('Domicilio'));
        };

        // Image Compressor
        const processImage = (file) => new Promise((resolve) => {
            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = (e) => {
                const img = new Image(); img.src = e.target.result;
                img.onload = () => {
                    const cvs = document.createElement('canvas'); const ctx = cvs.getContext('2d');
                    const scale = Math.min(500/img.width, 500/img.height);
                    cvs.width = img.width * scale; cvs.height = img.height * scale;
                    ctx.drawImage(img,0,0,cvs.width,cvs.height);
                    resolve(cvs.toDataURL('image/jpeg', 0.7));
                };
            };
        });

        // Seed Data Helpers
        const defaults = [
            {id: "1", name:"ZootMix Premium (Adulto)", price:650, category:"alimento", image:"https://images.unsplash.com/photo-1568640347023-a616a30bc3bd?auto=format&fit=crop&w=400&q=80", description:"Nutrición completa para energía diaria."},
            {id: "2", name:"Pelota Resistente K9", price:120, category:"juguetes", image:"https://images.unsplash.com/photo-1546422401-68b415cbf8de?auto=format&fit=crop&w=400&q=80", description:"Indestructible, ideal para mordedores fuertes."},
            {id: "3", name:"Correa Retráctil 5m", price:340, category:"accesorios", image:"https://images.unsplash.com/photo-1576201836106-db1758fd1c97?auto=format&fit=crop&w=400&q=80", description:"Paseos con libertad y seguridad."},
            {id: "4", name:"Vitaminas ZootVits", price:210, category:"medicamentos", image:"https://images.unsplash.com/photo-1584017911766-d451b3d0e843?auto=format&fit=crop&w=400&q=80", description:"Suplemento multivitamínico diario."}
        ];

        // Local Seed for Offline Mode
        const seedDataLocal = async () => {
            products = [...defaults];
            saveLocalData();
            window.renderProducts();
        };

        const seedData = async () => {
             localStorage.setItem('zootSeeded', 'true');
             defaults.forEach(d => window.addProductToDB(d));
        };

        // Render initial
        window.renderProducts();
        window.renderCart();
        window.renderAdminPanel();

    </script>
</body>
</html>
