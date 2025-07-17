<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Road Traffic Management System</title>

  <!-- ⭐ CSS zote ziko hapa -->
  <style>
    :root {
      --main-bg: #004466;
      --main-light: #ffffff;
      --dark-bg: #333333;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: Arial, sans-serif; background: #f2f2f2; }

    header {
      background: var(--main-bg);
      color: var(--main-light);
      text-align: center;
      padding: 20px;
    }
    nav { margin-top: 10px; }
    nav a {
      color: var(--main-light);
      text-decoration: none;
      margin: 0 12px;
      font-weight: bold;
      padding: 6px 10px;
      border-radius: 6px;
    }
    nav a.active,
    nav a:hover { background: rgba(255, 255, 255, 0.2); }

    main { padding: 25px; max-width: 900px; margin: auto; }

    /* Generic card */
    .card {
      background: #fff;
      border-radius: 10px;
      padding: 25px;
      margin-bottom: 25px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.08);
    }

    /* Form styles */
    form label { margin-top: 10px; display: block; font-weight: 600; }
    form input, form select, form textarea {
      width: 100%; padding: 10px; margin-top: 4px;
      border: 1px solid #ccc; border-radius: 6px;
    }
    form button {
      background: var(--main-bg); color: var(--main-light);
      border: none; padding: 10px 18px; margin-top: 14px;
      border-radius: 6px; cursor: pointer; font-weight: bold;
    }
    form button:hover { opacity: 0.9; }

    /* Section visibility */
    section { display: none; }
    section.active { display: block; }

    footer {
      background: var(--dark-bg);
      color: var(--main-light);
      text-align: center;
      padding: 12px;
      margin-top: 30px;
    }
  </style>
</head>
<body>
  <header>
    <h1> muhir mood Road Traffic Management System 👩‍💻 </h1>
    <nav>
      <a href="#home"   id="link-home"   class="active">Home</a>
      <a href="#report" id="link-report">Report Incident</a>
      <a href="#traffic" id="link-traffic">Traffic Updates</a>
    </nav>
  </header>

  <!-- ⭐ HOME SECTION -->
  <section id="home" class="active">
    <main>
      <div class="card">
        <h2>Welcome</h2>
        <p>This platform helps you report road incidents and get real‑time traffic updates across Tanzania.</p>
        <p style="margin-top:15px;"><em>Drive safely and keep others informed!</em></p>
      </div>

      <img src="https://images.unsplash.com/photo-1544197150-b99a580bb7a8?auto=format&fit=crop&w=1200&q=60"
           alt="Road safety" style="width:100%; border-radius:10px; max-height:340px; object-fit:cover;">
    </main>
  </section>

  <!-- ⭐ REPORT SECTION -->
  <section id="report">
    <main>
      <div class="card">
        <h2>Report a Road Incident</h2>
        <form id="incidentForm">
          <label for="location">Location</label>
          <input type="text" id="location" name="location" placeholder="e.g. Morogoro Road, Dar es Salaam" required>

          <label for="type">Type of Incident</label>
          <select id="type" name="type">
            <option value="accident">Accident</option>
            <option value="traffic_jam">Traffic Jam</option>
            <option value="road_damage">Road Damage</option>
          </select>

          <label for="description">Description</label>
          <textarea id="description" name="description" rows="4" placeholder="Short description..." required></textarea>

          <button type="submit">Submit Report</button>
        </form>
      </div>
    </main>
  </section>

  <!-- ⭐ TRAFFIC SECTION -->
  <section id="traffic">
    <main>
      <div class="card">
        <h2>Latest Traffic Reports</h2>
        <ul id="trafficList" style="margin-left:18px; line-height: 1.8;">
          <!-- Example static items -->
          <li><strong>[Dodoma]</strong> Road blockage due to accident — <em>reported 2 hrs ago</em></li>
          <li><strong>[Mwanza]</strong> Heavy traffic near city centre — <em>reported 1 hr ago</em></li>
           <li><strong>[Arusha]</strong> helping  — <em>reported 3 hrs ago</em></li>
        </ul>
      </div>
    </main>
  </section>

  <footer>
    &copy; 2025 muhir mood Road Safety
  </footer>

  <!-- ⭐ JavaScript zote ziko hapa -->
  <script>
    /**********************
     * Simple SPA routing *
     **********************/
    const links = document.querySelectorAll("nav a");
    const sections = document.querySelectorAll("section");

    function setActive(page) {
      // Toggle link classes
      links.forEach(l => l.classList.toggle("active", l.id === "link-" + page));

      // Toggle sections
      sections.forEach(sec => sec.classList.toggle("active", sec.id === page));
    }

    // Handle navigation clicks
    links.forEach(l => {
      l.addEventListener("click", e => {
        e.preventDefault();
        const page = l.getAttribute("href").substring(1);
        window.location.hash = page;
        setActive(page);
      });
    });

    // Route on page load / hash change
    window.addEventListener("load", () => {
      const initial = location.hash.substring(1) || "home";
      setActive(initial);
    });
    window.addEventListener("hashchange", () => {
      const page = location.hash.substring(1);
      setActive(page);
    });

    /********************************
     * Handle incident form submit  *
     ********************************/
    document.getElementById("incidentForm").addEventListener("submit", e => {
      e.preventDefault();

      // Collect data (for now we just echo to UI)
      const loc = document.getElementById("location").value.trim();
      const type = document.getElementById("type").value;
      const desc = document.getElementById("description").value.trim();
      const timestamp = new Date().toLocaleString("en-GB", { hour: "2-digit", minute: "2-digit" });

      // Add to traffic list
      const li = document.createElement("li");
      li.innerHTML = `<strong>[${loc}]</strong> ${desc} — <em>reported at ${timestamp}</em>`;
      document.getElementById("trafficList").prepend(li);

      // Reset form & switch tab
      e.target.reset();
      window.location.hash = "traffic";
      setActive("traffic");
      alert("Incident submitted successfully! Thank you for your report.");
    });
  </script>
</body>
</html>
