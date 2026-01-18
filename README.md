<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🌟 Nazmus Sakib | CTO & Web Development Secretary</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/loaders/GLTFLoader.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/controls/OrbitControls.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
            color: #fff;
            min-height: 100vh;
            overflow-x: hidden;
            perspective: 1000px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 2;
        }
        
        /* 3D Background Canvas */
        #bg-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
        }
        
        /* Floating Particles */
        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }
        
        .particle {
            position: absolute;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.2);
        }
        
        /* Header Section */
        .header {
            text-align: center;
            padding: 40px 0;
            margin-bottom: 40px;
            transform-style: preserve-3d;
            animation: float 6s ease-in-out infinite;
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0px) rotateY(0deg); }
            50% { transform: translateY(-20px) rotateY(5deg); }
        }
        
        .profile-title {
            font-size: 3.5rem;
            background: linear-gradient(90deg, #ff8a00, #e52e71, #9d4edd);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 10px;
            text-shadow: 0 0 30px rgba(157, 78, 221, 0.5);
            letter-spacing: 1px;
        }
        
        .profile-subtitle {
            font-size: 1.5rem;
            color: #a8a8e6;
            margin-bottom: 30px;
        }
        
        /* Roles Section with 3D Card */
        .roles-section {
            margin: 50px 0;
            transform-style: preserve-3d;
            transition: transform 0.5s;
        }
        
        .section-title {
            font-size: 2.2rem;
            text-align: center;
            margin-bottom: 30px;
            color: #ff8a00;
            text-shadow: 0 0 15px rgba(255, 138, 0, 0.5);
        }
        
        .roles-container {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 30px;
            perspective: 1000px;
        }
        
        .role-card {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 20px;
            padding: 25px;
            width: 300px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
            transform-style: preserve-3d;
            transition: all 0.5s ease;
            position: relative;
            overflow: hidden;
        }
        
        .role-card:hover {
            transform: translateY(-15px) rotateX(5deg);
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.3);
            border-color: #ff8a00;
        }
        
        .role-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
            transition: 0.5s;
        }
        
        .role-card:hover::before {
            left: 100%;
        }
        
        .role-title {
            font-size: 1.8rem;
            margin-bottom: 10px;
            color: #ff8a00;
        }
        
        .role-org {
            font-size: 1.2rem;
            color: #a8a8e6;
            margin-bottom: 15px;
        }
        
        .role-term {
            font-size: 1rem;
            color: #9d9dff;
            font-style: italic;
        }
        
        /* Skills Section with 3D Spheres */
        .skills-section {
            margin: 60px 0;
        }
        
        .skills-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 20px;
            perspective: 1000px;
        }
        
        .skill-sphere {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            background: rgba(255, 255, 255, 0.05);
            border: 2px solid transparent;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
            transform-style: preserve-3d;
            transition: all 0.5s ease;
            position: relative;
            overflow: hidden;
        }
        
        .skill-sphere:hover {
            transform: scale(1.1) rotateY(20deg);
            border-color: #e52e71;
            box-shadow: 0 15px 30px rgba(229, 46, 113, 0.3);
        }
        
        .skill-icon {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        
        .skill-name {
            font-size: 0.9rem;
            text-align: center;
        }
        
        /* GitHub Stats Section */
        .github-section {
            margin: 60px 0;
        }
        
        .stats-container {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 30px;
            perspective: 1000px;
        }
        
        .stat-card {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 20px;
            width: 250px;
            text-align: center;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transform-style: preserve-3d;
            transition: all 0.5s ease;
            position: relative;
            overflow: hidden;
        }
        
        .stat-card:hover {
            transform: translateZ(20px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
        }
        
        .stat-value {
            font-size: 2.5rem;
            font-weight: bold;
            background: linear-gradient(90deg, #ff8a00, #e52e71);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin: 10px 0;
        }
        
        .stat-label {
            font-size: 1.1rem;
            color: #a8a8e6;
        }
        
        /* Contact Section */
        .contact-section {
            margin: 60px 0;
            text-align: center;
        }
        
        .contact-container {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 30px;
            perspective: 1000px;
        }
        
        .contact-card {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 25px;
            width: 300px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transform-style: preserve-3d;
            transition: all 0.5s ease;
            position: relative;
            overflow: hidden;
        }
        
        .contact-card:hover {
            transform: translateY(-10px) rotateX(5deg);
            border-color: #9d4edd;
        }
        
        .contact-icon {
            font-size: 2.5rem;
            margin-bottom: 15px;
            color: #9d4edd;
        }
        
        .contact-title {
            font-size: 1.5rem;
            margin-bottom: 10px;
            color: #ff8a00;
        }
        
        .contact-link {
            color: #a8a8e6;
            text-decoration: none;
            font-size: 1.1rem;
            display: inline-block;
            margin-top: 10px;
            transition: color 0.3s;
        }
        
        .contact-link:hover {
            color: #ff8a00;
            text-decoration: underline;
        }
        
        /* Social Media Section */
        .social-section {
            margin: 60px 0;
            text-align: center;
        }
        
        .social-icons {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 25px;
            perspective: 1000px;
        }
        
        .social-icon {
            width: 70px;
            height: 70px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.8rem;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transform-style: preserve-3d;
            transition: all 0.5s ease;
            position: relative;
            overflow: hidden;
        }
        
        .social-icon:hover {
            transform: scale(1.2) translateZ(20px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
        }
        
        .social-icon.facebook:hover {
            background: #1877F2;
        }
        
        .social-icon.instagram:hover {
            background: linear-gradient(45deg, #405DE6, #5851DB, #833AB4, #C13584, #E1306C, #FD1D1D);
        }
        
        .social-icon.linkedin:hover {
            background: #0A66C2;
        }
        
        .social-icon.twitter:hover {
            background: #000000;
        }
        
        /* 3D Floating Elements */
        .floating-element {
            position: absolute;
            width: 50px;
            height: 50px;
            border-radius: 10px;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
            z-index: 1;
            transform-style: preserve-3d;
            animation: floatElement 15s infinite linear;
        }
        
        @keyframes floatElement {
            0% { transform: translateY(0) rotate(0deg); }
            100% { transform: translateY(-1000px) rotate(720deg); }
        }
        
        /* Footer */
        .footer {
            text-align: center;
            padding: 40px 0;
            color: #a8a8e6;
            font-size: 1rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            margin-top: 60px;
        }
        
        /* Responsive Design */
        @media (max-width: 768px) {
            .container {
                padding: 15px;
            }
            
            .profile-title {
                font-size: 2.5rem;
            }
            
            .profile-subtitle {
                font-size: 1.2rem;
            }
            
            .section-title {
                font-size: 1.8rem;
            }
            
            .role-card, .contact-card {
                width: 100%;
                max-width: 400px;
            }
            
            .skill-sphere {
                width: 100px;
                height: 100px;
            }
        }
    </style>
</head>
<body>
    <!-- 3D Background Canvas -->
    <canvas id="bg-canvas"></canvas>
    
    <!-- Floating Particles -->
    <div class="particles" id="particles"></div>
    
    <!-- 3D Floating Elements -->
    <div class="floating-elements"></div>
    
    <div class="container">
        <!-- Header Section -->
        <header class="header">
            <h1 class="profile-title">🌟 Nazmus Sakib</h1>
            <h2 class="profile-subtitle">Chief Technology Officer & Secretary of Web Development</h2>
        </header>
        
        <!-- Roles Section -->
        <section class="roles-section">
            <h2 class="section-title">💼 Leadership & Professional Roles</h2>
            <div class="roles-container">
                <div class="role-card">
                    <h3 class="role-title">Chief Technology Officer (CTO)</h3>
                    <p class="role-org">FabTech.IT</p>
                    <p class="role-term">Present</p>
                </div>
                <div class="role-card">
                    <h3 class="role-title">Secretary of Web Development</h3>
                    <p class="role-org">NUB Computer Club - NUBCC</p>
                    <p class="role-term">2025-2026</p>
                </div>
            </div>
        </section>
        
        <!-- Skills Section -->
        <section class="skills-section">
            <h2 class="section-title">💻 Full-Stack Expertise</h2>
            <p style="text-align: center; margin-bottom: 30px; color: #a8a8e6; max-width: 800px; margin-left: auto; margin-right: auto;">
                I am a dedicated <strong>Web developer</strong> with deep expertise in the <strong>React.js</strong> frontend ecosystem and the powerful <strong>Laravel</strong> PHP framework on the backend. My core focus is on <strong>advanced Web development</strong> and engaging in complex <strong>problem-solving projects</strong>.
            </p>
            
            <h3 class="section-title" style="font-size: 1.8rem; margin-top: 40px;">Frontend Technologies</h3>
            <div class="skills-container">
                <div class="skill-sphere">
                    <div class="skill-icon"><i class="fab fa-react"></i></div>
                    <div class="skill-name">React.js</div>
                </div>
                <div class="skill-sphere">
                    <div class="skill-icon"><i class="fab fa-js"></i></div>
                    <div class="skill-name">JavaScript</div>
                </div>
                <div class="skill-sphere">
                    <div class="skill-icon"><i class="fab fa-html5"></i></div>
                    <div class="skill-name">HTML5</div>
                </div>
                <div class="skill-sphere">
                    <div class="skill-icon"><i class="fab fa-css3-alt"></i></div>
                    <div class="skill-name">CSS3</div>
                </div>
                <div class="skill-sphere">
                    <div class="skill-icon"><i class="fab fa-bootstrap"></i></div>
                    <div class="skill-name">Tailwind</div>
                </div>
            </div>
            
            <h3 class="section-title" style="font-size: 1.8rem; margin-top: 40px;">Backend & Database</h3>
            <div class="skills-container">
                <div class="skill-sphere">
                    <div class="skill-icon"><i class="fab fa-laravel"></i></div>
                    <div class="skill-name">Laravel</div>
                </div>
                <div class="skill-sphere">
                    <div class="skill-icon"><i class="fab fa-node-js"></i></div>
                    <div class="skill-name">Node.js</div>
                </div>
                <div class="skill-sphere">
                    <div class="skill-icon"><i class="fab fa-php"></i></div>
                    <div class="skill-name">PHP</div>
                </div>
                <div class="skill-sphere">
                    <div class="skill-icon"><i class="fas fa-database"></i></div>
                    <div class="skill-name">MySQL</div>
                </div>
                <div class="skill-sphere">
                    <div class="skill-icon"><i class="fas fa-server"></i></div>
                    <div class="skill-name">MongoDB</div>
                </div>
            </div>
            
            <h3 class="section-title" style="font-size: 1.8rem; margin-top: 40px;">Programming Languages</h3>
            <div class="skills-container">
                <div class="skill-sphere">
                    <div class="skill-icon"><i class="fas fa-c"></i></div>
                    <div class="skill-name">C</div>
                </div>
                <div class="skill-sphere">
                    <div class="skill-icon"><i class="fas fa-code"></i></div>
                    <div class="skill-name">C++</div>
                </div>
                <div class="skill-sphere">
                    <div class="skill-icon"><i class="fab fa-java"></i></div>
                    <div class="skill-name">Java</div>
                </div>
                <div class="skill-sphere">
                    <div class="skill-icon"><i class="fab fa-python"></i></div>
                    <div class="skill-name">Python</div>
                </div>
            </div>
        </section>
        
        <!-- GitHub Stats Section -->
        <section class="github-section">
            <h2 class="section-title">📊 My GitHub Dynamics</h2>
            <div class="stats-container">
                <div class="stat-card">
                    <div class="stat-label">Total Contributions</div>
                    <div class="stat-value">1,247</div>
                    <div class="stat-desc">Last Year</div>
                </div>
                <div class="stat-card">
                    <div class="stat-label">Repositories</div>
                    <div class="stat-value">48</div>
                    <div class="stat-desc">Public & Private</div>
                </div>
                <div class="stat-card">
                    <div class="stat-label">Streak</div>
                    <div class="stat-value">126</div>
                    <div class="stat-desc">Days</div>
                </div>
                <div class="stat-card">
                    <div class="stat-label">Followers</div>
                    <div class="stat-value">89</div>
                    <div class="stat-desc">GitHub Community</div>
                </div>
            </div>
        </section>
        
        <!-- Contact Section -->
        <section class="contact-section">
            <h2 class="section-title">🤝 Collaboration & Contact</h2>
            <p style="text-align: center; margin-bottom: 30px; color: #a8a8e6; max-width: 800px; margin-left: auto; margin-right: auto;">
                I am actively looking to collaborate on projects involving <strong>problem-solving</strong>, <strong>innovation</strong>, and new <strong>technology development</strong>.
            </p>
            <div class="contact-container">
                <div class="contact-card">
                    <div class="contact-icon"><i class="fab fa-whatsapp"></i></div>
                    <h3 class="contact-title">WhatsApp</h3>
                    <p>Direct messaging for quick communication</p>
                    <a href="https://wa.me/01313186576" class="contact-link">+880 1313-186576</a>
                </div>
                <div class="contact-card">
                    <div class="contact-icon"><i class="fab fa-linkedin"></i></div>
                    <h3 class="contact-title">LinkedIn</h3>
                    <p>Professional networking and collaboration</p>
                    <a href="https://www.linkedin.com/in/nazmus-sakib-303345241/" class="contact-link">Connect with me</a>
                </div>
            </div>
        </section>
        
        <!-- Social Media Section -->
        <section class="social-section">
            <h2 class="section-title">🌐 Social Media Presence</h2>
            <div class="social-icons">
                <a href="https://www.facebook.com/profile.php?id=100058835270925" class="social-icon facebook">
                    <i class="fab fa-facebook-f"></i>
                </a>
                <a href="https://www.instagram.com/nazmus12_arish12/" class="social-icon instagram">
                    <i class="fab fa-instagram"></i>
                </a>
                <a href="https://www.linkedin.com/in/nazmus-sakib-303345241/" class="social-icon linkedin">
                    <i class="fab fa-linkedin-in"></i>
                </a>
                <a href="https://x.com/Nazmussakib1432" class="social-icon twitter">
                    <i class="fab fa-twitter"></i>
                </a>
                <a href="https://github.com/NazmusSakib2036" class="social-icon" style="color: #fff;">
                    <i class="fab fa-github"></i>
                </a>
            </div>
        </section>
        
        <!-- Footer -->
        <footer class="footer">
            <p>© 2025 Nazmus Sakib | All Rights Reserved</p>
            <p style="margin-top: 10px; font-size: 0.9rem;">Designed with ❤️ for GitHub Profile</p>
        </footer>
    </div>
    
    <script>
        // Create floating particles
        function createParticles() {
            const particlesContainer = document.getElementById('particles');
            const particleCount = 50;
            
            for (let i = 0; i < particleCount; i++) {
                const particle = document.createElement('div');
                particle.classList.add('particle');
                
                // Random size
                const size = Math.random() * 5 + 2;
                particle.style.width = `${size}px`;
                particle.style.height = `${size}px`;
                
                // Random position
                particle.style.left = `${Math.random() * 100}%`;
                particle.style.top = `${Math.random() * 100}%`;
                
                // Random animation
                const duration = Math.random() * 20 + 10;
                const delay = Math.random() * 5;
                particle.style.animation = `floatElement ${duration}s infinite linear ${delay}s`;
                
                particlesContainer.appendChild(particle);
            }
        }
        
        // Create floating elements
        function createFloatingElements() {
            const container = document.querySelector('.floating-elements');
            const elementCount = 8;
            
            for (let i = 0; i < elementCount; i++) {
                const element = document.createElement('div');
                element.classList.add('floating-element');
                
                // Random position
                element.style.left = `${Math.random() * 90 + 5}%`;
                element.style.top = `${Math.random() * 100 + 100}%`;
                
                // Random size
                const size = Math.random() * 30 + 20;
                element.style.width = `${size}px`;
                element.style.height = `${size}px`;
                
                // Random color
                const colors = ['rgba(255, 138, 0, 0.1)', 'rgba(229, 46, 113, 0.1)', 'rgba(157, 78, 221, 0.1)'];
                const color = colors[Math.floor(Math.random() * colors.length)];
                element.style.background = color;
                element.style.borderColor = color.replace('0.1', '0.3');
                
                // Random animation delay
                const delay = Math.random() * 10;
                element.style.animationDelay = `${delay}s`;
                
                container.appendChild(element);
            }
        }
        
        // 3D Background with Three.js
        function init3DBackground() {
            // Check if WebGL is supported
            if (!WEBGL.isWebGLAvailable()) {
                console.warn('WebGL not supported, using fallback background');
                return;
            }
            
            const canvas = document.getElementById('bg-canvas');
            const scene = new THREE.Scene();
            const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            const renderer = new THREE.WebGLRenderer({ canvas, alpha: true, antialias: true });
            
            renderer.setSize(window.innerWidth, window.innerHeight);
            renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
            
            // Create floating geometric objects
            const geometries = [
                new THREE.TetrahedronGeometry(1.5, 0),
                new THREE.OctahedronGeometry(1.3, 0),
                new THREE.IcosahedronGeometry(1.2, 0),
                new THREE.DodecahedronGeometry(1.4, 0)
            ];
            
            const material = new THREE.MeshPhongMaterial({
                color: 0x9d4edd,
                shininess: 100,
                transparent: true,
                opacity: 0.15,
                specular: 0xffffff
            });
            
            const objects = [];
            const objectCount = 8;
            
            for (let i = 0; i < objectCount; i++) {
                const geometry = geometries[Math.floor(Math.random() * geometries.length)];
                const mesh = new THREE.Mesh(geometry, material);
                
                // Random position
                mesh.position.x = (Math.random() - 0.5) * 30;
                mesh.position.y = (Math.random() - 0.5) * 20;
                mesh.position.z = (Math.random() - 0.5) * 30;
                
                // Random rotation
                mesh.rotation.x = Math.random() * Math.PI;
                mesh.rotation.y = Math.random() * Math.PI;
                
                // Random scale
                const scale = Math.random() * 0.8 + 0.5;
                mesh.scale.set(scale, scale, scale);
                
                scene.add(mesh);
                objects.push(mesh);
            }
            
            // Add lights
            const ambientLight = new THREE.AmbientLight(0xffffff, 0.3);
            scene.add(ambientLight);
            
            const directionalLight = new THREE.DirectionalLight(0xffffff, 0.5);
            directionalLight.position.set(1, 1, 1);
            scene.add(directionalLight);
            
            const pointLight = new THREE.PointLight(0xff8a00, 0.5, 50);
            pointLight.position.set(10, 10, 10);
            scene.add(pointLight);
            
            camera.position.z = 15;
            
            // Animation loop
            function animate() {
                requestAnimationFrame(animate);
                
                // Rotate objects
                objects.forEach((obj, index) => {
                    obj.rotation.x += 0.005 + (index * 0.0005);
                    obj.rotation.y += 0.003 + (index * 0.0003);
                    
                    // Float up and down
                    obj.position.y += Math.sin(Date.now() * 0.001 + index) * 0.002;
                });
                
                // Slowly rotate camera
                camera.position.x = Math.sin(Date.now() * 0.0003) * 5;
                camera.position.z = 15 + Math.cos(Date.now() * 0.0002) * 2;
                camera.lookAt(scene.position);
                
                renderer.render(scene, camera);
            }
            
            // Handle window resize
            function onWindowResize() {
                camera.aspect = window.innerWidth / window.innerHeight;
                camera.updateProjectionMatrix();
                renderer.setSize(window.innerWidth, window.innerHeight);
            }
            
            window.addEventListener('resize', onWindowResize);
            
            // Start animation
            animate();
        }
        
        // Initialize everything when page loads
        document.addEventListener('DOMContentLoaded', function() {
            createParticles();
            createFloatingElements();
            
            try {
                init3DBackground();
            } catch (error) {
                console.log('3D background failed to load:', error);
            }
            
            // Add scroll animations
            const observerOptions = {
                threshold: 0.1,
                rootMargin: '0px 0px -50px 0px'
            };
            
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.style.opacity = '1';
                        entry.target.style.transform = 'translateY(0)';
                    }
                });
            }, observerOptions);
            
            // Observe all sections for scroll animations
            document.querySelectorAll('.roles-section, .skills-section, .github-section, .contact-section, .social-section').forEach(section => {
                section.style.opacity = '0';
                section.style.transform = 'translateY(30px)';
                section.style.transition = 'opacity 0.8s ease, transform 0.8s ease';
                observer.observe(section);
            });
        });
    </script>
</body>
</html>
