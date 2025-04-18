<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Rohit V Deshmukh - Portfolio</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.4/gsap.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/0.149.0/three.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/vanilla-tilt/1.8.0/vanilla-tilt.min.js"></script>
  <style>
    :root {
      --bg-color: #0e1525;
      --text-color: #e2e8f0;
      --accent-color: #3b82f6;
      --secondary-color: #10b981;
      --tertiary-color: #8b5cf6;
      --card-bg: rgba(30, 41, 59, 0.7);
      --social-icon-size: 40px;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Poppins', sans-serif;
    }

    body {
      background: var(--bg-color);
      color: var(--text-color);
      overflow-x: hidden;
      line-height: 1.6;
    }

    #canvas-container {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100vh;
      z-index: -1;
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 2rem;
      position: relative;
    }

    .header {
      text-align: center;
      margin-bottom: 3rem;
      padding-top: 4rem;
      position: relative;
    }

    .header h1 {
      font-size: 3.5rem;
      margin-bottom: 1rem;
      background: linear-gradient(to right, var(--accent-color), var(--tertiary-color));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      position: relative;
      opacity: 0;
      transform: translateY(-20px);
    }

    .header h3 {
      font-size: 1.5rem;
      opacity: 0.8;
      margin-bottom: 2rem;
      opacity: 0;
      transform: translateY(-20px);
    }

    .profile-img {
      width: 150px;
      height: 150px;
      border-radius: 50%;
      object-fit: cover;
      margin: 0 auto 2rem;
      border: 4px solid var(--accent-color);
      display: block;
      opacity: 0;
      transform: scale(0.8);
    }

    .about-section {
      background: var(--card-bg);
      padding: 2rem;
      border-radius: 12px;
      margin-bottom: 3rem;
      backdrop-filter: blur(10px);
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
      opacity: 0;
      transform: translateY(20px);
    }

    .about-items {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 1.5rem;
      margin-top: 2rem;
    }

    .about-item {
      display: flex;
      align-items: flex-start;
      gap: 1rem;
    }

    .about-item i {
      font-size: 1.5rem;
      color: var(--accent-color);
    }

    .connect-section {
      margin-bottom: 3rem;
      opacity: 0;
    }

    .section-title {
      font-size: 1.8rem;
      margin-bottom: 1.5rem;
      position: relative;
      padding-bottom: 0.5rem;
      display: inline-block;
    }

    .section-title::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 3px;
      background: linear-gradient(to right, var(--accent-color), var(--tertiary-color));
      transition: transform 0.3s ease;
      transform: scaleX(0);
      transform-origin: left;
    }

    .section-title:hover::after {
      transform: scaleX(1);
    }

    .social-icons {
      display: flex;
      gap: 1.5rem;
      flex-wrap: wrap;
      margin-top: 1.5rem;
    }

    .social-icon {
      width: var(--social-icon-size);
      height: var(--social-icon-size);
      border-radius: 10px;
      background: var(--card-bg);
      display: flex;
      align-items: center;
      justify-content: center;
      transition: all 0.3s ease;
      cursor: pointer;
      box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
      transform: translateY(20px);
      opacity: 0;
    }

    .social-icon img {
      width: 24px;
      height: 24px;
      transition: transform 0.3s ease;
    }

    .social-icon:hover {
      transform: translateY(-5px);
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
      background: var(--accent-color);
    }

    .social-icon:hover img {
      transform: scale(1.2);
    }

    .skills-section {
      margin-bottom: 3rem;
      opacity: 0;
    }

    .skills-container {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(80px, 1fr));
      gap: 1.5rem;
      margin-top: 2rem;
    }

    .skill-item {
      background: var(--card-bg);
      border-radius: 12px;
      padding: 1rem;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      transition: all 0.3s ease;
      opacity: 0;
      transform: translateY(20px);
    }

    .skill-item:hover {
      transform: translateY(-5px) scale(1.05);
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
      background: rgba(59, 130, 246, 0.2);
    }

    .skill-item img {
      width: 40px;
      height: 40px;
      margin-bottom: 0.5rem;
      transition: transform 0.3s ease;
    }

    .skill-item:hover img {
      transform: rotate(10deg) scale(1.2);
    }

    .skill-item p {
      font-size: 0.8rem;
      text-align: center;
    }

    .stats-section {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2rem;
      margin-bottom: 3rem;
      opacity: 0;
    }

    .stat-card {
      background: var(--card-bg);
      border-radius: 12px;
      padding: 1.5rem;
      position: relative;
      overflow: hidden;
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
      transition: all 0.3s ease;
      min-height: 200px;
    }

    .stat-card:hover {
      transform: translateY(-10px);
      box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
    }

    .stat-card::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: linear-gradient(135deg, rgba(59, 130, 246, 0.15), rgba(139, 92, 246, 0.15));
      clip-path: circle(0% at 0% 0%);
      transition: clip-path 0.5s ease;
    }

    .stat-card:hover::before {
      clip-path: circle(150% at 0% 0%);
    }

    .stat-card img {
      width: 100%;
      border-radius: 8px;
      margin-top: 1rem;
    }

    .contact-section {
      text-align: center;
      margin-bottom: 3rem;
      opacity: 0;
    }

    .email-btn {
      background: linear-gradient(to right, var(--accent-color), var(--tertiary-color));
      color: white;
      border: none;
      padding: 0.8rem 2rem;
      border-radius: 50px;
      font-size: 1.1rem;
      font-weight: 500;
      cursor: pointer;
      transition: all 0.3s ease;
      margin-top: 1.5rem;
      display: inline-block;
      text-decoration: none;
      box-shadow: 0 4px 15px rgba(59, 130, 246, 0.3);
    }

    .email-btn:hover {
      transform: translateY(-5px);
      box-shadow: 0 10px 25px rgba(59, 130, 246, 0.5);
    }

    footer {
      text-align: center;
      padding: 2rem 0;
      opacity: 0.7;
      font-size: 0.9rem;
    }

    .cursor {
      position: fixed;
      width: 20px;
      height: 20px;
      border-radius: 50%;
      background: rgba(59, 130, 246, 0.5);
      pointer-events: none;
      mix-blend-mode: difference;
      z-index: 9999;
      transform: translate(-50%, -50%);
    }

    .cursor-follower {
      position: fixed;
      width: 50px;
      height: 50px;
      border-radius: 50%;
      background: rgba(139, 92, 246, 0.15);
      pointer-events: none;
      z-index: 9998;
      transition: transform 0.1s ease;
      transform: translate(-50%, -50%);
    }

    @media (max-width: 768px) {
      .header h1 {
        font-size: 2.5rem;
      }
      .header h3 {
        font-size: 1.2rem;
      }
      .skills-container {
        grid-template-columns: repeat(auto-fill, minmax(70px, 1fr));
      }
      .cursor, .cursor-follower {
        display: none;
      }
    }

    /* Animation for scroll reveal */
    @keyframes fadeInUp {
      from {
        opacity: 0;
        transform: translateY(20px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }
  </style>
</head>
<body>
  <div class="cursor"></div>
  <div class="cursor-follower"></div>
  <div id="canvas-container"></div>

  <div class="container">
    <header class="header">
      <img src="https://github.com/rohitdeshmukh27.png" alt="Rohit V Deshmukh" class="profile-img">
      <h1>Hi 👋, I'm Rohit V Deshmukh</h1>
      <h3>A passionate frontend developer & Penetration Tester[beginner] from Pune, India</h3>
    </header>

    <section class="about-section">
      <h2 class="section-title">About Me</h2>
      <div class="about-items">
        <div class="about-item">
          <i>🌱</i>
          <p>I'm currently learning <strong>React Native & Penetration Testing</strong></p>
        </div>
        <div class="about-item">
          <i>👯</i>
          <p>I'm looking to collaborate on <strong>Front-end Projects</strong></p>
        </div>
        <div class="about-item">
          <i>🤝</i>
          <p>I'm looking for help with <strong>UI/UX, Front-end & Penetration Testing</strong></p>
        </div>
      </div>
    </section>

    <section class="connect-section">
      <h2 class="section-title">Connect with me</h2>
      <div class="social-icons">
        <a href="https://linkedin.com/in/rohitdeshmukh27" target="_blank" class="social-icon">
          <img src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/linked-in-alt.svg" alt="LinkedIn">
        </a>
        <a href="https://instagram.com/rohitvd27" target="_blank" class="social-icon">
          <img src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/instagram.svg" alt="Instagram">
        </a>
        <a href="https://www.youtube.com/@rohitdeshmukh27" target="_blank" class="social-icon">
          <img src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/youtube.svg" alt="YouTube">
        </a>
        <a href="https://www.hackerrank.com/rohitdeshmukh27" target="_blank" class="social-icon">
          <img src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/hackerrank.svg" alt="HackerRank">
        </a>
        <a href="https://www.leetcode.com/rohitdeshmukh27" target="_blank" class="social-icon">
          <img src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/leet-code.svg" alt="LeetCode">
        </a>
      </div>
    </section>

    <section class="skills-section">
      <h2 class="section-title">Languages and Tools</h2>
      <div class="skills-container">
        <div class="skill-item">
          <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original-wordmark.svg" alt="HTML5">
          <p>HTML5</p>
        </div>
        <div class="skill-item">
          <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original-wordmark.svg" alt="CSS3">
          <p>CSS3</p>
        </div>
        <div class="skill-item">
          <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg" alt="JavaScript">
          <p>JavaScript</p>
        </div>
        <div class="skill-item">
          <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/react/react-original-wordmark.svg" alt="React">
          <p>React</p>
        </div>
        <div class="skill-item">
          <img src="https://reactnative.dev/img/header_logo.svg" alt="React Native">
          <p>React Native</p>
        </div>
        <div class="skill-item">
          <img src="https://angular.io/assets/images/logos/angular/angular.svg" alt="Angular">
          <p>Angular</p>
        </div>
        <div class="skill-item">
          <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/vuejs/vuejs-original-wordmark.svg" alt="Vue.js">
          <p>Vue.js</p>
        </div>
        <div class="skill-item">
          <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/nodejs/nodejs-original-wordmark.svg" alt="Node.js">
          <p>Node.js</p>
        </div>
        <div class="skill-item">
          <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/express/express-original-wordmark.svg" alt="Express">
          <p>Express</p>
        </div>
        <div class="skill-item">
          <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="Python">
          <p>Python</p>
        </div>
        <div class="skill-item">
          <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/c/c-original.svg" alt="C">
          <p>C</p>
        </div>
        <div class="skill-item">
          <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/cplusplus/cplusplus-original.svg" alt="C++">
          <p>C++</p>
        </div>
        <div class="skill-item">
          <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/php/php-original.svg" alt="PHP">
          <p>PHP</p>
        </div>
        <div class="skill-item">
          <img src="https://www.vectorlogo.zone/logos/tailwindcss/tailwindcss-icon.svg" alt="Tailwind CSS">
          <p>Tailwind</p>
        </div>
        <div class="skill-item">
          <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/bootstrap/bootstrap-plain-wordmark.svg" alt="Bootstrap">
          <p>Bootstrap</p>
        </div>
        <div class="skill-item">
          <img src="https://www.vectorlogo.zone/logos/figma/figma-icon.svg" alt="Figma">
          <p>Figma</p>
        </div>
        <div class="skill-item">
          <img src="https://www.vectorlogo.zone/logos/git-scm/git-scm-icon.svg" alt="Git">
          <p>Git</p>
        </div>
        <div class="skill-item">
          <img src="https://www.vectorlogo.zone/logos/firebase/firebase-icon.svg" alt="Firebase">
          <p>Firebase</p>
        </div>
        <div class="skill-item">
          <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mysql/mysql-original-wordmark.svg" alt="MySQL">
          <p>MySQL</p>
        </div>
        <div class="skill-item">
          <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/linux/linux-original.svg" alt="Linux">
          <p>Linux</p>
        </div>
      </div>
    </section>

    <section class="stats-section">
      <div class="stat-card">
        <h3>GitHub Stats</h3>
        <img src="https://github-readme-stats.vercel.app/api?username=rohitdeshmukh27&show_icons=true&locale=en&theme=tokyonight" alt="GitHub Stats">
      </div>
      <div class="stat-card">
        <h3>Most Used Languages</h3>
        <img src="https://github-readme-stats.vercel.app/api/top-langs?username=rohitdeshmukh27&show_icons=true&locale=en&layout=compact&theme=tokyonight" alt="Most Used Languages">
      </div>
      <div class="stat-card">
        <h3>Streak Stats</h3>
        <img src="https://github-readme-streak-stats.herokuapp.com/?user=rohitdeshmukh27&theme=tokyonight" alt="Streak Stats">
      </div>
    </section>

    <section class="contact-section">
      <h2 class="section-title">Get in Touch</h2>
      <a href="mailto:rohitvd27@gmail.com" class="email-btn">Send me an email</a>
    </section>

    <footer>
      <p>© 2025 Rohit V Deshmukh | All Rights Reserved</p>
    </footer>
  </div>

  <script>
    // Mouse follower cursor effect
    const cursor = document.querySelector('.cursor');
    const cursorFollower = document.querySelector('.cursor-follower');
    
    document.addEventListener('mousemove', e => {
      cursor.style.left = e.clientX + 'px';
      cursor.style.top = e.clientY + 'px';
      
      // Add a slight delay to the follower
      setTimeout(() => {
        cursorFollower.style.left = e.clientX + 'px';
        cursorFollower.style.top = e.clientY + 'px';
      }, 80);
    });

    // Hover effect on links
    const links = document.querySelectorAll('a');
    links.forEach(link => {
      link.addEventListener('mouseenter', () => {
        cursor.style.transform = 'translate(-50%, -50%) scale(2)';
        cursorFollower.style.transform = 'translate(-50%, -50%) scale(0.5)';
      });
      
      link.addEventListener('mouseleave', () => {
        cursor.style.transform = 'translate(-50%, -50%) scale(1)';
        cursorFollower.style.transform = 'translate(-50%, -50%) scale(1)';
      });
    });

    // Add tilt effect to cards
    VanillaTilt.init(document.querySelectorAll(".skill-item"), {
      max: 25,
      speed: 400,
      glare: true,
      "max-glare": 0.5,
    });

    VanillaTilt.init(document.querySelectorAll(".stat-card"), {
      max: 15,
      speed: 400,
      glare: true,
      "max-glare": 0.3,
    });

    // Interactive background with Three.js
    const createBackground = () => {
      const container = document.getElementById('canvas-container');
      const width = window.innerWidth;
      const height = window.innerHeight;
      
      const scene = new THREE.Scene();
      const camera = new THREE.PerspectiveCamera(75, width / height, 0.1, 1000);
      const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
      
      renderer.setSize(width, height);
      container.appendChild(renderer.domElement);
      
      // Create particles
      const particlesGeometry = new THREE.BufferGeometry();
      const particlesCount = 2000;
      
      const posArray = new Float32Array(particlesCount * 3);
      
      for(let i = 0; i < particlesCount * 3; i++) {
        posArray[i] = (Math.random() - 0.5) * 10;
      }
      
      particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));
      
      const particlesMaterial = new THREE.PointsMaterial({
        size: 0.02,
        color: 0x3b82f6,
        transparent: true,
        opacity: 0.8,
      });
      
      const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
      scene.add(particlesMesh);
      
      camera.position.z = 2;
      
      // Mouse movement effect
      document.addEventListener('mousemove', animateParticles);
      let mouseX = 0;
      let mouseY = 0;
      
      function animateParticles(event) {
        mouseX = event.clientX / width - 0.5;
        mouseY = event.clientY / height - 0.5;
      }
      
      const animate = () => {
        requestAnimationFrame(animate);
        
        particlesMesh.rotation.y += 0.001;
        
        particlesMesh.rotation.x += mouseY * 0.001;
        particlesMesh.rotation.y += mouseX * 0.001;
        
        renderer.render(scene, camera);
      };
      
      animate();
      
      // Handle resize
      window.addEventListener('resize', () => {
        const width = window.innerWidth;
        const height = window.innerHeight;
        
        camera.aspect = width / height;
        camera.updateProjectionMatrix();
        
        renderer.setSize(width, height);
      });
    };

    // GSAP animations
    const animateElements = () => {
      // Header animations
      gsap.to('.header h1', { 
        opacity: 1, 
        y: 0, 
        duration: 1, 
        ease: "power3.out" 
      });
      
      gsap.to('.header h3', { 
        opacity: 1, 
        y: 0, 
        duration: 1, 
        delay: 0.3, 
        ease: "power3.out" 
      });
      
      gsap.to('.profile-img', { 
        opacity: 1, 
        scale: 1, 
        duration: 1, 
        delay: 0.2, 
        ease: "back.out(1.7)" 
      });
      
      // About section
      gsap.to('.about-section', { 
        opacity: 1, 
        y: 0, 
        duration: 1, 
        delay: 0.4, 
        ease: "power3.out" 
      });
      
      // Connect section
      gsap.to('.connect-section', { 
        opacity: 1, 
        duration: 1, 
        delay: 0.6, 
        ease: "power3.out" 
      });
      
      // Social icons
      gsap.to('.social-icon', { 
        opacity: 1, 
        y: 0, 
        duration: 1, 
        stagger: 0.1, 
        delay: 0.8, 
        ease: "back.out(1.7)" 
      });
      
      // Skills section
      gsap.to('.skills-section', { 
        opacity: 1, 
        duration: 1, 
        delay: 1, 
        ease: "power3.out" 
      });
      
      // Skill items
      gsap.to('.skill-item', { 
        opacity: 1, 
        y: 0, 
        duration: 1, 
        stagger: 0.05, 
        delay: 1.2, 
        ease: "back.out(1.7)" 
      });
      
      // Stats section
      gsap.to('.stats-section', { 
        opacity: 1, 
        duration: 1, 
        delay: 1.4, 
        ease: "power3.out" 
      });
      
      // Contact section
      gsap.to('.contact-section', { 
        opacity: 1, 
        duration: 1, 
        delay: 1.6, 
        ease: "power3.out" 
      });
      
      // Footer
      gsap.to('footer', { 
        opacity: 0.7, 
        duration: 1, 
        delay: 1.8, 
        ease: "power3.out" 
      });
    };

    // Initialize scroll reveal for elements
    const scrollReveal = () => {
      const sections = document.querySelectorAll('section');
      
      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.style.animation = `fadeInUp 1s forwards ease`;
            observer.unobserve(entry.target);
          }
        });
      }, { threshold: 0.1 });
      
      sections.forEach(section => {
        observer.observe(section);
      });
    };

    document.addEventListener('DOMContentLoaded', () => {
      createBackground();
      animateElements();
      scrollReveal();
    });
  </script>
</body>
</html>
