# Advanced-Website-with-Responsive-Design-and-Interactive-Features
This project is a modern, responsive website that incorporates several advanced features. It includes a simple navigation bar, a fully functional image carousel, a contact form with validation, and a sleek, user-friendly design. The website is built using HTML, CSS, and JavaScript to ensure that it is both visually appealing and interactive.
HOST A WEBSITE FOR FREE USING AWS
Step 1: Launch an EC2 Instance
1.	Log into AWS Management Console: Go to AWS Management Console and log in.
2.	Create EC2 Instance:
o	Go to the EC2 Dashboard.
o	Click Launch Instance.
o	Select an AMI (Amazon Machine Image). For example, choose Amazon Linux 2 AMI or Ubuntu.
o	Choose an Instance Type (e.g., t2.micro for free-tier eligible).
o	Configure instance details (keep default settings unless you need to customize).
o	Add storage if necessary.
o	Configure Security Group:
	Open ports 22 (SSH), 80 (HTTP), and 443 (HTTPS).
	For SSH, restrict access to your IP (for security reasons).
3.	Review and Launch: Review your instance settings and launch it.
o	Download the key pair .pem file if you don’t have one, as you’ll use this to SSH into the instance.
4.	Get Public IP: Once the instance is running, find its Public IP in the EC2 dashboard. This will be used to access your website.
Step 2: SSH into the EC2 Instance
1.	Open a terminal on your local machine.
2.	Change the directory to where your .pem file is located.
3.	Use the following command to SSH into your instance:
bash
Copy
ssh -i "your-key.pem" ec2-user@your-public-ip
Replace your-key.pem with the actual key name and your-public-ip with your EC2 instance's public IP.

Step 3: Install Apache or Nginx
For Apache:
1.	Install Apache: For Amazon Linux 2 or Ubuntu, you can install Apache using the following commands:
o	For Amazon Linux 2:
bash
Copy
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
o	For Ubuntu:
bash
Copy
sudo apt update
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
2.	Verify Apache Installation: Visit http://your-public-ip in your browser. If Apache is installed correctly, you should see the Apache test page.
For Nginx:
1.	Install Nginx:
o	For Amazon Linux 2:
bash
Copy
sudo amazon-linux-extras install nginx1 -y
sudo systemctl start nginx
sudo systemctl enable nginx
o	For Ubuntu:
bash
Copy
sudo apt update
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
2.	Verify Nginx Installation: Visit http://your-public-ip in your browser. If Nginx is installed correctly, you should see the Nginx welcome page.
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
