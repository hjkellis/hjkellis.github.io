+++
title= "Hello, I'm Hunter"
template = "homepage.html"

+++

<div style="display: flex; flex-wrap: wrap; align-items: center; gap: 20px;">
  <div style="flex: 1; min-width: 250px;">
    <p>
      I am a <span id="ageDisplay"></span> year old Electrical & Computer Engineer with interests in control systems, robotics, and autonomy.
    </p>
    <p>
      Checkout my <a href="./projects">projects</a>, <a href="./posts">blog posts</a>, or <a href="./about">experience</a>.
    </p>
  </div>
</div>

<script>
  const birthDate = new Date("2002-01-01T00:00:00Z");

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

