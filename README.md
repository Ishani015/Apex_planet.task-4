# Apex_planet.task-4

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ApexPlanet Internship Task 4 - Full Project Implementation</title>
  <style>
    /* CSS RESET & GENERAL STYLES */
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    :root {
      --primary-color: #2b7a78;
      --secondary-color: #3aaf9f;
      --dark-color: #17252a;
      --light-color: #feffff;
      --bg-color: #f0f7f4;
      --accent-color: #def2f1;
    }
    body {
      background-color: var(--bg-color);
      color: var(--dark-color);
      display: flex;
      flex-direction: column;
      min-height: 100vh;
    }

    /* NAVIGATION */
    header {
      background-color: var(--primary-color);
      color: white;
      padding: 1rem 2rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      position: sticky;
      top: 0;
      z-index: 100;
    }
    .logo {
      font-size: 1.5rem;
      font-weight: bold;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    nav ul {
      display: flex;
      list-style: none;
      gap: 15px;
    }
    nav button {
      background: transparent;
      border: 1px solid transparent;
      color: white;
      padding: 8px 16px;
      font-size: 1rem;
      border-radius: 4px;
      cursor: pointer;
      transition: 0.3s;
    }
    nav button:hover, nav button.active {
      background-color: var(--secondary-color);
      border-color: white;
    }

    /* MAIN CONTENT LAYOUT */
    main {
      flex: 1;
      max-width: 1100px;
      width: 100%;
      margin: 20px auto;
      padding: 0 15px;
    }
    .tab-content {
      display: none;
      animation: fadeIn 0.4s ease-in-out;
    }
    .tab-content.active {
      display: block;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* UTILITY STYLES */
    .card {
      background: white;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
      margin-bottom: 20px;
    }
    .section-title {
      color: var(--primary-color);
      margin-bottom: 15px;
      border-bottom: 2px solid var(--accent-color);
      padding-bottom: 8px;
    }
    .btn {
      background-color: var(--primary-color);
      color: white;
      border: none;
      padding: 8px 16px;
      border-radius: 4px;
      cursor: pointer;
      font-size: 0.95rem;
      transition: 0.2s;
    }
    .btn:hover {
      background-color: var(--secondary-color);
    }
    .btn-danger {
      background-color: #e74c3c;
    }
    .btn-danger:hover {
      background-color: #c0392b;
    }

    /* =======================================
       1. PORTFOLIO SECTION
       ======================================= */
    .hero {
      text-align: center;
      padding: 40px 20px;
      background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
      color: white;
      border-radius: 8px;
      margin-bottom: 20px;
    }
    .hero h1 { font-size: 2.5rem; margin-bottom: 10px; }
    .hero p { font-size: 1.2rem; opacity: 0.9; }
    
    .portfolio-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 20px;
    }
    .skills-list {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-top: 10px;
    }
    .skill-tag {
      background-color: var(--accent-color);
      color: var(--primary-color);
      padding: 6px 12px;
      border-radius: 15px;
      font-weight: bold;
      font-size: 0.85rem;
    }
    .form-group {
      margin-bottom: 15px;
    }
    .form-group label {
      display: block;
      margin-bottom: 5px;
      font-weight: bold;
    }
    .form-group input, .form-group textarea {
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-size: 1rem;
    }

    /* =======================================
       2. TO-DO & NOTES SECTION
       ======================================= */
    .todo-input-container {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
    }
    .todo-input-container input {
      flex: 1;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    .task-list {
      list-style: none;
    }
    .task-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 12px 15px;
      background: #f9f9f9;
      border: 1px solid #eee;
      border-radius: 4px;
      margin-bottom: 10px;
      transition: 0.2s;
    }
    .task-item.completed span {
      text-decoration: line-through;
      color: #888;
    }
    .task-item span {
      cursor: pointer;
      flex: 1;
    }

    /* =======================================
       3. PRODUCT LISTING SECTION
       ======================================= */
    .product-controls {
      display: flex;
      flex-wrap: wrap;
      gap: 15px;
      margin-bottom: 20px;
      background: white;
      padding: 15px;
      border-radius: 8px;
      align-items: center;
    }
    .control-group {
      display: flex;
      flex-direction: column;
      gap: 5px;
    }
    .control-group select, .control-group input {
      padding: 8px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    .product-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
      gap: 20px;
    }
    .product-card {
      background: white;
      border-radius: 8px;
      padding: 15px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.05);
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      border: 1px solid #eee;
    }
    .product-img {
      width: 100%;
      height: 140px;
      background-color: var(--accent-color);
      border-radius: 4px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2.5rem;
      margin-bottom: 10px;
    }
    .product-title { font-weight: bold; margin-bottom: 5px; }
    .product-category { font-size: 0.8rem; color: #666; text-transform: uppercase; margin-bottom: 8px; }
    .product-meta {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 10px;
      font-weight: bold;
    }
    .product-price { color: var(--primary-color); font-size: 1.1rem; }
    .product-rating { color: #f39c12; font-size: 0.9rem; }

    /* FOOTER */
    footer {
      background-color: var(--dark-color);
      color: white;
      text-align: center;
      padding: 15px;
      margin-top: auto;
      font-size: 0.9rem;
    }
  </style>
</head>
<body>

  <!-- HEADER NAVIGATION -->
  <header>
    <div class="logo">
      <span>🌿</span> ApexPlanet Internship
    </div>
    <nav>
      <ul>
        <li><button class="nav-btn active" onclick="showTab('portfolio')">Portfolio</button></li>
        <li><button class="nav-btn" onclick="showTab('todo')">To-Do / Notes</button></li>
        <li><button class="nav-btn" onclick="showTab('products')">Products</button></li>
      </ul>
    </nav>
  </header>

  <!-- MAIN CONTAINER -->
  <main>
    
    <!-- TASK 1: PERSONAL PORTFOLIO WEBSITE -->
    <section id="portfolio" class="tab-content active">
      <div class="hero">
        <h1>Hello, I'm Ishani</h1>
        <p>Full-Stack Web Development Intern @ ApexPlanet</p>
      </div>

      <div class="portfolio-grid">
        <!-- About Section -->
        <div class="card">
          <h2 class="section-title">About Me</h2>
          <p>Passionate software engineering intern specializing in building interactive, user-friendly, and responsive web applications using modern programming tools and web technologies.</p>
          <h4 style="margin-top:15px;">Skills</h4>
          <div class="skills-list">
            <span class="skill-tag">HTML</span>
            <span class="skill-tag">C</span>
            <span class="skill-tag">C++</span>
            <span class="skill-tag">Java</span>
            <span class="skill-tag">Python</span>
          </div>
        </div>

        <!-- Projects Section -->
        <div class="card">
          <h2 class="section-title">Projects</h2>
          <ul style="list-style:none; line-height: 1.8;">
            <li>🚀 <strong>Personal Portfolio:</strong> Multi-section responsive site showcase.</li>
            <li>📝 <strong>Persistent To-Do App:</strong> Interactive local-storage task tracking.</li>
            <li>🛒 <strong>E-Commerce Catalog:</strong> Dynamic real-time product filter & sort page.</li>
          </ul>
        </div>
      </div>

      <!-- Contact Section -->
      <div class="card">
        <h2 class="section-title">Contact Me</h2>
        <form id="contactForm" onsubmit="handleContactSubmit(event)">
          <div class="form-group">
            <label for="name">Name</label>
            <input type="text" id="name" required placeholder="Enter your name">
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <input type="email" id="email" required placeholder="Enter your email">
          </div>
          <div class="form-group">
            <label for="message">Message</label>
            <textarea id="message" rows="4" required placeholder="Enter your message"></textarea>
          </div>
          <button type="submit" class="btn">Send Message</button>
        </form>
      </div>
    </section>

    <!-- TASK 2: TO-DO / NOTE-TAKING APP WITH LOCALSTORAGE -->
    <section id="todo" class="tab-content">
      <div class="card">
        <h2 class="section-title">To-Do & Note App (LocalStorage)</h2>
        <div class="todo-input-container">
          <input type="text" id="taskInput" placeholder="Add a new task or note...">
          <button class="btn" onclick="addTask()">Add Task</button>
        </div>

        <ul id="taskList" class="task-list"></ul>
      </div>
    </section>

    <!-- TASK 3: PRODUCT LISTING WITH FILTERING & SORTING -->
    <section id="products" class="tab-content">
      <div class="card">
        <h2 class="section-title">Product Showcase (Filter & Sort)</h2>
        
        <!-- Controls -->
        <div class="product-controls">
          <div class="control-group">
            <label for="categoryFilter">Category</label>
            <select id="categoryFilter" onchange="renderProducts()">
              <option value="all">All Categories</option>
              <option value="electronics">Electronics</option>
              <option value="fashion">Fashion</option>
              <option value="lifestyle">Lifestyle</option>
            </select>
          </div>

          <div class="control-group">
            <label for="sortBy">Sort By</label>
            <select id="sortBy" onchange="renderProducts()">
              <option value="default">Default</option>
              <option value="price-low">Price: Low to High</option>
              <option value="price-high">Price: High to Low</option>
              <option value="rating">Highest Rating</option>
            </select>
          </div>

          <div class="control-group">
            <label for="searchInput">Search</label>
            <input type="text" id="searchInput" placeholder="Search product..." oninput="renderProducts()">
          </div>
        </div>

        <!-- Product Grid -->
        <div id="productGrid" class="product-grid"></div>
      </div>
    </section>

  </main>

  <!-- FOOTER -->
  <footer>
    <p>&copy; Task - 4 Implementation | ApexPlanet Software Pvt Ltd Timeline: 9 Days</p>
  </footer>

  <!-- JAVASCRIPT LOGIC -->
  <script>
    /* =======================================
       GLOBAL / TAB NAVIGATION LOGIC
       ======================================= */
    function showTab(tabId) {
      document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active'));
      document.querySelectorAll('.nav-btn').forEach(btn => btn.classList.remove('active'));

      document.getElementById(tabId).classList.add('active');
      event.target.classList.add('active');
    }

    function handleContactSubmit(event) {
      event.preventDefault();
      alert('Thank you for reaching out! Your message has been sent successfully.');
      document.getElementById('contactForm').reset();
    }

    /* =======================================
       TO-DO LIST LOGIC (LOCALSTORAGE)
       ======================================= */
    function getTasksFromStorage() {
      return JSON.parse(localStorage.getItem('apexTasks')) || [];
    }

    function saveTasksToStorage(tasks) {
      localStorage.setItem('apexTasks', JSON.stringify(tasks));
    }

    function renderTasks() {
      const taskList = document.getElementById('taskList');
      const tasks = getTasksFromStorage();
      taskList.innerHTML = '';

      if (tasks.length === 0) {
        taskList.innerHTML = '<li style="text-align:center; color:#777; padding:10px;">No tasks added yet!</li>';
        return;
      }

      tasks.forEach((task, index) => {
        const li = document.createElement('li');
        li.className = `task-item ${task.completed ? 'completed' : ''}`;
        li.innerHTML = `
          <span onclick="toggleTask(${index})">${escapeHtml(task.text)}</span>
          <button class="btn btn-danger" onclick="deleteTask(${index})">Delete</button>
        `;
        taskList.appendChild(li);
      });
    }

    function addTask() {
      const input = document.getElementById('taskInput');
      const text = input.value.trim();
      if (!text) return;

      const tasks = getTasksFromStorage();
      tasks.push({ text: text, completed: false });
      saveTasksToStorage(tasks);
      input.value = '';
      renderTasks();
    }

    function toggleTask(index) {
      const tasks = getTasksFromStorage();
      tasks[index].completed = !tasks[index].completed;
      saveTasksToStorage(tasks);
      renderTasks();
    }

    function deleteTask(index) {
      const tasks = getTasksFromStorage();
      tasks.splice(index, 1);
      saveTasksToStorage(tasks);
      renderTasks();
    }

    function escapeHtml(text) {
      const div = document.createElement('div');
      div.innerText = text;
      return div.innerHTML;
    }

    /* =======================================
       PRODUCT LISTING LOGIC
       ======================================= */
    const productsData = [
      { id: 1, name: 'Wireless Headphones', category: 'electronics', price: 99, rating: 4.5, icon: '🎧' },
      { id: 2, name: 'Smart Watch', category: 'electronics', price: 149, rating: 4.8, icon: '⌚' },
      { id: 3, name: 'Running Shoes', category: 'fashion', price: 79, rating: 4.2, icon: '👟' },
      { id: 4, name: 'Leather Backpack', category: 'fashion', price: 59, rating: 4.0, icon: '🎒' },
      { id: 5, name: 'Stainless Water Bottle', category: 'lifestyle', price: 25, rating: 4.7, icon: '🧴' },
      { id: 6, name: 'Desk LED Lamp', category: 'lifestyle', price: 35, rating: 4.3, icon: '💡' }
    ];

    function renderProducts() {
      const grid = document.getElementById('productGrid');
      const category = document.getElementById('categoryFilter').value;
      const sortBy = document.getElementById('sortBy').value;
      const searchQuery = document.getElementById('searchInput').value.toLowerCase();

      // 1. Filter by category & search input
      let items = productsData.filter(item => {
        const matchesCategory = (category === 'all' || item.category === category);
        const matchesSearch = item.name.toLowerCase().includes(searchQuery);
        return matchesCategory && matchesSearch;
      });

      // 2. Sort items
      if (sortBy === 'price-low') {
        items.sort((a, b) => a.price - b.price);
      } else if (sortBy === 'price-high') {
        items.sort((a, b) => b.price - a.price);
      } else if (sortBy === 'rating') {
        items.sort((a, b) => b.rating - a.rating);
      }

      // 3. Render HTML
      grid.innerHTML = '';
      if (items.length === 0) {
        grid.innerHTML = '<p style="grid-column: 1/-1; text-align:center; padding: 20px;">No products matching criteria.</p>';
        return;
      }

      items.forEach(product => {
        const card = document.createElement('div');
        card.className = 'product-card';
        card.innerHTML = `
          <div>
            <div class="product-img">${product.icon}</div>
            <div class="product-category">${product.category}</div>
            <div class="product-title">${product.name}</div>
          </div>
          <div class="product-meta">
            <span class="product-price">$${product.price}</span>
            <span class="product-rating">★ ${product.rating}</span>
          </div>
        `;
        grid.appendChild(card);
      });
    }

    // INITIALIZATION ON PAGE LOAD
    document.addEventListener('DOMContentLoaded', () => {
      renderTasks();
      renderProducts();
    });
  </script>
</body>
</html>
