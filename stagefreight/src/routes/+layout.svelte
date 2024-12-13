<script>import "../app.css";</script>

<!-- <header class="bg-black text-white p-4">
</header> -->
<!-- src/routes/+layout.svelte -->

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
      <!-- Removed the Home button -->
      <a href="/tour" class="hover:text-gray-400">Tour</a>
      <a href="/merch" class="hover:text-gray-400">Merch</a>
      <a href="/contact" class="hover:text-gray-400">Contact</a>
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
      <p>&copy; 2024 Stage Fright. All rights reserved.</p>
  </footer>

</section>  
