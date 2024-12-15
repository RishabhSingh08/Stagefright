<script>
  import "../app.css";

  let menuVisible = false;

  const toggleMenu = () => {
    menuVisible = !menuVisible;
  };

  const closeMenu = () => {
    menuVisible = false;
  };
</script>

<style>
    @media (min-width: 1024px){
        .nav-link {
    position: relative;
    color: white;
    text-decoration: none;
    font-size: 1rem;
    font-weight: bold;
    transition: color 0.3s ease;
    display: block;
    padding: 0.5rem 0;
  }

  .nav-link::after {
    content: '';
    position: absolute;
    bottom: 6px;
    left: 0;
    width: 0;
    height: 1.5px;
    background-color: rgb(220 38 38);
    transition: width 0.3s ease;
  }

  .nav-link:hover {
    color: rgb(220 38 38);
  }

  .nav-link:hover::after {
    width: 100%;
  }
    }

</style>



<nav class="fixed top-0 left-0 w-full bg-black text-white shadow-md z-50 border-b border-white">
  <div class="container mx-auto px-4 py-2 flex justify-between items-center">
    <div class="flex items-center space-x-4">
      <a href="/" class="flex items-center space-x-2">
        <img src="/images/logo.png" alt="Stage Fright Logo" class="h-10 w-auto" />
      </a>
    </div>
    <button
    aria-label="Toggle Menu"
      id="menu-toggle"
      class="block lg:hidden text-white focus:outline-none"
      on:click={toggleMenu}
    >
      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
      </svg>
    </button>
    <div class="hidden lg:flex lg:space-x-6 lg:items-center">
      <a href="/tour" class="nav-link">Tour</a>
      <a href="/merch" class="nav-link">Merch</a>
      <a href="/contact" class="nav-link">Contact</a>
    </div>
  </div>
  {#if menuVisible}
    <div class="bg-black text-white flex flex-col px-4 space-y-2 lg:hidden border-t border-white py-2">
      <a href="/tour" class="nav-link border-b border-zinc-700  py-2" on:click={closeMenu}>Tour</a>
      <a href="/merch" class="nav-link border-b border-zinc-700  py-2" on:click={closeMenu}>Merch</a>
      <a href="/contact" class="nav-link py-2" on:click={closeMenu}>Contact</a>
    </div>
  {/if}
</nav>

<main>
  <slot />
</main>
<section class="border-t border-white">
  <footer class="bg-black text-white p-4 text-center flex flex-col items-center space-y-4 lg:space-y-0 lg:flex-row lg:justify-between lg:items-center">
    <a href="/" class="flex items-center space-x-2">
      <img src="/images/logo.png" alt="Stage Fright Logo" class="h-12" />
    </a>
    <div class="text-xs sm:text-sm text-center lg:text-left sm:block">
      <p class="sm:hidden">
        Rishabh Singh & Kaushal Ganapur | Plano West High School BPA | Stage Fright | Plano, Texas | 2024
      </p>
      <p class="hidden sm:block">
        Plano West High School BPA | Stage Fright | Plano, Texas | 2024
      </p>
    </div>
    <div class="text-xs sm:text-sm text-center lg:text-left sm:block">
      <p class="hidden sm:block">Rishabh Singh | Kaushal Ganapur | Aadwaith Sajin</p>
    </div>
  </footer>
</section>

