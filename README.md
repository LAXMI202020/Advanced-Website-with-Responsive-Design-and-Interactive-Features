STEPS:
Step 1: Create an AWS Free Tier Account
Go to AWS Sign Up

Register with your email and complete identity verification.

AWS Free Tier provides 750 hours per month of EC2 usage for free.

Step 2: Launch an EC2 Instance
Login to AWS Console.

Open EC2 Dashboard.

Click Launch Instance.

Set up:

Name: Advanced-Website-Server

AMI (OS): Choose Ubuntu 22.04 LTS (recommended) or Amazon Linux 2.

Instance Type: Select t2.micro (Free Tier eligible).

Key Pair: Create or select an existing key pair (to SSH into the server).

Security Group:

Allow HTTP (port 80)

Allow SSH (port 22) (for access)

Storage: Default 8GB is enough.

Click Launch Instance and wait for it to initialize.

Step 3: Connect to EC2 Instance via SSH
Open a terminal and run:

sh
Copy
Edit
ssh -i your-key.pem ubuntu@your-ec2-public-ip
Replace your-key.pem with your private key file and your-ec2-public-ip with the instance's public IP.

After logging in, update the server:

sh
Copy
Edit
sudo apt update && sudo apt upgrade -y
Step 4: Install and Configure NGINX or Apache HTTPD
Option 1: Install NGINX (Recommended)
Install NGINX:

sh
Copy
Edit
sudo apt install nginx -y
Start and enable NGINX:

sh
Copy
Edit
sudo systemctl start nginx
sudo systemctl enable nginx
Check if it's running:

sh
Copy
Edit
systemctl status nginx
Open your browser and visit http://your-ec2-public-ip – You should see the NGINX default page.

Option 2: Install Apache HTTPD
Install Apache:

sh
Copy
Edit
sudo apt install apache2 -y
Start and enable Apache:

sh
Copy
Edit
sudo systemctl start apache2
sudo systemctl enable apache2
Check status:

sh
Copy
Edit
systemctl status apache2
Open http://your-ec2-public-ip in a browser. The Apache default page should appear.

Step 5: Deploy Your Website
Move Your Website Files
Navigate to the web root directory:

For NGINX:

sh
Copy
Edit
cd /var/www/html
For Apache HTTPD:

sh
Copy
Edit
cd /var/www/html
Upload your website files from your local machine to EC2 using SCP:

sh
Copy
Edit
scp -i your-key.pem -r /path/to/your/website ubuntu@your-ec2-public-ip:/var/www/html/
Replace /path/to/your/website with your actual project folder.

Set permissions:

sh
Copy
Edit
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html
Step 6: Configure NGINX or Apache
NGINX Configuration
Open the configuration file:

sh
Copy
Edit
sudo nano /etc/nginx/sites-available/default
Replace existing content with:

nginx
Copy
Edit
server {
    listen 80;
    server_name your-ec2-public-ip;

    root /var/www/html;
    index index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }
}
Save (CTRL + X, Y, Enter).

Restart NGINX:

sh
Copy
Edit
sudo systemctl restart nginx
Apache HTTPD Configuration
Open Apache config file:

sh
Copy
Edit
sudo nano /etc/apache2/sites-available/000-default.conf
Update:

apache
Copy
Edit
<VirtualHost *:80>
    DocumentRoot /var/www/html
    <Directory /var/www/html>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
Save (CTRL + X, Y, Enter).

Restart Apache:

sh
Copy
Edit
sudo systemctl restart apache2
Step 7: Access Your Website
Open http://your-ec2-public-ip in your browser.

Your Advanced Website should be live! 🚀





CODE OF MY STATIC WEBSITE(index.html):
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Advanced Features Website</title>
  <link rel="stylesheet" href="styles.css">
  <script src="script.js" defer></script>
