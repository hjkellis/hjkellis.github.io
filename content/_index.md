+++
title= "Hello, I'm Hunter"
template = "homepage.html"
+++

<div style="display: flex; flex-wrap: wrap; align-items: center; gap: 20px;">
  <img src="/images/ta.jpg" alt="profile picture" style="width: 300px; max-width: 100%;">
  <div style="flex: 1; min-width: 250px;">
    <p>
      I am a <span id="ageDisplay"></span> year old Electrical & Computer Engineer with interests in control systems, robotics, and autonomy.
    </p>
    <p>
      Checkout my <a href="./projects">projects</a>, <a href="./posts">blog posts</a>, or <a href="./timeline">experience</a>.
    </p>
    <p><a href="/pdfs/Ellis-Hunter-Resume.pdf">PDF Resume</a></p>
  </div>
</div>

<script>
  const birthDate = new Date("2001-11-20T00:00:00Z");

  function updateAge() {
    const now = new Date();
    const ageInMilliseconds = now - birthDate;
    const millisecondsInYear = 1000 * 60 * 60 * 24 * 365.2425; // accounts for leap years
    const age = ageInMilliseconds / millisecondsInYear;

    document.getElementById("ageDisplay").textContent = age.toFixed(11);
    
    requestAnimationFrame(updateAge);
  }

  updateAge();

</script>
