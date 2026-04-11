    <title>Aqualink Delivery Service</title>
<html lang="en">
  <head>
    <meta charset="UTF-8" />


    <style>
      body {
        font-family: Arial, sans-serif;
        margin: 0;
        background: #f4f4f4;
      }

      /* Navbar */
      nav {
        background: #333;
        padding: 10px;
        text-align: center;
      }
      nav img {
        height: 50px;
        display: block;
        margin: auto;
      }
      nav button {
        background: #ff6600;
        border: none;
        padding: 10px 20px;
        margin: 5px;
        color: white;
        cursor: pointer;
      }
      nav button:hover {
        background: #e65c00;
      }

      /* Sections */
      .section {
        display: none;
        padding: 20px;
      }
      .active {
        display: block;
      }

      /* Card */
      .card {
        background: white;
        padding: 15px;
        margin: 10px 0;
        border-radius: 5px;
      }

      /* Form */
      form {
        background: white;
        padding: 15px;
        border-radius: 5px;
      }
      input,
      button {
        padding: 10px;
        margin: 5px 0;
        width: 100%;
      }

      /* Logo center */
      .logo-center {
        height: 120px;
        display: block;
        margin: 20px auto;
      }
    </style>
  </head>

  <body>
    <!-- NAVBAR -->
    <nav>
      <img src="Qlogo.jpg" alt="Qlink Logo" />
      <button onclick="showSection('home')">Home</button>
      <button onclick="showSection('services')">Services</button>
      <button onclick="showSection('contact')">Contact</button>
    </nav>

    <!-- HOME -->
    <div id="home" class="section active">
      <h2>Welcome to Qlink Delivery 🚚</h2>

      <img src="Qlogo.jpg" class="logo-center" />

      <div class="card">
        <p>Fast and reliable delivery at your doorstep.</p>
        <button onclick="showDetails()">Show Details</button>
        <p id="details"></p>
      </div>
    </div>

    <!-- SERVICES -->
    <div id="services" class="section">
      <h2>Our Services</h2>
      <div class="card">
        <ul>
          <li>Food Delivery</li>
          <li>Parcel Delivery</li>
          <li>Same Day Delivery</li>
        </ul>
        <button onclick="showDetails()">Show Details</button>
        <p id="details"></p>
      </div>
    </div>

    <!-- CONTACT -->
    <div id="contact" class="section">
      <h2>Contact Us</h2>

      <div class="card">
        <button onclick="showContact()">Show Contact Info</button>
        <p id="contactInfo"></p>
      </div>

      <h3>Fill Form</h3>
      <form onsubmit="return validateForm();">
        <input type="text" id="name" placeholder="Enter Name" required="" />
        <input type="email" id="email" placeholder="Enter Email" required="" />

        <label id="captchaLabel"></label>
        <input type="text" id="captchaInput" placeholder="Enter Captcha" required="" />

        <button type="submit">Submit</button>
      </form>
    </div>

    <script>
      /* Section Switch */
      function showSection(section) {
        document.querySelectorAll(".section").forEach((sec) => {
          sec.classList.remove("active");
        });
        document.getElementById(section).classList.add("active");
      }

      /* Details */
      function showDetails() {
        let info = "Address: Main Road, City | Location: Near Market | Contact: +91 9876543210";
        document.querySelectorAll("#details").forEach((el) => {
          el.innerText = info;
        });
      }

      /* Contact Info */
      function showContact() {
        document.getElementById("contactInfo").innerText =
          "Address: Nazma Street, Doha | Location: Doha,Qatar | Phone: +974 77365917";
      }

      /* CAPTCHA */
      let num1 = Math.floor(Math.random() * 10);
      let num2 = Math.floor(Math.random() * 10);

      document.getElementById("captchaLabel").innerText = "Captcha: " + num1 + " + " + num2 + " = ?";

      function validateForm() {
        let userAnswer = document.getElementById("captchaInput").value;

        if (userAnswer != num1 + num2) {
          alert("Wrong captcha!");
          return false;
        }

        alert("Form submitted successfully!");
        return true;
      }
    </script>
  </body>
</html>
