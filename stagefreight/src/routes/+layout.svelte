<script>import "../app.css";</script>

<!-- <header class="bg-black text-white p-4">
</header> -->
<!-- src/routes/+layout.svelte -->
<style>
  .nav-link {
    position: relative;
    color: white;
    text-decoration: none;
    font-size: 1rem;
    font-weight: bold;
    transition: color 0.3s ease;
  }

  .nav-link:hover {
    color: rgb(220 38 38);
  }

  .nav-link::after {
    content: '';
    position: absolute;
    bottom: -2px;
    left: 0;
    width: 0;
    height: 2px;
    background-color: red;
    transition: width 0.3s ease;
  }

  .nav-link:hover::after {
    width: 100%;
  }
</style>

<head>
  <!-- index.html -->
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">

</head>

<nav class="fixed top-0 left-0 w-full bg-black text-white shadow-md z-50 border-b border-white">
  <div class="container mx-auto px-4 py-4 flex justify-between items-center">
    <div class="flex items-center space-x-4">
      <!-- Logo and Text wrapped in anchor tags to navigate to the home page -->
      <a href="/" class="flex items-center space-x-2">
        <img src="/images/logo.png" alt="Stage Fright Logo" class="h-10 w-auto" />
      </a>
    </div>
    <div class="space-x-6">
      <!-- Animated underline on hover -->
      <a href="/tour" class="nav-link">Tour</a>
      <a href="/merch" class="nav-link">Merch</a>
      <a href="/contact" class="nav-link">Contact</a>
    </div>
  </div>
</nav>



<main>
  <slot />
</main>

<section class="border-t border-white">

  <footer class=" bg-black text-white p-4 text-center flex justify-between items-center">
      <a href="/" class="flex items-center space-x-2">
        <img src="/images/logo.png" alt="Stage Fright Logo" class="h-12" />
      </a>
      <p>BPA 435 Website Design Team | STAGEFRIGHT | Plano West Senior High School</p>
      <p>Rishabh Singh | Plano, TX 2024</p>

  </footer>

</section>  
