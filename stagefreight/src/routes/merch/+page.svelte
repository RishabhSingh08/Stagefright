<script>
  import { writable } from 'svelte/store';
  import { browser } from '$app/environment';


const products = [
  {
    id: 1,
    name: "Stage Fright T-shirt",
    price: 25.00,
    image: "/images/shirt.png",
    description: "A premium cotton T-shirt with a bold Stage Fright logo, perfect for fans.",
    sizes: ["S", "M", "L", "XL"]
  },
  {
    id: 2,
    name: "Stage Fright Cap",
    price: 20.00,
    image: "/images/cap.png",
    description: "A sleek and stylish cap with the iconic Stage Fright logo, adjustable for all sizes.",
    sizes: [] 
  },
  {
    id: 3,
    name: "Stage Fright Hoodie",
    price: 50.00,
    image: "/images/hoodie.png",
    description: "Stay cozy with this soft, high-quality hoodie featuring the official Stage Fright design.",
    sizes: ["S", "M", "L", "XL"]
  },
  {
    id: 4,
    name: "Stage Fright Sweatshirt",
    price: 35.00,
    image: "/images/ss.png",
    description: "A durable and comfortable sweatshirt showcasing Stage Fright's unique artwork.",
    sizes: ["S", "M", "L", "XL"] 
  },
  {
    id: 5,
    name: "Stage Fright Poster",
    price: 12.00,
    image: "/images/Poster.png",
    description: "A poster with Stage Fright's logo, perfect for hanging up for show.",
    sizes: []
  }
];
  const cart = writable([]);

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

const removeItem = (itemToRemove) => {
  cart.update(items => {
    return items.filter(item => item.id !== itemToRemove.id || item.size !== itemToRemove.size);
  });
};

  let showModal = false;
  let selectedProduct = null;
  let selectedSize = 'S';

  let initialCart = [];
  if (browser) {
    const savedCart = localStorage.getItem('cart');
    initialCart = savedCart ? JSON.parse(savedCart) : [];
  }
  cart.set(initialCart);

  cart.subscribe((items) => {
    if (browser) {
      localStorage.setItem('cart', JSON.stringify(items));
    }
  });

    const checkout = () => {
  alert("We can't accept online orders right now");
  cart.set([]);
  };
</script>


<head>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css" />
</head>

<style>
    @keyframes popup {
    0% {
      transform: scale(0.8);
      opacity: 0;
    }
    100% {
      transform: scale(1);
      opacity: 1;
    }
  }

  .modal-enter {
    animation: popup 0.3s ease-out forwards;
  }
</style>

<section class="relative bg-black text-white py-12 sm:py-8 mt-12">
  <div class="absolute inset-0">
    <img src="/images/band1.png" alt="Tour Hero" class="object-cover w-full h-full opacity-30" />
  </div>

  <div class="relative container mx-auto px-4 sm:px-2 py-12 sm:py-8 flex flex-col md:grid md:grid-cols-12 gap-8">
    <div class="order-1 md:order-none col-span-8">
      <h2 class="text-6xl font-bold text-center text-red-500 mb-6">MERCH</h2>
      <p class="text-lg sm:text-base text-center mb-8 sm:mb-6">Get your official Stage Fright gear! All items are limited edition, so act fast!</p>
      <div class="grid grid-cols-1 sm:grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 sm:gap-4">
        {#each products as product}
          <button
            type="button"
            on:click={() => { showModal = true; selectedProduct = product; }}
            class="bg-zinc-900 p-6 sm:p-4 rounded-lg shadow-lg text-center cursor-pointer hover:scale-105 hover:border hover:border-red-500 transition"
            aria-label="View product details"
          >
            <img src={product.image} alt={product.name} class="w-full h-auto mb-4 rounded-md" />
            <h3 class="text-xl sm:text-lg font-semibold text-red-500">{product.name}</h3>
            <p class="text-sm sm:text-xs text-zinc-400">${product.price.toFixed(2)}</p>
          </button>
        {/each}
      </div>
    </div>

    <div class="order-2 md:order-none col-span-4 bg-zinc-900 text-white p-6 sm:p-4 shadow-xl rounded-lg overflow-y-auto">
      <h3 class="text-2xl sm:text-xl font-semibold text-red-500 mb-6 sm:mb-4 text-center">Your Cart</h3>
      {#if $cart.length > 0}
        <ul class="space-y-4">
          {#each $cart as item}
            <li class="flex justify-between items-center border-b border-zinc-700 pb-2">
              <div class="flex-1">
                <p class="font-semibold">{item.name} <span class="text-sm text-zinc-400">({item.size})</span></p>
                <p class="text-sm sm:text-xs text-zinc-400">x{item.quantity}</p>
              </div>
              <span class="text-red-500 font-semibold border-r pr-4 border-zinc-500">${(item.price * item.quantity).toFixed(2)}</span>
              <button 
                on:click={() => removeItem(item)} 
                class="text-sm text-red-500 hover:text-red-700 ml-4"
                aria-label="Remove item"
              >
                <i class="fa fa-trash" aria-hidden="true"></i>
              </button>
            </li>
          {/each}
        </ul>
        <div class="mt-6 sm:mt-4">
          <div class="flex justify-between text-lg sm:text-base font-semibold border-t border-zinc-700 pt-4">
            <span>Total:</span>
            <span class="text-red-500">${$cart.reduce((total, item) => total + item.price * item.quantity, 0).toFixed(2)}</span>
          </div>
          <button
            on:click={checkout}
            class="w-full mt-6 sm:mt-4 px-6 sm:px-4 py-3 sm:py-2 bg-red-500 text-white rounded-lg hover:bg-red-500 transition"
            aria-label="Proceed to checkout"
          >
            Checkout
          </button>
        </div>
      {:else}
        <p class="text-center text-zinc-400 mt-12 sm:mt-8">Your cart is empty.</p>
      {/if}
    </div>
  </div>
</section>

{#if showModal}
  <div class="fixed inset-0 bg-black bg-opacity-80 flex justify-center items-center z-50">
    <div class="bg-zinc-900 text-white p-8 sm:p-6 rounded-lg w-96 sm:w-80 shadow-lg modal-enter">
      <h3 class="text-3xl sm:text-2xl font-semibold text-red-500 mb-4">{selectedProduct.name}</h3>
      <img src={selectedProduct.image} alt={selectedProduct.name} class="w-full h-auto mb-4 rounded-md" />
      <p class="text-zinc-400 sm:text-sm">{selectedProduct.description}</p>

      {#if selectedProduct.sizes.length > 0}
        <div class="mt-4">
          <label for="size" class="block text-sm sm:text-xs text-zinc-400">Select Size</label>
          <select id="size" bind:value={selectedSize} class="mt-2 p-2 bg-zinc-800 text-white border border-zinc-700 rounded w-full">
            {#each selectedProduct.sizes as size}
              <option value={size}>{size}</option>
            {/each}
          </select>
        </div>
      {/if}

      <div class="mt-6 sm:mt-4 flex justify-between space-x-4">
        <button on:click={() => { addToCart(selectedProduct, selectedSize); showModal = false; }} class="flex-1 px-6 sm:px-4 py-3 sm:py-2 bg-red-500 text-white rounded-lg hover:bg-red-500 transition">Add to Cart</button>
        <button on:click={() => showModal = false} class="flex-1 px-6 sm:px-4 py-3 sm:py-2 bg-red-500 text-white rounded-lg hover:bg-red-500 transition">Close</button>
      </div>
    </div>
  </div>
{/if}
