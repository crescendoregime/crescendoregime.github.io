#HTML:

<h2>Admin Login</h2>
  <form id="contactForm">
    <input type="text" id="username" placeholder="Username" required="">
    <input type="password" id="password" placeholder="Password" required=""><br>
    <input type="submit" value="Login">
</form>

#CSS:

#contactForm input, #contactForm textarea { display:block; width:90%; margin:10px auto; padding:10px; border-radius:5px; border:1px solid #880015; }
.submitbutton { background: #880015; color: #ffc90e; border:none; padding:10px 20px; cursor:pointer; border-radius:5px; }

#All of the JavaScript:

/* None of this is relevant */

document.addEventListener("DOMContentLoaded", () => {
  /* ===== Dark Mode ===== */
  const darkToggle = document.getElementById("darkModeToggle");

  if (localStorage.getItem("darkMode") === "enabled") {
    document.body.classList.add("dark-mode");
    darkToggle.textContent = "Light Mode";
  } else {
    darkToggle.textContent = "Dark Mode";
  }

  darkToggle.addEventListener("click", () => {
    document.body.classList.toggle("dark-mode");
    const isDark = document.body.classList.contains("dark-mode");
    darkToggle.textContent = isDark ? "Light Mode" : "Dark Mode";
    localStorage.setItem("darkMode", isDark ? "enabled" : "disabled");
  });

  /* ===== Hamburger Menu ===== */
  const hamburger = document.getElementById("hamburger");
  const navLinks = document.getElementById("navLinks");

  hamburger.addEventListener("click", () => navLinks.classList.toggle("active"));

  navLinks.querySelectorAll("a").forEach(link => {
    link.addEventListener("click", () => navLinks.classList.remove("active"));
  });

  /* ===== Login Modal ===== */
  const loginModal = document.getElementById("loginModal");
  const openLogin = document.getElementById("openLogin");
  const closeLogin = document.getElementById("closeLogin");
  const loginForm = document.getElementById("loginForm");

  openLogin.addEventListener("click", () => loginModal.style.display = "flex");
  closeLogin.addEventListener("click", () => loginModal.style.display = "none");
  window.addEventListener("click", e => {
    if (e.target === loginModal) loginModal.style.display = "none";
  });

  loginForm.addEventListener("submit", async (e) => {
    e.preventDefault();
    const username = document.getElementById("username").value;
    const password = document.getElementById("password").value;

    try {
      const res = await fetch("/.netlify/functions/login", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ username, password })
      });
      const data = await res.json();

      if (res.ok && data.success) {
        alert("Login successful!");
        loginModal.style.display = "none";
        localStorage.setItem("authToken", data.token);
        window.location.href = "/messages.html";
      } else {
        alert(data.error || "Invalid credentials");
      }
    } catch (err) {
      alert("Error connecting to login function: " + err.message);
    }
  });

  /* ===== Contact Form ===== */
  const contactForm = document.getElementById("contactForm");
  if (contactForm) {
    contactForm.addEventListener("submit", async (e) => {
      e.preventDefault();

      const name = document.getElementById("name").value;
      const email = document.getElementById("email").value;
      const message = document.getElementById("message").value;

      try {
        const res = await fetch("/.netlify/functions/contact", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ name, email, message }),
        });
        const data = await res.json();

        if (res.ok && data.success) {
          alert("Message sent successfully!");
          contactForm.reset();
        } else {
          alert(data.error || "Failed to send message");
        }
      } catch (err) {
        alert("Error connecting to contact function: " + err.message);
      }
    });
  }

  /* ===== Skills Progress Bars ===== */
  window.addEventListener("load", () => {
    const htmlBar = document.querySelector(".html-bar");
    const cssBar = document.querySelector(".css-bar");
    const jsBar = document.querySelector(".js-bar");

    if (htmlBar) htmlBar.style.width = "90%";
    if (cssBar) cssBar.style.width = "25%";
    if (jsBar) jsBar.style.width = "45%";
  });
});
