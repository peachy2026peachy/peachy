```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>PEACHY Studio | Clean Girl Aesthetic Store</title>
  
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  
  <!-- React & React DOM CDNs -->
  <script src="https://unpkg.com/react@18/umd/react.production.min.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js" crossorigin></script>
  
  <!-- Babel Standalone for JSX compilation -->
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

  <!-- Lucide Icons CDN -->
  <script src="https://unpkg.com/lucide@latest"></script>

  <!-- Custom Styles & Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400..700;1,400..700&family=Plus+Jakarta+Sans:wght@300;400;500;600;700&display=swap" rel="stylesheet">

  <style>
    body {
      font-family: 'Plus Jakarta Sans', sans-serif;
    }
    .font-serif {
      font-family: 'Playfair Display', serif;
    }
    /* Hide scrollbars for clean aesthetic */
    .scrollbar-none::-webkit-scrollbar {
      display: none;
    }
    .scrollbar-none {
      -ms-overflow-style: none;
      scrollbar-width: none;
    }
  </style>
</head>
<body class="bg-[#FFFBF8] text-[#4A3D39] selection:bg-orange-100 selection:text-orange-700">

  <div id="root"></div>

  <!-- React Code -->
  <script type="text/babel">
    const { useState, useEffect, useMemo } = React;

    const PRODUCTS = [
      {
        id: 'p1',
        name: 'Peachy Glow Dew Serum',
        category: 'Skincare',
        price: 38,
        rating: 4.9,
        reviewsCount: 128,
        tags: ['Bestseller', 'Viral TikTok', 'Clean Girl'],
        image: 'https://images.unsplash.com/photo-1620916566398-39f1143ab7be?auto=format&fit=crop&q=80&w=800',
        secondaryImage: 'https://images.unsplash.com/photo-1608248597261-891963953538?auto=format&fit=crop&q=80&w=800',
        description: 'Ultra-hydrating peach extract serum infused with multi-weight Hyaluronic Acid for that juicy glass-skin finish.',
        details: ['100% Vegan & Cruelty-free', 'Dermatologist Tested', 'Peach Nectar Extract', '30ml / 1 fl. oz.'],
        colors: ['Original Dew'],
        badge: 'Viral'
      },
      {
        id: 'p2',
        name: 'Peach Nectar Mulberry Silk Pillowcase',
        category: 'Silk & Haircare',
        price: 55,
        rating: 5.0,
        reviewsCount: 210,
        tags: ['Bestseller', 'Clean Girl'],
        image: 'https://images.unsplash.com/photo-1616046229478-9901c5536a45?auto=format&fit=crop&q=80&w=800',
        secondaryImage: 'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?auto=format&fit=crop&q=80&w=800',
        description: 'Hypoallergenic 22 Momme grade 6A silk. Keeps hair friction-free and preserves skin hydration overnight.',
        details: ['Grade 6A Mulberry Silk', 'Zipper closure', 'Prevents bedhead & friction creases'],
        colors: ['Peach Cream', 'Blush Tint', 'Cloud White'],
        badge: 'Must Have'
      },
      {
        id: 'p3',
        name: 'Peach Quartz Sculp & Contour Gua Sha',
        category: 'Skincare',
        price: 28,
        rating: 4.8,
        reviewsCount: 84,
        tags: ['Self-Care', 'Viral TikTok'],
        image: 'https://images.unsplash.com/photo-1600428877878-1a0fd85beda8?auto=format&fit=crop&q=80&w=800',
        secondaryImage: 'https://images.unsplash.com/photo-1598440947619-2c35fc9aa908?auto=format&fit=crop&q=80&w=800',
        description: 'Natural hand-carved Peach Quartz stone created to relieve facial tension, drain lymphatics, and sculpt high cheekbones.',
        details: ['100% Authentic Peach Quartz', 'Ergonomic curves', 'Satin pouch included'],
        colors: ['Peach Quartz'],
        badge: null
      },
      {
        id: 'p4',
        name: 'Peachy Cloud Spa Headband Set',
        category: 'Accessories',
        price: 18,
        rating: 4.9,
        reviewsCount: 340,
        tags: ['Clean Girl', 'New'],
        image: 'https://images.unsplash.com/photo-1522337360788-8b13dee7a37e?auto=format&fit=crop&q=80&w=800',
        secondaryImage: 'https://images.unsplash.com/photo-1512496015851-a90fb38ba796?auto=format&fit=crop&q=80&w=800',
        description: 'Plush sponge headband with matching wrist cuffs. Perfect for keeping hair back during your Peachy skincare ritual.',
        details: ['Ultra Soft Microfiber', 'High Absorbency', 'One size fits all'],
        colors: ['Peachy Pink', 'Creamy Vanilla', 'Soft Apricot'],
        badge: 'Popular'
      },
      {
        id: 'p5',
        name: 'Golden Hour Shimmering Peach Body Oil',
        category: 'Skincare',
        price: 42,
        rating: 4.7,
        reviewsCount: 96,
        tags: ['Bestseller', 'Clean Girl'],
        image: 'https://images.unsplash.com/photo-1608248597261-891963953538?auto=format&fit=crop&q=80&w=800',
        secondaryImage: 'https://images.unsplash.com/photo-1620916566398-39f1143ab7be?auto=format&fit=crop&q=80&w=800',
        description: 'Nourishing dry oil with micro-gold specks and peach blossom essence for an all-over sun-kissed radiance.',
        details: ['Jojoba & Argan Base', 'Peach Blossom & Vanilla Fragrance', 'Non-greasy finish'],
        colors: ['Peach Gold'],
        badge: null
      },
      {
        id: 'p6',
        name: 'Peachy Mind Undated Daily Journal',
        category: 'Stationery',
        price: 32,
        rating: 4.9,
        reviewsCount: 77,
        tags: ['New', 'Self-Care'],
        image: 'https://images.unsplash.com/photo-1544716278-ca5e3f4abd8c?auto=format&fit=crop&q=80&w=800',
        secondaryImage: 'https://images.unsplash.com/photo-1517842645767-c639042777db?auto=format&fit=crop&q=80&w=800',
        description: 'Minimalist peach linen planner with morning intention prompts, habit trackers, and gold foil detail.',
        details: ['120gsm Premium Paper', 'Linen hard cover', 'Ribbon marker'],
        colors: ['Peach Linen', 'Blush Velvet'],
        badge: 'New'
      },
      {
        id: 'p7',
        name: 'Dainty Peach Blossom Pearl Necklace',
        category: 'Jewelry',
        price: 48,
        rating: 5.0,
        reviewsCount: 112,
        tags: ['Clean Girl', 'Bestseller'],
        image: 'https://images.unsplash.com/photo-1599643478518-a784e5dc4c8f?auto=format&fit=crop&q=80&w=800',
        secondaryImage: 'https://images.unsplash.com/photo-1535632066927-ab7c9ab60908?auto=format&fit=crop&q=80&w=800',
        description: 'Freshwater pearls layered with a delicate 18k rose gold peach charm. Subtle, elegant, and timeless.',
        details: ['18k Rose Gold Plated', 'Natural Pearls', '14-16" Adjustable length'],
        colors: ['Rose Gold Peach'],
        badge: 'Essential'
      },
      {
        id: 'p8',
        name: 'Sweet Peach & Soft Cashmere Room Mist',
        category: 'Decor',
        price: 34,
        rating: 4.8,
        reviewsCount: 63,
        tags: ['Self-Care'],
        image: 'https://images.unsplash.com/photo-1615397349754-cfa2066a298e?auto=format&fit=crop&q=80&w=800',
        secondaryImage: 'https://images.unsplash.com/photo-1592945403244-b3fbafd7f539?auto=format&fit=crop&q=80&w=800',
        description: 'A delicate room fragrance infused with notes of white peach, coconut water, and velvety cashmere wood.',
        details: ['Essential oil blend', 'Phthalate Free', '100ml Matte Peach Bottle'],
        colors: ['Matte Peach'],
        badge: null
      }
    ];

    const CURRENCIES = {
      USD: { symbol: '$', rate: 1 },
      EUR: { symbol: '€', rate: 0.92 },
      GBP: { symbol: '£', rate: 0.79 }
    };

    const CATEGORIES = [
      { name: 'All Products', icon: '🍑' },
      { name: 'Skincare', icon: '🧴' },
      { name: 'Silk & Haircare', icon: '🎀' },
      { name: 'Decor', icon: '🕯️' },
      { name: 'Stationery', icon: '📖' },
      { name: 'Jewelry', icon: '💎' },
      { name: 'Accessories', icon: '✨' }
    ];

    function App() {
      const [currency, setCurrency] = useState('USD');
      const [selectedCategory, setSelectedCategory] = useState('All Products');
      const [activeFilter, setActiveFilter] = useState('All');
      const [wishlist, setWishlist] = useState([]);
      const [cart, setCart] = useState([]);
      const [isCartOpen, setIsCartOpen] = useState(false);
      const [isSearchOpen, setIsSearchOpen] = useState(false);
      const [searchQuery, setSearchQuery] = useState('');
      const [quickViewProduct, setQuickViewProduct] = useState(null);
      const [toastMessage, setToastMessage] = useState(null);

      const [quizStep, setQuizStep] = useState(0);
      const [quizAnswers, setQuizAnswers] = useState({});
      const [quizResult, setQuizResult] = useState(null);

      useEffect(() => {
        if (window.lucide) {
          window.lucide.createIcons();
        }
      });

      const formatPrice = (priceUSD) => {
        const { symbol, rate } = CURRENCIES[currency];
        return `${symbol}${(priceUSD * rate).toFixed(2)}`;
      };

      const showToast = (msg) => {
        setToastMessage(msg);
        setTimeout(() => setToastMessage(null), 3000);
      };

      const toggleWishlist = (productId) => {
        setWishlist(prev => {
          const exists = prev.includes(productId);
          const updated = exists ? prev.filter(id => id !== productId) : [...prev, productId];
          showToast(exists ? 'Removed from Wishlist' : '🍑 Saved to Peachy Wishlist');
          return updated;
        });
      };

      const addToCart = (product, color = null, quantity = 1) => {
        const selectedColor = color || (product.colors ? product.colors[0] : 'Default');
        setCart(prevCart => {
          const existingIndex = prevCart.findIndex(
            item => item.id === product.id && item.selectedColor === selectedColor
          );
          if (existingIndex > -1) {
            const updated = [...prevCart];
            updated[existingIndex].quantity += quantity;
            return updated;
          }
          return [...prevCart, { ...product, selectedColor, quantity }];
        });
        showToast(`🛍️ Added ${product.name} to Cart`);
      };

      const updateCartQuantity = (index, delta) => {
        setCart(prevCart => {
          const updated = [...prevCart];
          const newQty = updated[index].quantity + delta;
          if (newQty <= 0) {
            updated.splice(index, 1);
          } else {
            updated[index].quantity = newQty;
          }
          return updated;
        });
      };

      const cartTotal = useMemo(() => {
        return cart.reduce((sum, item) => sum + item.price * item.quantity, 0);
      }, [cart]);

      const freeShippingThreshold = 60;
      const progressToFreeShipping = Math.min(100, (cartTotal / freeShippingThreshold) * 100);

      const filteredProducts = useMemo(() => {
        return PRODUCTS.filter(product => {
          const matchesCategory = selectedCategory === 'All Products' || product.category === selectedCategory;
          const matchesTag = activeFilter === 'All' || product.tags.includes(activeFilter);
          const matchesSearch = searchQuery === '' || 
            product.name.toLowerCase().includes(searchQuery.toLowerCase()) ||
            product.description.toLowerCase().includes(searchQuery.toLowerCase());
          return matchesCategory && matchesTag && matchesSearch;
        });
      }, [selectedCategory, activeFilter, searchQuery]);

      const handleQuizSubmit = (answers) => {
        setQuizAnswers(answers);
        let recommendedIds = ['p1', 'p2'];
        if (answers.vibe === 'Glow') recommendedIds = ['p1', 'p5', 'p3'];
        else if (answers.vibe === 'Cozy') recommendedIds = ['p2', 'p8', 'p6'];
        else recommendedIds = ['p4', 'p7', 'p1'];

        const bundle = PRODUCTS.filter(p => recommendedIds.includes(p.id));
        setQuizResult(bundle);
      };

      return (
        <div className="min-h-screen relative overflow-x-hidden">

          {/* Ambient Glow Orbs */}
          <div className="fixed -top-40 -left-40 w-96 h-96 bg-orange-200/40 rounded-full blur-3xl pointer-events-none z-0" />
          <div className="fixed top-1/2 -right-40 w-96 h-96 bg-rose-100/50 rounded-full blur-3xl pointer-events-none z-0" />

          {/* Header */}
          <div className="sticky top-0 z-40 backdrop-blur-md bg-white/85 border-b border-orange-100/80 shadow-xs">
            <div className="bg-gradient-to-r from-orange-100 via-rose-100 to-amber-100 py-2 px-4 text-center text-xs tracking-wider text-amber-900 font-medium flex items-center justify-center gap-2">
              <span>🍑 Welcome to PEACHY STUDIO | Use code <strong>PEACHY10</strong> for 10% off your first ritual 🍑</span>
            </div>

            <header className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
              <a href="#" className="font-serif text-2xl sm:text-3xl font-light tracking-widest text-slate-800 hover:opacity-80 transition flex items-center gap-1.5">
                PEACHY <span className="italic text-xs tracking-normal font-sans text-orange-400 border border-orange-200 px-2 py-0.5 rounded-full uppercase">Studio</span>
              </a>

              <nav className="hidden md:flex items-center space-x-8 text-sm font-medium text-slate-600 tracking-wide">
                {CATEGORIES.slice(0, 6).map(cat => (
                  <button
                    key={cat.name}
                    onClick={() => setSelectedCategory(cat.name)}
                    className={`transition-all duration-200 hover:text-orange-500 relative py-1 ${
                      selectedCategory === cat.name ? 'text-orange-500 font-semibold' : ''
                    }`}
                  >
                    {cat.name}
                    {selectedCategory === cat.name && (
                      <span className="absolute bottom-0 left-0 w-full h-0.5 bg-orange-400 rounded-full" />
                    )}
                  </button>
                ))}
              </nav>

              <div className="flex items-center gap-3 sm:gap-4">
                <div className="hidden sm:flex items-center gap-1 text-xs bg-orange-50/70 px-2.5 py-1.5 rounded-full border border-orange-100">
                  <select 
                    value={currency} 
                    onChange={(e) => setCurrency(e.target.value)}
                    className="bg-transparent font-medium text-slate-700 outline-none cursor-pointer"
                  >
                    {Object.keys(CURRENCIES).map(curr => (
                      <option key={curr} value={curr}>{curr} ({CURRENCIES[curr].symbol})</option>
                    ))}
                  </select>
                </div>

                <button 
                  onClick={() => setIsSearchOpen(true)}
                  className="p-2 text-slate-600 hover:text-orange-500 hover:bg-orange-50 rounded-full transition"
                >
                  <i data-lucide="search" className="w-5 h-5"></i>
                </button>

                <button 
                  className="p-2 text-slate-600 hover:text-orange-500 hover:bg-orange-50 rounded-full transition relative"
                  onClick={() => showToast(`❤️ You have ${wishlist.length} saved items`)}
                >
                  <i data-lucide="heart" className={`w-5 h-5 ${wishlist.length > 0 ? "fill-orange-400 text-orange-400" : ""}`}></i>
                  {wishlist.length > 0 && (
                    <span className="absolute top-1 right-1 bg-orange-400 text-white text-[10px] w-4 h-4 rounded-full flex items-center justify-center font-bold">
                      {wishlist.length}
                    </span>
                  )}
                </button>

                <button 
                  onClick={() => setIsCartOpen(true)}
                  className="p-2 bg-gradient-to-r from-orange-400 to-rose-400 text-white rounded-full transition hover:shadow-lg hover:shadow-orange-200/60 relative flex items-center justify-center px-3.5 gap-1.5"
                >
                  <i data-lucide="shopping-bag" className="w-4 h-4"></i>
                  <span className="text-xs font-medium">{cart.reduce((a, b) => a + b.quantity, 0)}</span>
                </button>
              </div>
            </header>
          </div>

          {/* Hero Section */}
          <section className="relative pt-12 pb-20 md:pt-20 md:pb-32 overflow-hidden">
            <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
              <div className="grid grid-cols-1 lg:grid-cols-12 gap-12 items-center">
                
                <div className="lg:col-span-7 space-y-6 text-center lg:text-left">
                  <div className="inline-flex items-center gap-2 px-4 py-1.5 rounded-full bg-orange-100/80 border border-orange-200 text-amber-900 text-xs tracking-wider uppercase font-medium">
                    🍑 Peachy Clean Girl Aesthetics
                  </div>

                  <h1 className="text-4xl sm:text-6xl font-serif text-slate-800 leading-[1.15] font-light">
                    Feel Naturally <br />
                    <span className="italic font-normal bg-gradient-to-r from-orange-400 via-rose-400 to-amber-400 bg-clip-text text-transparent">
                      Soft, Dewy & Peachy
                    </span>
                  </h1>

                  <p className="text-slate-600 text-base sm:text-lg max-w-xl mx-auto lg:mx-0 leading-relaxed font-light">
                    Welcome to <strong>PEACHY</strong>. Discover a dreamy collection of peach-infused skincare, mulberry silk, glowing decor, and soft minimalist accessories made for your daily self-love rituals.
                  </p>

                  <div className="pt-2 flex flex-col sm:flex-row items-center justify-center lg:justify-start gap-4">
                    <a 
                      href="#catalog" 
                      className="w-full sm:w-auto px-8 py-4 bg-slate-900 text-white rounded-full hover:bg-orange-500 transition-all duration-300 shadow-lg shadow-orange-100 font-medium text-sm tracking-wider flex items-center justify-center gap-2 group"
                    >
                      Shop Peachy Drops
                    </a>

                    <a 
                      href="#quiz" 
                      className="w-full sm:w-auto px-8 py-4 bg-white/80 border border-orange-200 text-slate-700 rounded-full hover:bg-orange-50 transition-all duration-300 text-sm font-medium tracking-wider flex items-center justify-center gap-2"
                    >
                      🍑 Take Routine Quiz
                    </a>
                  </div>
                </div>

                <div className="lg:col-span-5 relative">
                  <div className="relative mx-auto max-w-sm sm:max-w-md">
                    <div className="relative rounded-3xl overflow-hidden shadow-2xl border-4 border-white/60">
                      <img 
                        src="https://images.unsplash.com/photo-1522337360788-8b13dee7a37e?auto=format&fit=crop&q=80&w=800" 
                        alt="Peachy Aesthetics"
                        className="w-full h-[440px] object-cover"
                      />
                    </div>
                  </div>
                </div>

              </div>
            </div>
          </section>

          {/* Product Grid */}
          <section id="catalog" className="py-16 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div className="flex flex-col md:flex-row md:items-end justify-between mb-10 gap-4 border-b border-orange-100 pb-6">
              <div>
                <h2 className="text-3xl sm:text-4xl font-serif text-slate-800 font-light">
                  Peachy <span className="italic font-normal text-orange-400">Favorites</span>
                </h2>
                <p className="text-slate-500 text-sm mt-1">Nourishing formulas and peach-toned luxuries.</p>
              </div>

              <div className="flex items-center gap-2 overflow-x-auto pb-1">
                {['All', 'Bestseller', 'Viral TikTok', 'Clean Girl', 'New'].map(tag => (
                  <button
                    key={tag}
                    onClick={() => setActiveFilter(tag)}
                    className={`px-3.5 py-1.5 rounded-full text-xs font-medium transition ${
                      activeFilter === tag
                        ? 'bg-slate-800 text-white'
                        : 'bg-orange-50 text-slate-600 hover:bg-orange-100'
                    }`}
                  >
                    {tag}
                  </button>
                ))}
              </div>
            </div>

            <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
              {filteredProducts.map((product) => (
                <div 
                  key={product.id}
                  className="bg-white rounded-3xl border border-orange-100/80 overflow-hidden hover:shadow-xl transition-all duration-300 flex flex-col relative"
                >
                  <button
                    onClick={() => toggleWishlist(product.id)}
                    className="absolute top-3 right-3 z-10 p-2 rounded-full bg-white/80 text-slate-400 hover:text-orange-500"
                  >
                    <i data-lucide="heart" className={`w-4 h-4 ${wishlist.includes(product.id) ? "fill-orange-400 text-orange-400" : ""}`}></i>
                  </button>

                  <div className="relative h-64 overflow-hidden bg-orange-50/30 cursor-pointer" onClick={() => setQuickViewProduct(product)}>
                    <img src={product.image} alt={product.name} className="w-full h-full object-cover" />
                  </div>

                  <div className="p-5 flex-1 flex flex-col justify-between space-y-3">
                    <div>
                      <span className="text-[11px] text-slate-400 mb-1 block">{product.category}</span>
                      <h3 onClick={() => setQuickViewProduct(product)} className="font-medium text-slate-800 text-sm hover:text-orange-500 cursor-pointer line-clamp-1">
                        {product.name}
                      </h3>
                    </div>

                    <div className="flex items-center justify-between pt-2 border-t border-orange-50">
                      <span className="font-serif text-lg font-semibold text-slate-800">
                        {formatPrice(product.price)}
                      </span>

                      <button
                        onClick={() => addToCart(product)}
                        className="px-4 py-2 bg-orange-100/80 text-orange-800 hover:bg-orange-400 hover:text-white rounded-full text-xs font-medium transition"
                      >
                        + Add
                      </button>
                    </div>
                  </div>
                </div>
              ))}
            </div>
          </section>

          {/* Cart Drawer */}
          {isCartOpen && (
            <div className="fixed inset-0 z-50 flex justify-end">
              <div onClick={() => setIsCartOpen(false)} className="fixed inset-0 bg-slate-900/30 backdrop-blur-xs" />

              <div className="relative w-full max-w-md bg-white h-full shadow-2xl flex flex-col z-10 border-l border-orange-100">
                <div className="p-5 border-b border-orange-100 flex items-center justify-between bg-orange-50/40">
                  <h3 className="font-serif text-lg text-slate-800 font-semibold">Your Peachy Bag ({cart.length})</h3>
                  <button onClick={() => setIsCartOpen(false)} className="p-1 text-slate-400 hover:text-slate-800">
                    <i data-lucide="x" className="w-5 h-5"></i>
                  </button>
                </div>

                <div className="flex-1 overflow-y-auto p-5 space-y-4">
                  {cart.length === 0 ? (
                    <div className="text-center py-16 text-slate-400 text-xs">Your bag is empty.</div>
                  ) : (
                    cart.map((item, idx) => (
                      <div key={idx} className="flex gap-4 p-3 bg-white border border-orange-100 rounded-2xl">
                        <img src={item.image} alt={item.name} className="w-16 h-16 object-cover rounded-xl" />
                        <div className="flex-1 flex flex-col justify-between">
                          <p className="text-xs font-semibold text-slate-800 line-clamp-1">{item.name}</p>
                          <div className="flex items-center justify-between mt-2">
                            <span className="text-xs font-semibold">{item.quantity} x {formatPrice(item.price)}</span>
                          </div>
                        </div>
                      </div>
                    ))
                  )}
                </div>

                {cart.length > 0 && (
                  <div className="p-5 border-t border-orange-100 bg-white space-y-4">
                    <div className="flex justify-between items-center text-sm font-semibold text-slate-800">
                      <span>Subtotal</span>
                      <span className="font-serif text-lg">{formatPrice(cartTotal)}</span>
                    </div>

                    <button 
                      onClick={() => showToast('🍑 Redirecting to Peachy checkout...')}
                      className="w-full py-3.5 bg-slate-900 text-white rounded-full text-xs font-semibold uppercase tracking-wider hover:bg-orange-500 transition shadow-lg"
                    >
                      Checkout • {formatPrice(cartTotal)}
                    </button>
                  </div>
                )}
              </div>
            </div>
          )}

          {/* Quick View Modal */}
          {quickViewProduct && (
            <div className="fixed inset-0 z-50 flex items-center justify-center p-4">
              <div onClick={() => setQuickViewProduct(null)} className="fixed inset-0 bg-slate-900/40 backdrop-blur-xs" />
              
              <div className="bg-white rounded-3xl max-w-lg w-full p-6 relative z-10 shadow-2xl border border-orange-100">
                <button onClick={() => setQuickViewProduct(null)} className="absolute top-4 right-4 text-slate-400 hover:text-slate-800">
                  <i data-lucide="x" className="w-5 h-5"></i>
                </button>

                <div className="space-y-4">
                  <img src={quickViewProduct.image} alt={quickViewProduct.name} className="w-full h-60 object-cover rounded-2xl" />
                  <h3 className="text-xl font-serif font-semibold text-slate-800">{quickViewProduct.name}</h3>
                  <p className="text-2xl font-serif text-orange-500">{formatPrice(quickViewProduct.price)}</p>
                  <p className="text-xs text-slate-500">{quickViewProduct.description}</p>

                  <button
                    onClick={() => {
                      addToCart(quickViewProduct);
                      setQuickViewProduct(null);
                    }}
                    className="w-full py-3 bg-orange-400 text-white rounded-full text-xs font-semibold hover:bg-orange-500 transition"
                  >
                    Add to Peachy Bag
                  </button>
                </div>
              </div>
            </div>
          )}

          {/* Toast */}
          {toastMessage && (
            <div className="fixed bottom-6 right-6 z-50 bg-slate-900 text-white px-5 py-3 rounded-2xl shadow-xl text-xs font-medium">
              {toastMessage}
            </div>
          )}

        </div>
      );
    }

    ReactDOM.createRoot(document.getElementById('root')).render(<App />);
  </script>
</body>
</html>
```