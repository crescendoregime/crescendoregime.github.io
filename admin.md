<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Crescendo Regime</title>
  <link type="text/css" rel="stylesheet" href="style.css"> 
</head>
<body>
  <nav>
    <div class="nav-container">
      <div class="logo"><a href="index.html"><img src="Crescendo Regime Emblem.png" class="emblem" alt="Crescendo Regime Emblem"></div>
      <ul class="nav-links" id="navLinks">
        <li><a href="index.html">Home</a></li>
        <li><a href="manifesto.html">Manifesto</a></li>
        <li><a href="propaganda.html">Propaganda</a></li>
        <li><a href="music.html">Music</a></li>
        <li><a href="admin.html">Admin</a></li>
        <br>
      </ul>
    </div>
  </nav>
  <header id="home">
    <img src="big brother.png" alt="Big Brother" class="header-image">
    <div class="centeredtext">Crescendo Regime</div>
    <p></p>
  </header>
  <h2>Please log in to access administrator pages.</h2>
  <button onclick="document.getElementById('id01').style.display='block'" style="width:auto;">Login</button>
  <div id="id01" class="modal">
    <form id="login" class="modal-content animate" action="admin.html" method="post">
      <div class="container">
        <label for="uname"><b>Username</b></label>
        <input type="text" placeholder="Enter Username" name="uname" required>
        <label for="password"><b>Password</b></label>
        <input type="password" placeholder="Enter Password" name="password" required>
        <button type="submit">Login</button>
      </div>
    </form>
  </div>
  <script>var modal = document.getElementById('id01'); window.onclick = function(event) {if (event.target == modal) {modal.style.display = "none";}}</script>
  <!-- https://www.w3schools.com/howto/tryit.asp?filename=tryhow_css_login_form_modal -->
</body></html>
