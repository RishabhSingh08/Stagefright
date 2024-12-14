<script>
  import { writable } from 'svelte/store';
  import { browser } from '$app/environment';

  // Shopping cart store to hold the cart data
  const cart = writable([]);

  // Product data
  const products = [
    {
      id: 1,
      name: "Stage Fright T-shirt",
      price: 20.00,
      image: "/images/shirt.png",
      description: "A high-quality cotton T-shirt with the Stage Fright logo.",
      sizes: ["S", "M", "L", "XL"]
    },
    {
      id: 2,
      name: "Stage Fright - Debut Album",
      price: 15.00,
      image: "/images/cd.png",
      description: "The debut album by Stage Fright, available on CD.",
      sizes: []  // No size for albums
    },
    {
      id: 3,
      name: "Stage Fright Cap",
      price: 25.00,
      image: "/images/cap.png",
      description: "A classic cap featuring the Stage Fright logo.",
      sizes: []  // No size for hats
    },
    {
      id: 4,
      name: "Stage Fright Hoodie",
      price: 40.00,
      image: "/images/hoodie.png",
      description: "Stay warm and stylish with the official Stage Fright hoodie.",
      sizes: ["S", "M", "L", "XL"]
    },
    {
      id: 5,
      name: "Stage Fright Poster",
      price: 10.00,
      image: "/images/band1.png",
      description: "A high-quality poster of Stage Fright in concert.",
      sizes: []  // No size for posters
    },
    {
      id: 6,
      name: "Stage Fright Shoes",
      price: 40.00,
      image: "/images/shoes.png",
      description: "High quality all-black shoes made for style.",
      sizes: ["S", "M", "L"]
    }
  ];

  // Handle adding item to cart
  const addToCart = (product, size) => {
    cart.update(items => {
      const existingItem = items.find(item => item.id === product.id && item.size === size);
      if (existingItem) {
        existingItem.quantity += 1;
      } else {
        items.push({ ...product, size, quantity: 1 });
      }
      return items;
    });
  };

  // Handle checkout
  const checkout = () => {
    alert("CHECKOUT");
  };

  let showModal = false;
  let selectedProduct = null;
  let selectedSize = 'S';

  // Initialize cart from localStorage
  let initialCart = [];
  if (browser) {
    const savedCart = localStorage.getItem('cart');
    initialCart = savedCart ? JSON.parse(savedCart) : [];
  }
  cart.set(initialCart);

  // Save cart to localStorage on change
  cart.subscribe((items) => {
    if (browser) {
      localStorage.setItem('cart', JSON.stringify(items));
    }
  });
</script>

<section class="relative bg-black text-white py-12 sm:py-8">
  <div class="absolute inset-0">
    <img src="/images/band1.png" alt="Tour Hero Image" class="object-cover w-full h-full opacity-30" />
  </div>

  <div class="relative container mx-auto px-4 sm:px-2 py-12 sm:py-8 flex flex-col md:grid md:grid-cols-12 gap-8">
    <!-- Merchandise Content -->
    <div class="order-1 md:order-none col-span-8">
      <h2 class="text-6xl sm:text-4xl font-bold text-center text-red-500 mb-12 sm:mb-8">MERCH</h2>
      <p class="text-lg sm:text-base text-center mb-8 sm:mb-6">Get your official Stage Fright gear! All items are limited edition, so act fast!</p>
      <div class="grid grid-cols-1 sm:grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 sm:gap-4">
        {#each products as product}
          <button
            type="button"
            on:click={() => { showModal = true; selectedProduct = product; }}
            class="bg-gray-900 p-6 sm:p-4 rounded-lg shadow-lg text-center cursor-pointer hover:scale-105 hover:border hover:border-red-500 transition"
            aria-label="View product details"
          >
            <img src={product.image} alt={product.name} class="w-full h-auto mb-4 rounded-md" />
            <h3 class="text-xl sm:text-lg font-semibold text-red-500">{product.name}</h3>
            <p class="text-sm sm:text-xs text-gray-400">${product.price.toFixed(2)}</p>
          </button>
        {/each}
      </div>
    </div>

    <!-- Cart Section -->
    <div class="order-2 md:order-none col-span-4 bg-gray-900 text-white p-6 sm:p-4 shadow-xl rounded-lg overflow-y-auto">
      <h3 class="text-2xl sm:text-xl font-semibold text-red-500 mb-6 sm:mb-4 text-center">Your Cart</h3>
      {#if $cart.length > 0}
        <ul class="space-y-4">
          {#each $cart as item}
            <li class="flex justify-between items-center border-b border-gray-700 pb-2">
              <div>
                <p class="font-semibold">{item.name} <span class="text-sm text-gray-400">({item.size})</span></p>
                <p class="text-sm sm:text-xs text-gray-400">x{item.quantity}</p>
              </div>
              <span class="text-red-500 font-semibold">${(item.price * item.quantity).toFixed(2)}</span>
            </li>
          {/each}
        </ul>
        <div class="mt-6 sm:mt-4">
          <div class="flex justify-between text-lg sm:text-base font-semibold border-t border-gray-700 pt-4">
            <span>Total:</span>
            <span class="text-red-500">${$cart.reduce((total, item) => total + item.price * item.quantity, 0).toFixed(2)}</span>
          </div>
          <button
            on:click={checkout}
            class="w-full mt-6 sm:mt-4 px-6 sm:px-4 py-3 sm:py-2 bg-red-500 text-white rounded-lg hover:bg-red-600 transition"
            aria-label="Proceed to checkout"
          >
            Checkout
          </button>
        </div>
      {:else}
        <p class="text-center text-gray-400 mt-12 sm:mt-8">Your cart is empty.</p>
      {/if}
    </div>
  </div>
</section>

<!-- Modal for Product Details -->
{#if showModal}
  <div class="fixed inset-0 bg-black bg-opacity-80 flex justify-center items-center z-50">
    <div class="bg-gray-900 text-white p-8 sm:p-6 rounded-lg w-96 sm:w-80 shadow-lg">
      <h3 class="text-3xl sm:text-2xl font-semibold text-red-500 mb-4">{selectedProduct.name}</h3>
      <img src={selectedProduct.image} alt={selectedProduct.name} class="w-full h-auto mb-4 rounded-md" />
      <p class="text-gray-400 sm:text-sm">{selectedProduct.description}</p>

      {#if selectedProduct.sizes.length > 0}
        <div class="mt-4">
          <label for="size" class="block text-sm sm:text-xs text-gray-400">Select Size</label>
          <select id="size" bind:value={selectedSize} class="mt-2 p-2 bg-gray-800 text-white border border-gray-700 rounded w-full">
            {#each selectedProduct.sizes as size}
              <option value={size}>{size}</option>
            {/each}
          </select>
        </div>
      {/if}

      <div class="mt-6 sm:mt-4 flex justify-between space-x-4">
        <button on:click={() => { addToCart(selectedProduct, selectedSize); showModal = false; }} class="flex-1 px-6 sm:px-4 py-3 sm:py-2 bg-red-500 text-white rounded-lg hover:bg-red-600 transition">Add to Cart</button>
        <button on:click={() => showModal = false} class="flex-1 px-6 sm:px-4 py-3 sm:py-2 bg-red-500 text-white rounded-lg hover:bg-red-600 transition">Close</button>
      </div>
    </div>
  </div>
{/if}