</head>
<body>
  <!-- Navigation Bar -->
  <header>
    <nav>
      <ul>
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#services">Services</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </nav>
  </header>

  <!-- Hero Section with Image Carousel -->
  <section id="home" class="hero">
    <div class="carousel">
      <img src="https://via.placeholder.com/1200x400?text=Image+1" alt="Slide 1">
      <img src="https://via.placeholder.com/1200x400?text=Image+2" alt="Slide 2">
      <img src="https://via.placeholder.com/1200x400?text=Image+3" alt="Slide 3">
    </div>
    <h1>Welcome to Our Website</h1>
    <p>Your one-stop solution for web development and more!</p>
  </section>

  <!-- About Section -->
  <section id="about" class="about">
    <h2>About Us</h2>
    <p>We are a team of passionate developers building innovative solutions to solve complex problems.</p>
  </section>

  <!-- Services Section -->
  <section id="services" class="services">
    <h2>Our Services</h2>
    <div class="service-item">
      <h3>Web Development</h3>
      <p>We build responsive, scalable, and beautiful websites that fit your business needs.</p>
    </div>
    <div class="service-item">
      <h3>App Development</h3>
      <p>We create mobile applications for Android and iOS platforms that are both functional and user-friendly.</p>
    </div>
    <div class="service-item">
      <h3>SEO Optimization</h3>
      <p>Our SEO strategies help your website rank higher on search engines and drive organic traffic.</p>
    </div>
  </section>

  <!-- Contact Section with Form Validation -->
  <section id="contact" class="contact">
    <h2>Contact Us</h2>
    <form id="contactForm" action="#" method="post" onsubmit="return validateForm()">
      <label for="name">Name</label>
      <input type="text" id="name" name="name" placeholder="Your Name" required>

      <label for="email">Email</label>
      <input type="email" id="email" name="email" placeholder="Your Email" required>

      <label for="message">Message</label>
      <textarea id="message" name="message" placeholder="Your Message" required></textarea>

      <button type="submit">Submit</button>
    </form>
  </section>

  <!-- Footer -->
  <footer>
    <p>&copy; 2025 Your Website. All rights reserved.</p>
  </footer>
</body>
</html>

CSS (styles.css)

/* General Styling */
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background-color: #f4f4f4;
}

header {
  background-color: #333;
  color: white;
  padding: 10px 0;
  text-align: center;
}

header nav ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

header nav ul li {
  display: inline;
  margin: 0 20px;
}

header nav ul li a {
  color: white;
  text-decoration: none;
  font-weight: bold;
}

.hero {
  text-align: center;
  background-color: #333;
  color: white;
  padding: 50px 20px;
}

.hero h1 {
  font-size: 3em;
}

.hero p {
  font-size: 1.5em;
}

.carousel {
  position: relative;
  max-width: 100%;
  height: 400px;
  overflow: hidden;
}

.carousel img {
  width: 100%;
  height: auto;
  display: none;
}

.about, .services, .contact {
  padding: 50px 20px;
  text-align: center;
}

h2 {
  font-size: 2.5em;
}

.service-item {
  margin: 20px 0;
}

.contact form {
  max-width: 600px;
  margin: 0 auto;
  background-color: #fff;
  padding: 20px;
  border-radius: 5px;
}

.contact label {
  display: block;
  margin: 10px 0 5px;
}

.contact input, .contact textarea {
  width: 100%;
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.contact button {
  padding: 10px 20px;
  background-color: #333;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

footer {
  text-align: center;
  padding: 20px;
  background-color: #333;
  color: white;
  margin-top: 50px;
}

/* Responsive Design */
@media (max-width: 768px) {
  .service-item {
    width: 100%;
    margin: 10px 0;
  }

  .hero h1 {
    font-size: 2em;
  }

  .hero p {
    font-size: 1.2em;
  }
}


JavaScript (script.js)
// Carousel functionality (auto-slide)
let currentIndex = 0;
const slides = document.querySelectorAll('.carousel img');
const totalSlides = slides.length;

function showSlide(index) {
  slides.forEach((slide, i) => {
    slide.style.display = (i === index) ? 'block' : 'none';
  });
}

function nextSlide() {
  currentIndex = (currentIndex + 1) % totalSlides;
  showSlide(currentIndex);
}

function prevSlide() {
  currentIndex = (currentIndex - 1 + totalSlides) % totalSlides;
  showSlide(currentIndex);
}

// Auto slide every 3 seconds
setInterval(nextSlide, 3000);
showSlide(currentIndex);

// Form validation
function validateForm() {
  const name = document.getElementById('name').value;
  const email = document.getElementById('email').value;
  const message = document.getElementById('message').value;

  if (!name || !email || !message) {
    alert('Please fill in all fields.');
    return false;
  }
  alert('Form submitted successfully!');
  return true;
}





 


  

  
