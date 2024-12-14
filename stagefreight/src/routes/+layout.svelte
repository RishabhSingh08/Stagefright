<script>
  import "../app.css";

  let menuVisible = false;

  const toggleMenu = () => {
    menuVisible = !menuVisible;
    const menu = document.getElementById("menu");

    if (menuVisible) {
      menu.classList.remove("hidden");
    } else {
      menu.classList.add("hidden");
    }
  };
</script>


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

<nav class="fixed top-0 left-0 w-full bg-black text-white shadow-md z-50 border-b border-white">
  <div class="container mx-auto px-4 py-4 flex justify-between items-center">
    <div class="flex items-center space-x-4">
      <!-- Logo -->
      <a href="/" class="flex items-center space-x-2">
        <img src="/images/logo.png" alt="Stage Fright Logo" class="h-10 w-auto" />
      </a>
    </div>
    <!-- Hamburger menu for mobile -->
    <button id="menu-toggle" class="block lg:hidden text-white focus:outline-none">
      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
      </svg>
    </button>
    <div id="menu" class="hidden lg:flex lg:space-x-6 lg:items-center">
      <!-- Links -->
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
  <footer class="bg-black text-white p-4 text-center flex flex-col items-center space-y-4 lg:space-y-0 lg:flex-row lg:justify-between lg:items-center">
    <a href="/" class="flex items-center space-x-2">
      <img src="/images/logo.png" alt="Stage Fright Logo" class="h-12" />
    </a>
    <div class="text-sm text-center lg:text-left">
      <p>BPA 435 Website Design Team | STAGEFRIGHT | Plano West Senior High School</p>
      <p>Rishabh Singh | Plano, TX 2024</p>
    </div>
  </footer>
</section>
