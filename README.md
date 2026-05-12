<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Velvet Nocturne | Dark Elegance Dresses</title>
    <!-- Google Fonts for modern typography -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,600;14..32,700&family=Playfair+Display:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
    <!-- Font Awesome 6 (free icons) -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background-color: #05050A;
            font-family: 'Inter', sans-serif;
            color: #EAE6E0;
            overflow-x: hidden;
            scroll-behavior: smooth;
        }

        /* custom scrollbar - dark mode */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #0f0f17;
        }
        ::-webkit-scrollbar-thumb {
            background: #c0a06b;
            border-radius: 8px;
        }

        /* animated gradient background (moving mist) */
        .moving-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            background: radial-gradient(circle at 20% 40%, #0c0712, #000000);
            overflow: hidden;
        }

        .moving-bg::before {
            content: "";
            position: absolute;
            width: 200%;
            height: 200%;
            top: -50%;
            left: -50%;
            background: repeating-linear-gradient(
                45deg,
                transparent,
                transparent 40px,
                rgba(80, 50, 100, 0.08) 40px,
                rgba(120, 70, 140, 0.05) 80px
            );
            animation: drift 30s linear infinite;
            pointer-events: none;
        }

        @keyframes drift {
            0% { transform: translate(0, 0) rotate(0deg); }
            100% { transform: translate(60px, 60px) rotate(2deg); }
        }

        /* floating orbs (moving dots/particles) */
        .orb {
            position: fixed;
            border-radius: 50%;
            background: radial-gradient(circle, rgba(200, 160, 110, 0.25), rgba(80, 50, 70, 0));
            filter: blur(40px);
            pointer-events: none;
            z-index: -1;
            animation: floatOrb 16s infinite alternate ease-in-out;
        }

        @keyframes floatOrb {
            0% { transform: translate(0, 0) scale(1); opacity: 0.3; }
            100% { transform: translate(80px, -50px) scale(1.2); opacity: 0.6; }
        }

        /* navigation bar */
        .navbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1.5rem 5%;
            backdrop-filter: blur(12px);
            background: rgba(10, 8, 18, 0.65);
            border-bottom: 1px solid rgba(192, 160, 107, 0.25);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .logo {
            font-family: 'Playfair Display', serif;
            font-size: 1.8rem;
            font-weight: 600;
            letter-spacing: 2px;
            background: linear-gradient(135deg, #F5E7D3, #CFB27C);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
        }

        .nav-links a {
            color: #ddd6cc;
            margin-left: 2rem;
            text-decoration: none;
            font-weight: 500;
            transition: 0.3s;
            font-size: 1rem;
        }

        .nav-links a:hover {
            color: #e7c994;
            text-shadow: 0 0 6px rgba(220, 180, 100, 0.5);
        }

        .hero {
            text-align: center;
            padding: 5rem 1rem 6rem;
        }

        .hero h1 {
            font-family: 'Playfair Display', serif;
            font-size: 3.8rem;
            font-weight: 600;
            letter-spacing: -0.5px;
            background: linear-gradient(120deg, #F3E9DC, #C6A15B);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            text-shadow: 0 2px 20px rgba(0,0,0,0.3);
        }

        .hero p {
            font-size: 1.2rem;
            max-width: 600px;
            margin: 1.2rem auto 0;
            opacity: 0.8;
            letter-spacing: 0.3px;
        }

        /* gallery grid - placeholder for user photos */
        .gallery {
            max-width: 1300px;
            margin: 2rem auto 5rem;
            padding: 0 2rem;
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 2rem;
        }

        .dress-card {
            background: rgba(20, 18, 28, 0.7);
            backdrop-filter: blur(8px);
            border-radius: 28px;
            overflow: hidden;
            border: 1px solid rgba(200, 170, 110, 0.25);
            transition: all 0.4s cubic-bezier(0.2, 0.9, 0.4, 1.1);
            box-shadow: 0 15px 35px rgba(0,0,0,0.5);
            cursor: pointer;
        }

        .dress-card:hover {
            transform: translateY(-10px) scale(1.02);
            border-color: rgba(210, 175, 95, 0.7);
            box-shadow: 0 25px 40px rgba(0,0,0,0.6), 0 0 0 1px rgba(210, 175, 95, 0.3);
        }

        /* image placeholder area – IMAGE SLOT: user will add photos later */
        .img-placeholder {
            width: 100%;
            height: 380px;
            background: #16121f;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
            transition: all 0.3s;
        }

        /* when actual image added via user (img tag), this style covers both */
        .dress-img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.5s ease;
        }

        .dress-card:hover .dress-img {
            transform: scale(1.05);
        }

        /* fallback icon for missing images (user placeholder) */
        .placeholder-icon {
            font-size: 3rem;
            color: #c6a15b;
            background: rgba(0,0,0,0.4);
            padding: 1rem;
            border-radius: 100px;
            backdrop-filter: blur(4px);
        }

        .card-info {
            padding: 1.5rem;
            text-align: center;
        }

        .card-info h3 {
            font-size: 1.4rem;
            font-weight: 500;
            letter-spacing: 1px;
            margin-bottom: 0.5rem;
            color: #f2e2ca;
        }

        .card-info p {
            font-size: 0.9rem;
            opacity: 0.75;
        }

        .price-tag {
            margin-top: 1rem;
            font-weight: 700;
            color: #e0bc7c;
            display: inline-block;
            background: rgba(0,0,0,0.5);
            padding: 0.3rem 1rem;
            border-radius: 40px;
            font-size: 0.9rem;
        }

        /* moving banner: horizontal ticker */
        .moving-ticker {
            background: rgba(0, 0, 0, 0.55);
            backdrop-filter: blur(12px);
            padding: 0.9rem 0;
            margin: 1rem 0 2rem;
            border-top: 1px solid rgba(200, 170, 110, 0.3);
            border-bottom: 1px solid rgba(200, 170, 110, 0.3);
            overflow: hidden;
            white-space: nowrap;
        }

        .ticker-content {
            display: inline-block;
            animation: scrollText 25s linear infinite;
            font-weight: 500;
            letter-spacing: 2px;
            font-size: 1rem;
        }

        .ticker-content span {
            margin: 0 2rem;
            color: #eacc9e;
        }

        .ticker-content i {
            margin: 0 0.8rem;
            color: #b9925c;
        }

        @keyframes scrollText {
            0% { transform: translateX(0%); }
            100% { transform: translateX(-50%); }
        }

        /* additional animated sparks */
        .spark {
            position: fixed;
            width: 3px;
            height: 3px;
            background: #ffdd99;
            border-radius: 50%;
            opacity: 0;
            pointer-events: none;
            z-index: 999;
            box-shadow: 0 0 6px #e2b87a;
            animation: sparkle 1.2s ease-out forwards;
        }

        @keyframes sparkle {
            0% { opacity: 1; transform: scale(1); }
            100% { opacity: 0; transform: translateY(-40px) scale(0.2); }
        }

        footer {
            text-align: center;
            padding: 2.5rem;
            font-size: 0.8rem;
            border-top: 1px solid rgba(150, 120, 80, 0.2);
            margin-top: 2rem;
            background: rgba(0,0,0,0.3);
            backdrop-filter: blur(8px);
        }

        /* responsiveness */
        @media (max-width: 700px) {
            .hero h1 { font-size: 2.5rem; }
            .navbar { flex-direction: column; gap: 1rem; }
            .nav-links a { margin: 0 1rem; }
            .gallery { padding: 0 1rem; gap: 1.5rem; }
        }

        /* instruction note for photo adding */
        .add-note {
            text-align: center;
            background: rgba(30, 25, 40, 0.8);
            width: fit-content;
            margin: 1rem auto 0;
            padding: 0.5rem 1.2rem;
            border-radius: 60px;
            font-size: 0.8rem;
            backdrop-filter: blur(4px);
            color: #bda77a;
        }
        .add-note i {
            margin-right: 6px;
        }
    </style>
</head>
<body>

<div class="moving-bg"></div>

<!-- floating orbs (dynamic moving items) -->
<div class="orb" style="width: 280px; height: 280px; top: 10%; left: -5%; animation-duration: 19s;"></div>
<div class="orb" style="width: 400px; height: 400px; bottom: 0%; right: -10%; background: radial-gradient(circle, rgba(130, 70, 140, 0.2), transparent); animation-duration: 22s;"></div>
<div class="orb" style="width: 200px; height: 200px; top: 40%; left: 70%; animation-duration: 14s; filter: blur(35px);"></div>

<nav class="navbar">
    <div class="logo"><i class="fas fa-crown" style="font-size: 1.4rem; margin-right: 6px;"></i> VELVET NOIR</div>
    <div class="nav-links">
        <a href="#">Atelier</a>
        <a href="#">Collection</a>
        <a href="#">Studio</a>
        <a href="#gallery-main">GALLERY</a>
    </div>
</nav>

<section class="hero">
    <h1>Where shadows weave elegance</h1>
    <p>Dark romanticism — timeless silhouettes, moving grace.<br>Add your own dress photography and let the gallery breathe.</p>
    <div class="add-note">
        <i class="fas fa-upload"></i> Ready for your images — just replace placeholder URLs or add <strong>img src</strong> inside .img-placeholder
    </div>
</section>

<!-- moving ticker (dynamic moving text) -->
<div class="moving-ticker">
    <div class="ticker-content">
        <span><i class="fas fa-star-of-life"></i> HAUTE COUTURE MEETS MIDNIGHT <i class="fas fa-moon"></i></span>
        <span><i class="fas fa-feather-alt"></i> VELVET · SILK · LACE <i class="fas fa-feather-alt"></i></span>
        <span><i class="fas fa-crown"></i> LIMITED EDITIONS — ETHICAL LUXURY</span>
        <span><i class="fas fa-wind"></i> MOVING WITH GRACE <i class="fas fa-gem"></i></span>
        <span><i class="fas fa-star-of-life"></i> HAUTE COUTURE MEETS MIDNIGHT <i class="fas fa-moon"></i></span>
        <span><i class="fas fa-feather-alt"></i> VELVET · SILK · LACE <i class="fas fa-feather-alt"></i></span>
        <span><i class="fas fa-crown"></i> LIMITED EDITIONS — ETHICAL LUXURY</span>
        <span><i class="fas fa-wind"></i> MOVING WITH GRACE <i class="fas fa-gem"></i></span>
    </div>
</div>

<!-- DRESS GALLERY SECTION - user will add photos later. Each card has placeholder area designed for image insertion -->
<div class="gallery" id="gallery-main">
    <!-- Card 1 -->
    <div class="dress-card">
        <div class="img-placeholder" id="imgSlot1">
            <!-- USER PHOTO AREA: Replace the below icon with your <img class="dress-img" src="your-photo.jpg" alt="dress"> -->
            <div class="placeholder-icon">
                <i class="fas fa-camera-retro"></i> <span style="font-size: 0.8rem; display:block;">Add photo</span>
            </div>
        </div>
        <div class="card-info">
            <h3>Midnight Velvet Gown</h3>
            <p>Fluid silhouette, emerald undertones</p>
            <div class="price-tag">€ 429</div>
        </div>
    </div>
    <!-- Card 2 -->
    <div class="dress-card">
        <div class="img-placeholder" id="imgSlot2">
            <div class="placeholder-icon">
                <i class="fas fa-camera-retro"></i> <span style="font-size: 0.8rem; display:block;">Add photo</span>
            </div>
        </div>
        <div class="card-info">
            <h3>Nocturnal Rose Dress</h3>
            <p>Lace appliqué, sheer sleeves</p>
            <div class="price-tag">€ 579</div>
        </div>
    </div>
    <!-- Card 3 -->
    <div class="dress-card">
        <div class="img-placeholder" id="imgSlot3">
            <div class="placeholder-icon">
                <i class="fas fa-camera-retro"></i> <span style="font-size: 0.8rem; display:block;">Add photo</span>
            </div>
        </div>
        <div class="card-info">
            <h3>Stardust Corset Dress</h3>
            <p>Shimmering net, dramatic train</p>
            <div class="price-tag">€ 699</div>
        </div>
    </div>
    <!-- Card 4 -->
    <div class="dress-card">
        <div class="img-placeholder" id="imgSlot4">
            <div class="placeholder-icon">
                <i class="fas fa-camera-retro"></i> <span style="font-size: 0.8rem; display:block;">Add photo</span>
            </div>
        </div>
        <div class="card-info">
            <h3>Onyx Slip Dress</h3>
            <p>Satin charmeuse, minimalist edge</p>
            <div class="price-tag">€ 349</div>
        </div>
    </div>
    <!-- Card 5 -->
    <div class="dress-card">
        <div class="img-placeholder" id="imgSlot5">
            <div class="placeholder-icon">
                <i class="fas fa-camera-retro"></i> <span style="font-size: 0.8rem; display:block;">Add photo</span>
            </div>
        </div>
        <div class="card-info">
            <h3>Raven Feather Gown</h3>
            <p>Dramatic cape detail, pleated bodice</p>
            <div class="price-tag">€ 849</div>
        </div>
    </div>
    <!-- Card 6 -->
    <div class="dress-card">
        <div class="img-placeholder" id="imgSlot6">
            <div class="placeholder-icon">
                <i class="fas fa-camera-retro"></i> <span style="font-size: 0.8rem; display:block;">Add photo</span>
            </div>
        </div>
        <div class="card-info">
            <h3>Dusk Tulle Ballgown</h3>
            <p>Layered tulle, celestial belt</p>
            <div class="price-tag">€ 989</div>
        </div>
    </div>
</div>

<footer>
    <i class="fas fa-feather-alt"></i>  DARK ELEGANCE ATELIER — your images define the vision  <i class="fas fa-feather-alt"></i><br>
    <span style="opacity: 0.5;">© Velvet Nocturne | replace photo placeholders with your dress images</span>
</footer>

<script>
    // 1. ADDITIONAL MOVING SPARKS ON INTERACTION: dynamic moving things (sparkles when clicking / hovering dress cards)
    function createSpark(event) {
        const spark = document.createElement('div');
        spark.classList.add('spark');
        const x = event.clientX;
        const y = event.clientY;
        spark.style.left = x + 'px';
        spark.style.top = y + 'px';
        document.body.appendChild(spark);
        setTimeout(() => {
            spark.remove();
        }, 1000);
    }

    // attach click spark effect to whole document: it's a moving particle effect
    document.addEventListener('click', (e) => {
        createSpark(e);
    });

    // additional hover spark effect on dress cards: while moving mouse on gallery items also produce mini sparks
    const cards = document.querySelectorAll('.dress-card');
    cards.forEach(card => {
        card.addEventListener('mousemove', (e) => {
            // only 10% chance to reduce overload but keep smooth moving items
            if (Math.random() < 0.2) {
                const rect = card.getBoundingClientRect();
                const sparkX = e.clientX;
                const sparkY = e.clientY;
                const sparkDiv = document.createElement('div');
                sparkDiv.classList.add('spark');
                sparkDiv.style.left = sparkX + 'px';
                sparkDiv.style.top = sparkY + 'px';
                sparkDiv.style.width = '2px';
                sparkDiv.style.height = '2px';
                sparkDiv.style.background = '#f5cf8e';
                document.body.appendChild(sparkDiv);
                setTimeout(() => sparkDiv.remove(), 800);
            }
        });
    });

    // 2. automatically give slight parallax move to floating orbs (extra moving dynamic)
    window.addEventListener('mousemove', (e) => {
        const orbs = document.querySelectorAll('.orb');
        const mouseX = e.clientX / window.innerWidth;
        const mouseY = e.clientY / window.innerHeight;
        orbs.forEach((orb, idx) => {
            const moveX = (mouseX - 0.5) * 18 * (idx + 1) * 0.5;
            const moveY = (mouseY - 0.5) * 15 * (idx + 1) * 0.4;
            orb.style.transform = `translate(${moveX}px, ${moveY}px)`;
        });
    });

    // 3. small continuous move effect on ticker content (already moving with css)
    // Plus dynamic addition for image placeholders: easy instruction for user to add actual photos.
    // Below we will create a helper comment, but also we can listen to image replace later? Not required, but convenience:
    // Provide human-readable instructions in console
    console.log("✨ VELVET NOIR: Dark dress website ready — to add YOUR photos:");
    console.log("1. Inside each .img-placeholder (div), replace the placeholder-icon <div> with <img class='dress-img' src='your-image-path.jpg' alt='dress name'>");
    console.log("2. All images will automatically fill the area & maintain hover zoom effects.");
    console.log("3. You can also add background images directly, but we recommend img tags for best animation.");
    
    // optional: preload demo note for gentle guidance on website - interactive preview.
    // we also create a simple small floating guidance popup? not needed, but a dynamic floating instruction can be fun
    const guideMsg = document.createElement('div');
    guideMsg.innerHTML = '<i class="fas fa-magic"></i> Replace placeholder icons with <strong>&lt;img class="dress-img"&gt;</strong> → your photos inherit dark motion design';
    guideMsg.style.position = 'fixed';
    guideMsg.style.bottom = '20px';
    guideMsg.style.right = '20px';
    guideMsg.style.backgroundColor = 'rgba(0,0,0,0.75)';
    guideMsg.style.backdropFilter = 'blur(12px)';
    guideMsg.style.padding = '0.8rem 1.2rem';
    guideMsg.style.borderRadius = '40px';
    guideMsg.style.fontSize = '0.75rem';
    guideMsg.style.borderLeft = '3px solid #c6a15b';
    guideMsg.style.zIndex = '1000';
    guideMsg.style.color = '#f3e5ce';
    guideMsg.style.fontFamily = 'Inter, sans-serif';
    guideMsg.style.pointerEvents = 'none';
    guideMsg.style.opacity = '0.9';
    document.body.appendChild(guideMsg);
    // hide after 7 seconds but keep reference slowly fade
    setTimeout(() => {
        guideMsg.style.transition = 'opacity 1s';
        guideMsg.style.opacity = '0';
        setTimeout(() => guideMsg.remove(), 2000);
    }, 7000);

    // additional interactive moving element: follow-star around mouse on hero area, but optional to keep lightweight
    // create small moving glow effect on images when hover? we have already zoom, but add changing shadow based on mouse?
    const heroes = document.querySelector('.hero');
    if (heroes) {
        heroes.addEventListener('mousemove', function(e) {
            const xAxis = (window.innerWidth / 2 - e.pageX) / 35;
            const yAxis = (window.innerHeight / 2 - e.pageY) / 35;
            document.querySelector('.hero h1').style.transform = `translate(${xAxis * 0.4}px, ${yAxis * 0.2}px)`;
        });
        heroes.addEventListener('mouseleave', () => {
            document.querySelector('.hero h1').style.transform = 'translate(0px, 0px)';
        });
    }

    // For user convenience — explicit example on how to add images: demonstrate with dynamic data but not overwrite user changes.
    // Since they will add images later, we want to keep the placeholder-icons untouched, but we also provide override example via clone modification guidance (no automatic changes)
    // To avoid confusion, we ensure that each card is easily editable. Done

    // small dynamic refresh to add moving "dress" floating text? already fine. Additional subtle rotating movement in background gradient.
    // ensuring that background gradient shifting:
    let rotateBg = 0;
    setInterval(() => {
        rotateBg = (rotateBg + 0.2) % 360;
        const bgLayer = document.querySelector('.moving-bg');
        if (bgLayer) {
            bgLayer.style.background = `radial-gradient(circle at ${35 + Math.sin(Date.now() / 8000) * 10}% ${45 + Math.cos(Date.now() / 7000) * 8}%, #0f081a, #010003)`;
        }
    }, 150);
    
    // preload font and design consistency - also include tooltip for dress images: dynamic onload check whether user replaced image
    window.addEventListener('load', () => {
        const placeholders = document.querySelectorAll('.img-placeholder');
        placeholders.forEach((ph, idx) => {
            // if none img exists, it's placeholder. we just leave it user-friendly.
            if (!ph.querySelector('img')) {
                // but we don't modify, just to notify in console but quiet.
            } else {
                console.log(`Image detected in card ${idx+1} — great! Your photo adapts to dark moving theme.`);
            }
        });
    });
</script>
</body>
</html>
