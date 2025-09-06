# ridemc
ridemc store
<!-- Cleaned up stray text and comments from previous edits -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RideMc Store - Minecraft Server Shop</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600;700&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Montserrat', sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a202c 0%, #2d3748 100%);
            min-height: 100vh;
            color: #e2e8f0;
        }
        
        .minecraft-btn {
            background: linear-gradient(145deg, #4299e1, #3182ce);
            border: 2px solid #2b6cb0;
            transition: all 0.3s ease;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            cursor: pointer;
        }
        
        .minecraft-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
            background: linear-gradient(145deg, #3182ce, #2b6cb0);
        }
        
        .gamemode-tab {
            transition: all 0.3s ease;
            border-bottom: 3px solid transparent;
            cursor: pointer;
        }
        
        .gamemode-tab.active {
            border-bottom: 3px solid #4299e1;
            background: rgba(66, 153, 225, 0.1);
        }
        
        .category-card {
            background: rgba(45, 55, 72, 0.8);
            border: 2px solid #4a5568;
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
            cursor: pointer;
        }
        
        .category-card:hover {
            transform: translateY(-5px);
            border-color: #4299e1;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
        }
        
        .product-card {
            background: rgba(74, 85, 104, 0.6);
            border: 1px solid #4a5568;
            transition: all 0.3s ease;
        }
        
        .product-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
            border-color: #4299e1;
        }
        
        .cart-notification {
            animation: slideIn 0.3s ease-out;
        }
        
        @keyframes slideIn {
            from {
                transform: translateX(100%);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }
        
        .currency-selector {
            background: rgba(45, 55, 72, 0.8);
            border: 2px solid #4a5568;
            color: white;
            padding: 8px 12px;
            border-radius: 6px;
            margin-left: 10px;
        }
        
        .currency-selector:focus {
            outline: none;
            border-color: #4299e1;
        }
    </style>
</head>
<body class="min-h-screen">
    <!-- Header -->
    <header class="bg-gray-900 border-b-4 border-blue-600 shadow-xl">
        <div class="container mx-auto px-4 py-4">
            <div class="flex flex-col md:flex-row justify-between items-center">
                <div class="flex items-center mb-4 md:mb-0">
                    <div class="w-12 h-12 bg-blue-600 rounded-lg flex items-center justify-center mr-3 overflow-hidden">
                        <img src="https://media.discordapp.net/attachments/1392460230318620813/1392460416051056704/5f4f1699-71ab-49b8-8d3b-aeedbf3034e1.png?ex=68af8e11&is=68ae3c91&hm=99c19405ec98a2b0efab1ed3ec7aaed2134b6b7f09c6695e21955367f83fd131&=&format=webp&quality=lossless" alt="Logo" class="object-cover w-12 h-12">
                    </div>
                    <h1 class="text-3xl font-bold text-white">RideMc Store</h1>
                </div>
                
                <div class="flex items-center space-x-4">
                    <div class="relative">
                        <button id="cartBtn" class="minecraft-btn px-6 py-2 rounded-lg text-white font-semibold flex items-center">
                            <i class="fas fa-shopping-cart mr-2"></i>
                            Cart <span id="cartCount" class="ml-2 bg-red-500 rounded-full px-2 py-1 text-xs">0</span>
                        </button>
                    </div>
                    <button id="joinServerBtn" class="bg-green-600 hover:bg-green-700 px-6 py-2 rounded-lg text-white font-semibold">
                        Join Server
                    </button>
    <!-- Join Server Modal -->
    <div id="joinServerModal" class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-60 z-50 hidden">
        <div class="bg-gray-900 rounded-lg shadow-lg p-8 max-w-sm w-full relative">
            <button id="closeJoinServerModal" class="absolute top-2 right-2 text-gray-400 hover:text-white text-2xl">&times;</button>
            <h2 class="text-2xl font-bold text-white mb-4">Server IP</h2>
            <p class="text-gray-300 mb-6">IP: <span id="serverIpModal" class="font-mono text-green-400 cursor-pointer hover:underline" title="Click to copy">play.ridemc.fun</span></p>
        </div>
    </div>
                </div>
            </div>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="relative py-16 bg-gradient-to-r from-blue-900 to-purple-900">
        <div class="container mx-auto px-4 text-center">
            <div class="max-w-3xl mx-auto">
                <h2 class="text-5xl font-bold text-white mb-4">Welcome to RideMc</h2>
                <p class="text-xl text-blue-200 mb-8">The Ultimate Minecraft Experience with Unique Gamemodes</p>
                <div class="flex flex-wrap justify-center gap-4">
                    <div class="bg-blue-600/30 backdrop-blur-sm px-4 py-2 rounded border border-blue-500">
                        <span id="serverIpHero" class="text-white cursor-pointer hover:underline" title="Click to copy">IP: play.ridemc.fun</span>
                    </div>
                    <div class="bg-green-600/30 backdrop-blur-sm px-4 py-2 rounded border border-green-500">
                        <span class="text-white">Version: 1.18+</span>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Currency Selector -->
    <div class="bg-gray-800 py-3">
        <div class="container mx-auto px-4 flex justify-end items-center">
            <span class="text-gray-300 mr-2">Currency:</span>
            <select id="currencySelector" class="currency-selector">
                <option value="NPR">NPR (नेरू)</option>
                <option value="USD">USD ($)</option>
                <option value="EUR">EUR (€)</option>
                <option value="GBP">GBP (£)</option>
                <option value="INR">INR (₹)</option>
            </select>
        </div>
    </div>

    <!-- Gamemode Navigation -->
    <section class="bg-gray-800 py-6 sticky top-0 z-10 shadow-lg">
        <div class="container mx-auto px-4">
            <div class="flex flex-wrap justify-center gap-2 md:gap-4">
                <button data-gamemode="lifesteal" class="gamemode-tab active px-6 py-3 rounded-lg bg-blue-600 text-white font-semibold">
                    <i class="fas fa-heart mr-2"></i>Lifesteal
                </button>
                <button data-gamemode="survival" class="gamemode-tab px-6 py-3 rounded-lg bg-green-600 text-white font-semibold">
                    <i class="fas fa-tree mr-2"></i>Survival
                </button>
                <button data-gamemode="skyblock" class="gamemode-tab px-6 py-3 rounded-lg bg-yellow-500 text-white font-semibold">
                    <i class="fas fa-cloud mr-2"></i>Skyblock
                </button>
                <button data-gamemode="pvp" class="gamemode-tab px-6 py-3 rounded-lg bg-red-600 text-white font-semibold">
                    <i class="fas fa-fist-raised mr-2"></i>FFA
                </button>
            </div>
        </div>
    </section>

    <!-- Main Content -->
    <main class="container mx-auto px-4 py-8">
        <!-- Lifesteal Section -->
        <div id="lifesteal" class="gamemode-content active">
            <h2 class="text-3xl font-bold text-white mb-8 text-center"><i class="fas fa-heart text-red-500 mr-2"></i>Lifesteal Store</h2>
            
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-12" id="lifesteal-categories">
                <div class="category-card p-6 rounded-lg text-center" data-gamemode="lifesteal" data-category="ranks">
                    <div class="w-16 h-16 bg-gradient-to-r from-purple-500 to-pink-500 rounded-full mx-auto mb-4 flex items-center justify-center">
                        <i class="fas fa-crown text-white text-2xl"></i>
                    </div>
                    <h3 class="text-xl font-semibold text-white mb-2">Ranks</h3>
                    <p class="text-gray-300">Exclusive permissions and perks</p>
                </div>
                
                <div class="category-card p-6 rounded-lg text-center" data-gamemode="lifesteal" data-category="kits">
                    <div class="w-16 h-16 bg-gradient-to-r from-blue-500 to-cyan-500 rounded-full mx-auto mb-4 flex items-center justify-center">
                        <i class="fas fa-box-open text-white text-2xl"></i>
                    </div>
                    <h3 class="text-xl font-semibold text-white mb-2">Kits</h3>
                    <p class="text-gray-300">Powerful item packages</p>
                </div>
                
                <div class="category-card p-6 rounded-lg text-center" data-gamemode="lifesteal" data-category="coins">
                    <div class="w-16 h-16 bg-gradient-to-r from-yellow-500 to-orange-500 rounded-full mx-auto mb-4 flex items-center justify-center">
                        <i class="fas fa-coins text-white text-2xl"></i>
                    </div>
                    <h3 class="text-xl font-semibold text-white mb-2">Coins</h3>
                    <p class="text-gray-300">Server currency packages</p>
                </div>
                
                <div class="category-card p-6 rounded-lg text-center" data-gamemode="lifesteal" data-category="keys">
                    <div class="w-16 h-16 bg-gradient-to-r from-green-500 to-emerald-500 rounded-full mx-auto mb-4 flex items-center justify-center">
                        <i class="fas fa-key text-white text-2xl"></i>
                    </div>
                    <h3 class="text-xl font-semibold text-white mb-2">Crate Keys</h3>
                    <p class="text-gray-300">Open exclusive crates</p>
                </div>
            </div>

            <!-- Products will be loaded here based on category selection -->
            <div id="lifesteal-products" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <div class="text-gray-400 text-center col-span-full py-8">
                    Select a category above to view products
                </div>
            </div>
        </div>

        <!-- Survival Section -->
        <div id="survival" class="gamemode-content hidden">
            <h2 class="text-3xl font-bold text-white mb-8 text-center"><i class="fas fa-tree text-green-500 mr-2"></i>Survival Store</h2>
            <!-- Survival bottom hidden for now -->
        </div>

        <!-- PvP Practice Section -->
        <!-- Skyblock Section -->
        <div id="skyblock" class="gamemode-content hidden">
            <h2 class="text-3xl font-bold text-white mb-8 text-center"><i class="fas fa-cloud text-yellow-400 mr-2"></i>Skyblock Store</h2>
            <!-- Skyblock bottom hidden for now -->
        </div>
        <div id="pvp" class="gamemode-content hidden">
            <h2 class="text-3xl font-bold text-white mb-8 text-center"><i class="fas fa-fist-raised text-red-500 mr-2"></i>FFA Store</h2>
            <!-- PvP bottom hidden for now -->
        </div>
    </main>

    <!-- Cart Sidebar -->
    <div id="cartSidebar" class="fixed top-0 right-0 h-full w-80 bg-gray-900 shadow-2xl transform translate-x-full transition-transform duration-300 z-50">
        <div class="p-6 h-full flex flex-col">
            <div class="flex justify-between items-center mb-6">
                <h3 class="text-xl font-bold text-white">Your Cart</h3>
                <button id="closeCart" class="text-gray-400 hover:text-white">
                    <i class="fas fa-times text-xl"></i>
                </button>
            </div>
            
            <div id="cartItems" class="flex-1 overflow-y-auto mb-4">
                <!-- Cart items will be added here -->
                <p class="text-gray-400 text-center py-8">Your cart is empty</p>
            </div>
            
            <div class="border-t border-gray-700 pt-4">
                <div class="flex justify-between items-center mb-4">
                    <span class="text-gray-300">Total:</span>
                    <span id="cartTotal" class="text-xl font-bold text-white">NPR 0.00</span>
                </div>
                <button id="checkoutBtn" class="w-full bg-green-600 hover:bg-green-700 py-3 rounded-lg text-white font-semibold">
                    Checkout
                </button>



            </div>
        </div>
    </div>

    <!-- Cart Notification -->
    <div id="cartNotification" class="fixed top-4 right-4 bg-green-600 text-white px-6 py-3 rounded-lg shadow-lg cart-notification hidden z-50">
        Item added to cart!
    </div>

    <!-- Footer -->
    <footer class="bg-gray-900 border-t border-gray-700 py-8 mt-12">
        <div class="container mx-auto px-4">
            <div class="text-center">
                <div class="flex justify-center mb-4">
                    <div class="w-12 h-12 bg-blue-600 rounded-lg flex items-center justify-center mr-3">
                        <i class="fas fa-cube text-white text-2xl"></i>
                    </div>
                </div>
                <h3 class="text-2xl font-bold text-white mb-2">RideMc</h3>
                <p class="text-gray-400 mb-6">The ultimate Minecraft server experience</p>
                
                <div class="flex justify-center space-x-6 mb-6">
                    <a href="https://discord.gg/NuKedJw67G" class="text-gray-400 hover:text-blue-400" target="_blank" rel="noopener">
                        <i class="fab fa-discord text-2xl"></i>
                    </a>
                </div>
                
                <p class="text-gray-500 text-sm">© 2023 RideMc Server. All rights reserved.</p>
            </div>
        </div>
    </footer>

    <div id="copyNotification" class="fixed top-20 left-1/2 transform -translate-x-1/2 bg-blue-600 text-white px-4 py-2 rounded shadow-lg z-50 hidden">Copied!</div>
    <script>
        // Currency exchange rates (for demonstration purposes)
        const exchangeRates = {
            NPR: { symbol: 'NPR', rate: 1, name: 'Nepalese Rupee' },
            USD: { symbol: '$', rate: 0.0075, name: 'US Dollar' },
            EUR: { symbol: '€', rate: 0.0069, name: 'Euro' },
            GBP: { symbol: '£', rate: 0.0059, name: 'British Pound' },
            INR: { symbol: '₹', rate: 0.62, name: 'Indian Rupee' }
        };

        // Product data
        const products = {
            lifesteal: {
                    ranks: [
                        { id: 1, name: "KING", price: 999, description: "Become a king of ridemc lifesteal" },
                        { id: 2, name: "EMPEROR", price: 699, description: "Become a emperor of ridemc lifesteal" },
                        { id: 3, name: "WARLORD", price: 499, description: "Become a warloard of ridemc lifesteal" },
                        { id: 4, name: "CHAMPION", price: 299, description: "Become a campion of ridemc lifesteal" },
                        { id: 5, name: "KNIGHT", price: 149, description: "become a kinght of ridemc lifesteal" }
                    ],
                kits: [
                    { id: 21, name: "King Kit", price: 200, description: "get the kit of king rank" },
                    { id: 22, name: "Emperor Kit", price: 149, description: "get the kit of emperior rank" },
                    { id: 23, name: "Warlord Kit", price: 100, description: "get the kit of warloard rank" },
                    { id: 24, name: "Champion Kit", price: 75, description: "get the kit of champion rank" },
                    { id: 25, name: "Knight Kit", price: 50, description: "get the kit of knight rank" }
                ],
                coins: [
                    { id: 8, name: "1,000 Coins", price: 4.99, description: "Small coin package" },
                    { id: 9, name: "5,000 Coins", price: 19.99, description: "Medium coin package" },
                    { id: 10, name: "10,000 Coins", price: 34.99, description: "Large coin package" }
                ],
                keys: [
                    { id: 11, name: "3 Crate Keys", price: 5.99, description: "Open 3 crates" },
                    { id: 12, name: "7 Crate Keys", price: 11.99, description: "Open 7 crates" },
                    { id: 13, name: "15 Crate Keys", price: 22.99, description: "Open 15 crates" }
                ]
            },
            survival: {
                ranks: [
                    { id: 14, name: "Chicken Rank", price: 35, description: "Basic survival rank with starter perks" },
                    { id: 15, name: "Fox Rank", price: 70, description: "Enhanced survival abilities" },
                    { id: 16, name: "Witch Rank", price: 100, description: "Magical abilities and potion perks" },
                    { id: 17, name: "Squid Rank", price: 150, description: "Aquatic abilities and water perks" },
                    { id: 18, name: "Creeper Rank", price: 200, description: "Explosive abilities and mining perks" },
                    { id: 19, name: "Goat Rank", price: 250, description: "Mountain climbing and agility perks" }
                ],
                kits: [
                    { id: 20, name: "Chicken Kit", price: 10, description: "Basic starter items" },
                    { id: 21, name: "Fox Kit", price: 20, description: "Enhanced survival tools" },
                    { id: 22, name: "Witch Kit", price: 35, description: "Potion brewing supplies" },
                    { id: 23, name: "Squid Kit", price: 50, description: "Fishing and aquatic gear" },
                    { id: 24, name: "Creeper Kit", price: 65, description: "Mining explosives and tools" },
                    { id: 25, name: "Goat Kit", price: 80, description: "Mountain climbing gear" }
                ],
                coins: [
                    { id: 26, name: "500 Coins", price: 30, description: "Small coin package" },
                    { id: 27, name: "1000 Coins", price: 65, description: "Medium coin package" },
                    { id: 28, name: "5000 Coins", price: 200, description: "Large coin package" },
                    { id: 29, name: "10000 Coins", price: 350, description: "Massive coin package" }
                ],
                keys: [
                    { id: 30, name: "Premium Key", price: 20, description: "Open premium crates" },
                    { id: 31, name: "Ultimate Key", price: 30, description: "Open ultimate crates" },
                    { id: 32, name: "Legendary Key", price: 45, description: "Open legendary crates" },
                    { id: 33, name: "Seasonal Key", price: 60, description: "Open seasonal crates" }
                ]
            },
            pvp: {
                ranks: [
                    { id: 101, name: "Overloard", price: 100, description: "Overloard rank with ultimate PvP powers" },
                    { id: 102, name: "Titan", price: 70, description: "Titan rank with advanced PvP features" },
                    { id: 103, name: "Legend", price: 50, description: "Legend rank with exclusive PvP perks" },
                    { id: 104, name: "Duke", price: 30, description: "Duke rank with special PvP abilities" },
                    { id: 105, name: "MVP", price: 15, description: "MVP rank for rising PvP stars" }
                ]
            },
            skyblock: {
                ranks: [
                    { id: 201, name: "Vip", price: 59, description: "Vip rank with special perks" },
                    { id: 202, name: "Vip+", price: 99, description: "Vip+ rank with extra features" },
                    { id: 203, name: "Mvp", price: 149, description: "Mvp rank with premium benefits" },
                    { id: 204, name: "Mvp+", price: 199, description: "Mvp+ rank with advanced perks" },
                    { id: 205, name: "Mvp++", price: 249, description: "Mvp++ rank with all exclusive features" }
                ]
            }
        };

        // Global variables
        let cart = [];
        let currentGamemode = 'lifesteal';
        let currentCategory = 'ranks';
        let currentCurrency = 'NPR';

        // DOM elements
        const gamemodeTabs = document.querySelectorAll('.gamemode-tab');
        const gamemodeContents = document.querySelectorAll('.gamemode-content');
        const categoryCards = document.querySelectorAll('.category-card');
        const cartBtn = document.getElementById('cartBtn');
        const cartSidebar = document.getElementById('cartSidebar');
        const closeCart = document.getElementById('closeCart');
        const cartItems = document.getElementById('cartItems');
        const cartCount = document.getElementById('cartCount');
        const cartTotal = document.getElementById('cartTotal');
        const cartNotification = document.getElementById('cartNotification');
        const currencySelector = document.getElementById('currencySelector');

        // Initialize the store
        function initStore() {
            loadProducts('lifesteal', 'ranks');
            setupEventListeners();
            updateAllPrices();
        }

        // Set up event listeners
        function setupEventListeners() {
            // Gamemode tabs
            gamemodeTabs.forEach(tab => {
                tab.addEventListener('click', (e) => {
                    const gamemode = tab.getAttribute('data-gamemode');
                    switchGamemode(gamemode);
                });
            });

            // Category cards
            document.addEventListener('click', (e) => {
                const categoryCard = e.target.closest('.category-card');
                if (categoryCard) {
                    const gamemode = categoryCard.getAttribute('data-gamemode');
                    const category = categoryCard.getAttribute('data-category');
                    currentGamemode = gamemode;
                    currentCategory = category;
                    loadProducts(gamemode, category);
                }
            });

            // Add to cart buttons
            document.addEventListener('click', (e) => {
                const addToCartBtn = e.target.closest('.add-to-cart');
                if (addToCartBtn) {
                    const id = parseInt(addToCartBtn.getAttribute('data-id'));
                    const name = addToCartBtn.getAttribute('data-name');
                    const price = parseFloat(addToCartBtn.getAttribute('data-price'));
                    addToCart(id, name, price);
                }
                // Remove from cart button
                const removeFromCartBtn = e.target.closest('.remove-from-cart');
                if (removeFromCartBtn) {
                    const id = parseInt(removeFromCartBtn.getAttribute('data-id'));
                    removeFromCart(id);
                }
            });

            // Cart functionality
            cartBtn.addEventListener('click', () => {
                cartSidebar.classList.remove('translate-x-full');
            });

            closeCart.addEventListener('click', () => {
                cartSidebar.classList.add('translate-x-full');
            });

            // Currency selector
            currencySelector.addEventListener('change', (e) => {
                currentCurrency = e.target.value;
                updateAllPrices();
                updateCart();
            });
        }

        // Attach the view-product event listener globally, only once
        if (!window._viewBtnListenerAdded) {
            document.addEventListener('click', (e) => {
                const viewBtn = e.target.closest('.view-product');
                if (viewBtn) {
                    const name = viewBtn.getAttribute('data-name');
                    const description = viewBtn.getAttribute('data-description');
                    showProductModal(name, description);
                }
            });
            window._viewBtnListenerAdded = true;
        }

        // Switch between gamemodes
        function switchGamemode(gamemode) {
            currentGamemode = gamemode;
            
            // Update active tab
            gamemodeTabs.forEach(tab => {
                if (tab.getAttribute('data-gamemode') === gamemode) {
                    tab.classList.add('active');
                } else {
                    tab.classList.remove('active');
                }
            });
            
            // Show correct content
            gamemodeContents.forEach(content => {
                if (content.id === gamemode) {
                    content.classList.remove('hidden');
                    content.classList.add('active');
                } else {
                    content.classList.add('hidden');
                    content.classList.remove('active');
                }
            });
            
            // Load products for the first category of the gamemode
            const firstCategory = Object.keys(products[gamemode])[0];
            currentCategory = firstCategory;
            loadProducts(gamemode, firstCategory);
        }

        // Load products for a category
        function loadProducts(gamemode, category) {
            if (gamemode === 'survival') {
                const container = document.getElementById('survival-products');
                if (!products.survival[category]) {
                    container.innerHTML = '<p class="text-gray-400 text-center col-span-full">No products available in this category.</p>';
                    return;
                }
                const productList = products.survival[category];
                container.innerHTML = '';
                productList.forEach(product => {
                    const convertedPrice = (product.price * exchangeRates[currentCurrency].rate).toFixed(2);
                    const productElement = document.createElement('div');
                    productElement.className = 'product-card rounded-lg p-6';
                    let viewBtn = '';
                    if (category !== 'coins' && category !== 'keys') {
                        viewBtn = `<button class="minecraft-btn px-4 py-2 rounded text-white view-product" 
                                    data-name="${product.name}" 
                                    data-description="${product.description}">
                                View
                            </button>`;
                    }
                    productElement.innerHTML = `
                        <div class="mb-4">
                            <div class="w-full h-32 bg-gradient-to-r from-blue-600 to-purple-600 rounded-lg flex items-center justify-center mb-4">
                                <i class="fas fa-cube text-white text-4xl"></i>
                            </div>
                            <h3 class="text-xl font-semibold text-white mb-2">${product.name}</h3>
                            <p class="text-gray-300 text-sm mb-4">${product.description}</p>
                        </div>
                        <div class="flex justify-between items-center gap-2">
                            <span class="price-display text-2xl font-bold text-green-400" data-original-price="${product.price}">
                                ${exchangeRates[currentCurrency].symbol}${convertedPrice}
                            </span>
                            <button class="minecraft-btn px-4 py-2 rounded text-white add-to-cart" 
                                    data-id="${product.id}" 
                                    data-name="${product.name}" 
                                    data-price="${product.price}">
                                Add to Cart
                            </button>
                            ${viewBtn}
                        </div>
                    `;
                    container.appendChild(productElement);
                });
            } else {
                const containerId = `${gamemode}-products`;
                const container = document.getElementById(containerId);
                if (!products[gamemode] || !products[gamemode][category]) {
                    container.innerHTML = '<p class="text-gray-400 text-center col-span-full">No products available in this category.</p>';
                    return;
                }
                const productList = products[gamemode][category];
                container.innerHTML = '';
                productList.forEach(product => {
                    const convertedPrice = (product.price * exchangeRates[currentCurrency].rate).toFixed(2);
                    const productElement = document.createElement('div');
                    productElement.className = 'product-card rounded-lg p-6';
                    let viewBtn = '';
                    if (gamemode !== 'pvp') {
                        viewBtn = `<button class="minecraft-btn px-4 py-2 rounded text-white view-product" 
                                    data-name="${product.name}" 
                                    data-description="${product.description}">
                                View
                            </button>`;
                    }
                    productElement.innerHTML = `
                        <div class="mb-4">
                            <div class="w-full h-32 bg-gradient-to-r from-blue-600 to-purple-600 rounded-lg flex items-center justify-center mb-4">
                                <i class="fas fa-cube text-white text-4xl"></i>
                            </div>
                            <h3 class="text-xl font-semibold text-white mb-2">${product.name}</h3>
                            <p class="text-gray-300 text-sm mb-4">${product.description}</p>
                        </div>
                        <div class="flex justify-between items-center gap-2">
                            <span class="price-display text-2xl font-bold text-green-400" data-original-price="${product.price}">
                                ${exchangeRates[currentCurrency].symbol}${convertedPrice}
                            </span>
                            <button class="minecraft-btn px-4 py-2 rounded text-white add-to-cart" 
                                    data-id="${product.id}" 
                                    data-name="${product.name}" 
                                    data-price="${product.price}">
                                Add to Cart
                            </button>
                            ${viewBtn}
                        </div>
                    `;
                    container.appendChild(productElement);
                });
            }
        }

        // Add item to cart
        function addToCart(id, name, price) {
            // Check if item already in cart
            const existingItem = cart.find(item => item.id === id);
            
            if (existingItem) {
                existingItem.quantity += 1;
            } else {
                cart.push({
                    id,
                    name,
                    price,
                    quantity: 1
                });
            }
            
            updateCart();
            showNotification();
        }

        // Update cart UI
        function updateCart() {
            cartItems.innerHTML = '';
            let total = 0;
            let count = 0;
            if (cart.length === 0) {
                cartItems.innerHTML = '<p class="text-gray-400 text-center py-8">Your cart is empty</p>';
            } else {
                cart.forEach(item => {
                    const itemTotal = item.price * item.quantity;
                    total += itemTotal;
                    count += item.quantity;
                    const convertedPrice = (itemTotal * exchangeRates[currentCurrency].rate).toFixed(2);
                    const cartItem = document.createElement('div');
                    cartItem.className = 'flex justify-between items-center py-3 border-b border-gray-700';
                    cartItem.innerHTML = `
                        <div>
                            <h4 class="text-white font-medium">${item.name}</h4>
                            <p class="text-gray-400 text-sm">${exchangeRates[currentCurrency].symbol}${(item.price * exchangeRates[currentCurrency].rate).toFixed(2)} x ${item.quantity}</p>
                        </div>
                        <div class="flex items-center gap-2">
                            <span class="text-green-400 font-semibold">${exchangeRates[currentCurrency].symbol}${convertedPrice}</span>
                            <button class="remove-from-cart text-red-500 hover:text-red-700 ml-2" data-id="${item.id}" title="Remove">&times;</button>
                        </div>
                    `;
                    cartItems.appendChild(cartItem);
                });
            }
            const convertedTotal = (total * exchangeRates[currentCurrency].rate).toFixed(2);
            cartCount.textContent = count;
            cartTotal.textContent = `${exchangeRates[currentCurrency].symbol}${convertedTotal}`;
        }
        // Remove item from cart
        function removeFromCart(id) {
            cart = cart.filter(item => item.id !== id);
            updateCart();
        }

        // Update all prices based on current currency
        function updateAllPrices() {
            // Update product prices
            document.querySelectorAll('.price-display').forEach(element => {
                const originalPrice = parseFloat(element.getAttribute('data-original-price'));
                const convertedPrice = (originalPrice * exchangeRates[currentCurrency].rate).toFixed(2);
                element.textContent = `${exchangeRates[currentCurrency].symbol}${convertedPrice}`;
            });

            // Update cart if it's open
            updateCart();
        }

                // Show add to cart notification
                function showNotification() {
                    cartNotification.classList.remove('hidden');
                    setTimeout(() => {
                        cartNotification.classList.add('hidden');
                    }, 1500);
                }
        
                // Initialize store on page load
        // Product view modal
        function showProductModal(name, description) {
            let modal = document.getElementById('productViewModal');
            // Skyblock rank images
            const skyblockImages = {
                'Vip': 'https://media.discordapp.net/attachments/1329455297751945297/1410095216907784264/Screenshot_2025-08-27_083300.png?ex=68afc502&is=68ae7382&hm=f029776e6e743a36621226141335c7571a5c98273c975cd72236758afc34101b&=&format=webp&quality=lossless',
                'Vip+': 'https://media.discordapp.net/attachments/1329455297751945297/1410095217201123390/Screenshot_2025-08-27_083314.png?ex=68afc502&is=68ae7382&hm=16e3f1ac97c5fcc894a8f4414c5d8c32eeb219328e249147fc64e7e466e86ca0&=&format=webp&quality=lossless',
                'Mvp': 'https://media.discordapp.net/attachments/1329455297751945297/1410095215804551220/Screenshot_2025-08-27_083320.png?ex=68afc501&is=68ae7381&hm=1b510ead89116c7b15388f38d1546f9242ff92079c0e684d34d1c00be19cd2e6&=&format=webp&quality=lossless',
                'Mvp+': 'https://media.discordapp.net/attachments/1329455297751945297/1410095216068661249/Screenshot_2025-08-27_083327.png?ex=68afc501&is=68ae7381&hm=c8a369ec0600c086fb8bfa1f0682fe4459506dd20fe61cba8abee16e11035932&=&format=webp&quality=lossless',
                'Mvp++': 'https://media.discordapp.net/attachments/1329455297751945297/1410095216345612288/Screenshot_2025-08-27_083337.png?ex=68afc501&is=68ae7381&hm=838794fb4a23b7af6abd99b4e690cbd6dc3bd93b4a3a3bd0149a8c35eeea94c8&=&format=webp&quality=lossless'
            };
            let imageHtml = '';
            // Only show image for skyblock ranks
            if (currentGamemode === 'skyblock' && skyblockImages[name]) {
                imageHtml = `<img src="${skyblockImages[name]}" alt="${name} image" class="w-full rounded mb-4">`;
            }
            if (!modal) {
                modal = document.createElement('div');
                modal.id = 'productViewModal';
                modal.className = 'fixed inset-0 flex items-center justify-center bg-black bg-opacity-60 z-50';
                modal.innerHTML = `
                    <div class="bg-gray-900 rounded-lg shadow-lg p-8 max-w-sm w-full relative">
                        <button id="closeProductViewModal" class="absolute top-2 right-2 text-gray-400 hover:text-white text-2xl">&times;</button>
                        <h2 class="text-2xl font-bold text-white mb-4">${name}</h2>
                        ${imageHtml}
                        <p class="text-gray-300 mb-6">${description}</p>
                    </div>
                `;
                document.body.appendChild(modal);
            } else {
                modal.querySelector('h2').textContent = name;
                // Remove any previous image
                const img = modal.querySelector('img');
                if (img) img.remove();
                if (currentGamemode === 'skyblock' && skyblockImages[name]) {
                    const h2 = modal.querySelector('h2');
                    h2.insertAdjacentHTML('afterend', `<img src="${skyblockImages[name]}" alt="${name} image" class="w-full rounded mb-4">`);
                }
                modal.querySelector('p').textContent = description;
                modal.classList.remove('hidden');
            }
            // Close modal
            const closeBtn = document.getElementById('closeProductViewModal');
            closeBtn.onclick = function() {
                modal.classList.add('hidden');
            };
            modal.onclick = function(e) {
                if (e.target === modal) {
                    modal.classList.add('hidden');
                }
            };
        }
                window.addEventListener('DOMContentLoaded', function() {
                    initStore();
                    // Checkout button redirect
                    const checkoutBtn = document.getElementById('checkoutBtn');
                    if (checkoutBtn) {
                        checkoutBtn.addEventListener('click', function() {
                            window.open('https://discord.gg/qcMu56748U', '_blank');
                        });
                    }
                    // Join Server modal logic
                    const joinServerBtn = document.getElementById('joinServerBtn');
                    const joinServerModal = document.getElementById('joinServerModal');
                    const closeJoinServerModal = document.getElementById('closeJoinServerModal');
                    if (joinServerBtn && joinServerModal && closeJoinServerModal) {
                        joinServerBtn.addEventListener('click', function() {
                            joinServerModal.classList.remove('hidden');
                        });
                        closeJoinServerModal.addEventListener('click', function() {
                            joinServerModal.classList.add('hidden');
                        });
                        joinServerModal.addEventListener('click', function(e) {
                            if (e.target === joinServerModal) {
                                joinServerModal.classList.add('hidden');
                            }
                        });
                    }

                    // Copy IP logic for both modal and hero
                    function showCopyNotification() {
                        const notif = document.getElementById('copyNotification');
                        notif.classList.remove('hidden');
                        setTimeout(() => notif.classList.add('hidden'), 1200);
                    }
                    function copyIp(ip) {
                        if (navigator.clipboard) {
                            navigator.clipboard.writeText(ip).then(showCopyNotification);
                        } else {
                            // fallback for old browsers
                            const temp = document.createElement('input');
                            temp.value = ip;
                            document.body.appendChild(temp);
                            temp.select();
                            document.execCommand('copy');
                            document.body.removeChild(temp);
                            showCopyNotification();
                        }
                    }
                    const ipModal = document.getElementById('serverIpModal');
                    if (ipModal) {
                        ipModal.addEventListener('click', function() {
                            copyIp('play.ridemc.fun');
                        });
                    }
                    const ipHero = document.getElementById('serverIpHero');
                    if (ipHero) {
                        ipHero.addEventListener('click', function() {
                            copyIp('play.ridemc.fun');
                        });
                    }
                });
            </script>
        </body>
        </html>
