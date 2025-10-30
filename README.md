
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Voulté — Secure the Look</title>
  <style>
    :root {
      --pink: #f5c6d0;
      --black: #2d2926;
    }

    html,body {
      height:100%;
      margin:0;
      font-family: Inter, Segoe UI, Roboto, Arial, sans-serif;
      background: var(--black);
      color: #fff;
      overflow-x: hidden;
    }

    .container { max-width:1200px; margin:0 auto; padding:24px }
    header {
      display:flex; align-items:center; justify-content:space-between;
      padding:12px 0; border-bottom:3px solid rgba(255,255,255,0.1)
    }
    .logo-text { font-size:2rem; font-weight:800; color:var(--pink); }
    .slogan { font-size:0.9rem; opacity:0.7; margin-top:-4px; }
    nav { display:flex; gap:18px; align-items:center }
    nav a { color:#fff; text-decoration:none; font-weight:600; cursor:pointer; }
    .pill {
      display:inline-block; background:rgba(255,255,255,0.08);
      padding:6px 10px; border-radius:999px; cursor:pointer;
      transition:all 0.2s ease;
    }
    .pill:hover { background: var(--pink); color: var(--black); }

    /* Hero */
    .hero { margin:28px 0; position:relative; overflow: hidden; }
    .hero { height: 80vh; max-height:700px; }
    .hero img { display:block; width:100%; height:100%; object-fit:cover; filter:brightness(0.8) }
    .hero-overlay {
      position:absolute; inset:0; display:flex; flex-direction:column;
      align-items:center; justify-content:center; text-align:center;
    }
    .hero-overlay h1 { font-size:3rem; margin:0; color:var(--pink); text-transform:uppercase; letter-spacing:2px; text-shadow: 0 2px 10px rgba(0,0,0,0.5); }
    .hero-overlay p { margin-top:10px; font-size:1.2rem; opacity:0.8; }

    .coming-soon { text-align:center; font-size:1.8rem; font-weight:700; margin:60px 0 20px; color:var(--pink); }

    /* Notify */
    .notify-section {
      display:flex; flex-direction:column; align-items:center; justify-content:center;
      background:var(--pink); color:var(--black);
      padding:50px 20px; border-radius:24px; width:80%; margin:40px auto; text-align:center;
    }
    .notify-section h2 { margin-bottom:14px; font-size:1.6rem; font-weight:700; letter-spacing:1px; }
    .notify-section p { margin-top:0; margin-bottom:22px; font-size:1rem; opacity:0.85; }
    .notify-form input {
      padding:12px; width:260px; border-radius:999px; border:none; margin-right:8px;
      outline:none; font-size:1rem;
      max-width:90%;
      box-sizing:border-box;
    }
    .notify-btn {
      background: var(--black); color: var(--pink);
      border:none; border-radius:999px; padding:12px 24px; font-weight:600; cursor:pointer;
      transition:background 0.2s ease;
      margin-top:8px;
    }
    .notify-btn:hover { background:#fff; color:var(--black); }

    /* Cart Drawer */
    .cart-overlay {
      position: fixed; top: 0; right: 0; width: 380px; height: 100%;
      background: var(--black); color: #fff; box-shadow: -2px 0 10px rgba(0,0,0,0.6);
      transform: translateX(100%); transition: transform 0.4s ease;
      z-index: 9999; display:flex; flex-direction:column; justify-content:space-between;
    }
    .cart-overlay.open { transform: translateX(0); }
    .cart-header { display:flex; justify-content:space-between; align-items:center; padding:20px; font-weight:700; color:var(--pink); }
    .cart-content { flex:1; display:flex; align-items:center; justify-content:center; opacity:0.8; }
    .checkout-btn { background:var(--pink); color:var(--black); border:none; border-radius:999px; padding:14px 24px; font-weight:700; width:300px; margin:0 auto 30px; }

    footer { margin-top:48px; padding:40px 0; text-align:center; border-top:3px solid rgba(255,255,255,0.06) }
    .socials { display:flex; gap:24px; justify-content:center; margin-top:10px }
    .socials img { width:28px; height:28px; filter:invert(1); opacity:0.9; transition:opacity 0.2s ease; }
    .socials img:hover { opacity:1; }

    /* About popup */
    .about-popup {
      position: fixed; top: 50%; left: 50%;
      transform: translate(-50%, -50%) scale(0.9);
      background: var(--black);
      border: 2px solid var(--pink);
      border-radius: 12px;
      padding: 30px;
      max-width: 400px;
      width: 90%;
      color: #fff;
      text-align: center;
      opacity: 0;
      visibility: hidden;
      transition: all 0.3s ease;
      z-index: 9999;
    }
    .about-popup.open { opacity: 1; visibility: visible; transform: translate(-50%, -50%) scale(1); }
    .about-popup button { background: var(--pink); color: var(--black); border: none; padding: 10px 20px; border-radius: 999px; cursor: pointer; margin-top: 15px; font-weight: 600; }

    /* Help button */
    .help-btn {
      position: fixed; bottom: 24px; right: 24px;
      background: var(--pink); color: var(--black);
      border: none; border-radius: 999px; padding: 12px 20px;
      font-weight: 700; box-shadow: 0 4px 12px rgba(0,0,0,0.4);
      cursor: pointer; transition: all 0.3s ease;
      z-index: 10000;
    }
    .help-btn:hover { background: #fff; transform: scale(1.05); }

    .chat-popup {
      position: fixed; bottom: 80px; right: 24px;
      background: var(--black); border: 2px solid var(--pink);
      border-radius: 16px; width: 320px; padding: 20px;
      display: none; flex-direction: column;
      z-index: 10001; box-shadow: 0 4px 12px rgba(0,0,0,0.6);
    }
    .chat-popup.open { display: flex; }
    .chat-popup h3 { color: var(--pink); margin-top: 0; text-align: center; }
    .chat-popup input, .chat-popup textarea {
      margin-top: 10px; padding: 10px; border-radius: 8px;
      border: 1px solid rgba(255,255,255,0.2); background: transparent; color: #fff;
    }
    .chat-popup button {
      background: var(--pink); color: var(--black);
      border: none; padding: 10px; border-radius: 999px;
      margin-top: 10px; cursor: pointer; font-weight: 700;
    }

    /* Mobile adjustments */
    @media (max-width: 768px) {
      .hero { height: 50vh; }
      .notify-form input { width: 90%; }
      .notify-btn { width: 90%; }
      .cart-overlay { width: 90%; }
    }
  </style>
</head>

<body>
  <div class="container">
    <header>
      <div class="logo">
        <div class="logo-text">Voulté</div>
        <div class="slogan">Secure the Look</div>
      </div>
      <nav>
        <a id="about-btn">About</a>
        <button id="cart-btn" class="pill">Cart (0)</button>
      </nav>
    </header>

    <section class="hero">
      <img src="https://images.unsplash.com/photo-1603252109303-2751441dd157?q=80&w=1600&auto=format&fit=crop" alt="Voulté Fashion">
      <div class="hero-overlay">
        <h1>VOUltÉ</h1>
        <p>Secure the Look</p>
      </div>
    </section>

    <div class="coming-soon">Coming Soon!</div>

    <div class="notify-section">
      <h2>Stay in the Loop</h2>
      <p>Be the first to know when we launch.</p>
      <form id="notify-form" class="notify-form">
        <input type="email" id="notify-email" name="email" placeholder="Enter your email" required>
        <button class="notify-btn" type="submit">Notify Me</button>
      </form>
    </div>

    <footer>
      <div class="socials">
        <a href="https://www.instagram.com/securethelook_?igsh=bmh1MzV5d3ZkamFy&utm_source=qr" target="_blank"><img src="https://cdn.jsdelivr.net/gh/simple-icons/simple-icons/icons/instagram.svg" alt="IG"></a>
        <a href="https://www.tiktok.com/@securethelook?_t=ZN-90xEWpupuRa&_r=1" target="_blank"><img src="https://cdn.jsdelivr.net/gh/simple-icons/simple-icons/icons/tiktok.svg" alt="TT"></a>
        <a href="https://snapchat.com/t/kfABLt2F" target="_blank"><img src="https://cdn.jsdelivr.net/gh/simple-icons/simple-icons/icons/snapchat.svg" alt="SC"></a>
      </div>
      <div style="margin-top:20px;opacity:0.8">© 2025 Voulté — Secure the Look</div>
    </footer>
  </div>

  <div id="cart-overlay" class="cart-overlay" aria-hidden="true">
    <div>
      <div class="cart-header">
        <span>Your Cart</span>
        <button id="close-cart" style="background:none;border:none;color:#fff;font-size:1.2rem;cursor:pointer;">×</button>
      </div>
      <div class="cart-content"><p>Your cart is empty.</p></div>
    </div>
    <button class="checkout-btn">Checkout</button>
  </div>

  <div id="about-popup" class="about-popup" aria-hidden="true">
    <p>This was just a dream and an idea that came true. From 1 person to more and more people. This is Voulté.</p>
    <button id="close-about">Close</button>
  </div>

  <button id="help-btn" class="help-btn" aria-expanded="false">Help</button>

  <div id="chat-popup" class="chat-popup" aria-hidden="true">
    <h3>👋 Our team is here to help you</h3>
    <form id="help-form">
      <input type="text" id="help-name" name="name" placeholder="Your Name" required>
      <input type="email" id="help-email" name="_replyto" placeholder="Your Email" required>
      <textarea id="help-message" name="message" rows="3" placeholder="Your Question" required></textarea>
      <button type="submit">Send</button>
    </form>
  </div>

  <!-- EmailJS SDK + App JS -->
  <script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
  <script>
    // === Replace these with your EmailJS keys ===
    const EMAILJS_PUBLIC_KEY = "YOUR_PUBLIC_KEY";
    const EMAILJS_SERVICE_ID = "YOUR_SERVICE_ID";
    const EMAILJS_NOTIFY_TEMPLATE = "YOUR_NOTIFY_TEMPLATE_ID";
    const EMAILJS_HELP_TEMPLATE = "YOUR_HELP_TEMPLATE_ID";
    // ============================================

    // Init EmailJS
    if (window.emailjs) {
      emailjs.init(EMAILJS_PUBLIC_KEY);
    } else {
      console.warn("EmailJS SDK not loaded.");
    }

    // Buttons / UI
    const cartBtn = document.getElementById('cart-btn');
    const cartOverlay = document.getElementById('cart-overlay');
    const closeCart = document.getElementById('close-cart');

    const aboutBtn = document.getElementById('about-btn');
    const aboutPopup = document.getElementById('about-popup');
    const closeAbout = document.getElementById('close-about');

    const helpBtn = document.getElementById('help-btn');
    const chatPopup = document.getElementById('chat-popup');

    // Safe event wiring
    if (cartBtn && cartOverlay && closeCart) {
      cartBtn.addEventListener('click', () => cartOverlay.classList.add('open'));
      closeCart.addEventListener('click', () => cartOverlay.classList.remove('open'));
    }

    if (aboutBtn && aboutPopup && closeAbout) {
      aboutBtn.addEventListener('click', () => aboutPopup.classList.add('open'));
      closeAbout.addEventListener('click', () => aboutPopup.classList.remove('open'));
    }

    if (helpBtn && chatPopup) {
      helpBtn.addEventListener('click', () => {
        const isOpen = chatPopup.classList.toggle('open');
        helpBtn.setAttribute('aria-expanded', isOpen ? 'true' : 'false');
      });
    }

    // Notify form (EmailJS)
    const notifyForm = document.getElementById('notify-form');
    if (notifyForm) {
      notifyForm.addEventListener('submit', function (e) {
        e.preventDefault();
        const email = document.getElementById('notify-email').value.trim();
        if (!email) return alert('Please enter your email.');

        if (!window.emailjs) {
          alert('Email service not ready. Try again later.');
          return;
        }

        emailjs.send(EMAILJS_SERVICE_ID, EMAILJS_NOTIFY_TEMPLATE, { email })
          .then(() => {
            alert('Thank you! You’ll be notified soon.');
            notifyForm.reset();
          })
          .catch((err) => {
            console.error('EmailJS error (notify):', err);
            alert('Something went wrong. Please try again.');
          });
      });
    }

    // Help form (EmailJS)
    const helpForm = document.getElementById('help-form');
    if (helpForm) {
      helpForm.addEventListener('submit', function (e) {
        e.preventDefault();
        const name = document.getElementById('help-name').value.trim();
        const email = document.getElementById('help-email').value.trim();
        const message = document.getElementById('help-message').value.trim();
        if (!name || !email || !message) return alert('Please fill in all fields.');

        if (!window.emailjs) {
          alert('Email service not ready. Try again later.');
          return;
        }

        emailjs.send(EMAILJS_SERVICE_ID, EMAILJS_HELP_TEMPLATE, {
          from_name: name,
          reply_to: email,
          message: message
        })
        .then(() => {
          alert('Your message was sent! We’ll get back to you soon.');
          helpForm.reset();
          chatPopup.classList.remove('open');
          helpBtn.setAttribute('aria-expanded','false');
        })
        .catch((err) => {
          console.error('EmailJS error (help):', err);
          alert('Error sending message. Please try again.');
        });
      });
    }

    // Hide GitHub auto-title if present (safe removal)
    document.addEventListener('DOMContentLoaded', () => {
      try {
        const topH1 = document.querySelector('body > h1');
        if (topH1 && /voulte|securethelook/i.test(topH1.textContent)) {
          topH1.remove();
        }
      } catch (e) { /* ignore */ }
    });
  </script>
</body>
</html>
