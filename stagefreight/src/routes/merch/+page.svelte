<style>
  /* Cart Styling */
  .cart {
    position: fixed; 
    top: 150px; 
    right: 0;
    width: 320px;
    height: auto;
    max-height: 70vh;
    background-color: #2d3748; 
    padding: 16px;
    overflow-y: auto;
    z-index: 50;
    color: white;
  }
  
  .cart h3 {
    font-size: 1.25rem;
    font-weight: 600;
  }

  .cart ul {
    list-style-type: none;
    padding: 0;
  }

  .cart li {
    display: flex;
    justify-content: space-between;
    padding: 8px 0;
  }

  .cart button {
    width: 100%;
    padding: 12px;
    background-color: #3182ce; /* bg-blue-500 */
    color: white;
    font-weight: 600;
    border-radius: 8px;
    border: none;
    cursor: pointer;
  }

  .cart button:hover {
    background-color: #2b6cb0; 
  }

  /* Footer Styling */
  footer {
    margin-top: 80px; 
    background-color: #1a202c; 
    padding: 20px 0;
    text-align: center;
    color: white;
  }
</style>

<script>
  import { writable } from 'svelte/store';

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
</script>




<section class="relative bg-black text-white py-16 pb-24">
    <div class="absolute inset-0">
    <!-- Background image for the tour section -->
    <img src="/images/band1.png" alt="Tour Hero Image" class="object-cover w-full h-full opacity-30" />
  </div>

  <div class="relative container mx-auto px-4 py-12">
    <h2 class="text-6xl font-bold text-center text-green-500 mb-12">MERCHANDISE</h2>
    <p class="text-lg text-center mb-8">Get your official Stage Fright gear! All items are limited edition, so act fast!</p>

    <!-- Merchandise Grid -->
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8">
      {#each products as product}
        <div class="bg-gray-900 p-6 rounded-lg shadow-lg text-center cursor-pointer hover:scale-105 hover:border hover:border-green-500 transition" on:click={() => { showModal = true; selectedProduct = product; }}>
          <img src={product.image} alt={product.name} class="w-full h-auto mb-4 rounded-md" />
          <h3 class="text-xl font-semibold text-green-500">{product.name}</h3>
          <p class="text-sm text-gray-400">${product.price.toFixed(2)}</p>
        </div>
      {/each}
    </div>
  </div>
</section>

<!-- Cart Sidebar -->
<div class="fixed top-40 right-4 w-96 max-h-[75vh] bg-gray-900 text-white p-6 shadow-xl rounded-lg overflow-y-auto transform transition-transform">
  <h3 class="text-2xl font-semibold text-green-500 mb-6 text-center">Your Cart</h3>
  {#if $cart.length > 0}
    <ul class="space-y-4">
      {#each $cart as item}
        <li class="flex justify-between items-center border-b border-gray-700 pb-2">
          <div>
            <p class="font-semibold">{item.name} <span class="text-sm text-gray-400">({item.size})</span></p>
            <p class="text-sm text-gray-400">x{item.quantity}</p>
          </div>
          <span class="text-green-500 font-semibold">${(item.price * item.quantity).toFixed(2)}</span>
        </li>
      {/each}
    </ul>
    <div class="mt-6">
      <div class="flex justify-between text-lg font-semibold border-t border-gray-700 pt-4">
        <span>Total:</span>
        <span class="text-green-500">${$cart.reduce((total, item) => total + item.price * item.quantity, 0).toFixed(2)}</span>
      </div>
      <button
        on:click={checkout}
        class="w-full mt-6 px-6 py-3 bg-green-500 text-white rounded-lg hover:bg-green-600 transition">
        Checkout
      </button>
    </div>
  {:else}
    <p class="text-center text-gray-400 mt-12">Your cart is empty.</p>
  {/if}
</div>


<!-- Modal for Product Details -->
{#if showModal}
  <div class="fixed inset-0 bg-black bg-opacity-80 flex justify-center items-center z-50">
    <div class="bg-gray-900 text-white p-8 rounded-lg w-96 shadow-lg">
      <h3 class="text-3xl font-semibold text-green-500 mb-4">{selectedProduct.name}</h3>
      <img src={selectedProduct.image} alt={selectedProduct.name} class="w-full h-auto mb-4 rounded-md" />
      <p class="text-gray-400">{selectedProduct.description}</p>

      {#if selectedProduct.sizes.length > 0}
        <div class="mt-4">
          <label for="size" class="block text-sm text-gray-400">Select Size</label>
          <select id="size" bind:value={selectedSize} class="mt-2 p-2 bg-gray-800 text-white border border-gray-700 rounded w-full">
            {#each selectedProduct.sizes as size}
              <option value={size}>{size}</option>
            {/each}
          </select>
        </div>
      {/if}

      <div class="mt-6 flex justify-between space-x-4">
        <button on:click={() => { addToCart(selectedProduct, selectedSize); showModal = false; }} class="flex-1 px-6 py-3 bg-green-500 text-white rounded-lg hover:bg-green-600 transition">Add to Cart</button>
        <button on:click={() => showModal = false} class="flex-1 px-6 py-3 bg-red-500 text-white rounded-lg hover:bg-red-600 transition">Close</button>
      </div>
    </div>
  </div>
{/if}
