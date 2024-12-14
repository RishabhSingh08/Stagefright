<script>
  import { onMount } from 'svelte';

  let confirmationMessage;
  let errorMessage;

  onMount(() => {
    const contactForm = document.getElementById('contactForm');
    confirmationMessage = document.getElementById('confirmationMessage');
    errorMessage = document.getElementById('errorMessage');

    contactForm.addEventListener('submit', (event) => {
      event.preventDefault(); // Prevent default submission

      const name = document.getElementById('name').value.trim();
      const email = document.getElementById('email').value.trim();
      const message = document.getElementById('message').value.trim();

      // Validate if any field is empty
      if (!name || !email || !message) {
        // Show error message
        errorMessage.classList.remove('hidden');
        confirmationMessage.classList.add('hidden'); // Ensure no conflicting message
        return; // Stop form submission
      }

      // Clear the error message if validation passes
      errorMessage.classList.add('hidden');

      // Clear the form fields
      contactForm.reset();

      // Display the confirmation message
      confirmationMessage.classList.remove('hidden');

      // Optionally hide the confirmation message after a few seconds
      setTimeout(() => {
        confirmationMessage.classList.add('hidden');
      }, 3000); // 3 seconds
    });
  });
</script>





<head>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css" />
</head>


<section class="bg-black text-white py-16">
  <div class="container mx-auto px-4">
    <h2 class="text-4xl md:text-6xl font-bold text-center text-red-500 my-12">CONTACT US</h2>
    <p class="text-lg text-center mb-8 text-zinc-300">
      Have a question? Want to book Stage Fright for an event? Reach out to us using the form below or find other ways to get in touch.
    </p>


    <!-- Contact Information Section -->
    <div class="grid grid-cols-1 md:grid-cols-2 gap-12 mb-12 p-8 bg-zinc-900 rounded-lg shadow-lg">
      <div class="md:pr-8 md:border-r md:border-zinc-600">
        <h3 class="text-2xl font-bold text-red-500 mb-4">Reach Out</h3>
        <p class="text-lg mb-4 text-zinc-300">
          You can contact us directly using the form, or feel free to reach out via email, phone, or through our social media pages.
        </p>
        <p class="text-lg font-semibold text-red-500 mb-2">Email:</p>
        <p class="text-lg text-zinc-300 mb-4">contact@stagefrightband.com</p>
        <p class="text-lg font-semibold text-red-500 mb-2">Phone:</p>
        <p class="text-lg text-zinc-300 mb-4">+1 (123) 456-7890</p>
        <p class="text-lg font-semibold text-red-500 mb-2">Address:</p>
        <p class="text-lg text-zinc-300">Stage Fright, 123 Music St., Los Angeles, CA, 90001</p>
      </div>

      <div class="md:pl-8">
        <h3 class="text-2xl font-bold text-red-500 mb-4">Follow Us</h3>
        <p class="text-lg mb-4 text-zinc-300">
          Stay connected with Stage Fright on our social media channels for the latest updates, news, and behind-the-scenes action!
        </p>
        <div class="flex space-x-6">
          <a href="https://facebook.com/stagefrightband" class="text-red-500 hover:text-red-500 transition" aria-label="Follow Stage Fright on Facebook">
            <i class="fab fa-facebook-square text-3xl"></i>
          </a>
          <a href="https://twitter.com/stagefrightband" class="text-red-500 hover:text-red-500 transition" aria-label="Follow Stage Fright on Twitter">
            <i class="fab fa-twitter text-3xl"></i>
          </a>
          <a href="https://instagram.com/stagefrightband" class="text-red-500 hover:text-red-500 transition" aria-label="Follow Stage Fright on Instagram">
            <i class="fab fa-instagram text-3xl"></i>
          </a>
          <a href="https://youtube.com/stagefrightband" class="text-red-500 hover:text-red-500 transition" aria-label="Follow Stage Fright on YouTube">
            <i class="fab fa-youtube text-3xl"></i>
          </a>
        </div>
      </div>
    </div>

    <!-- Contact Form Section -->
    <div class="max-w-lg mx-auto mb-12 p-8 bg-zinc-900 rounded-lg shadow-lg">
      <h3 class="text-3xl font-bold text-red-500 mb-4">Send Us a Message</h3>
      <p class="text-lg mb-8 text-zinc-300">We're happy to hear from you. Whether you want to book us for a show, ask a question, or send us feedback, fill out the form below and we’ll get back to you as soon as possible.</p>

<form id="contactForm" class="space-y-6">
  <div class="mb-4">
    <label for="name" class="block text-lg font-semibold text-red-500">Name</label>
    <input type="text" id="name" class="w-full px-4 py-2 bg-zinc-800 text-white rounded border border-zinc-600 focus:ring-2 focus:ring-red-500" placeholder="Your name" />
  </div>
  <div class="mb-4">
    <label for="email" class="block text-lg font-semibold text-red-500">Email</label>
    <input type="email" id="email" class="w-full px-4 py-2 bg-zinc-800 text-white rounded border border-zinc-600 focus:ring-2 focus:ring-red-500" placeholder="Your email address" />
  </div>
  <div class="mb-4">
    <label for="message" class="block text-lg font-semibold text-red-500">Message</label>
    <textarea id="message" class="w-full px-4 py-2 bg-zinc-800 text-white rounded border border-zinc-600 focus:ring-2 focus:ring-red-500" rows="5" placeholder="Your message"></textarea>
  </div>
  <button type="submit" class="w-full bg-red-500 hover:bg-red-500 text-black py-2 px-6 rounded-lg transition">Submit</button>
</form>

<!-- Error message -->
<p id="errorMessage" class="text-center text-lg text-red-500 mt-4 hidden">Missing Field!</p>

<!-- Confirmation message -->
<p id="confirmationMessage" class="text-center text-lg text-green-500 mt-4 hidden">Message Sent!</p>
    </div>

    <!-- Map Section -->
<div class="mb-12 p-8 bg-zinc-900 rounded-lg shadow-lg flex flex-col items-center justify-center">
  <h3 class="text-2xl font-bold text-red-500 text-center mb-4">Find Us</h3>
  <p class="text-lg text-zinc-300 text-center mb-8">We’re based in Los Angeles, but we travel the world! Here’s our location for any in-person inquiries:</p>
  <img src="images/map.png" alt="" class="scale-110 rounded-xl self-center my-4">
</div>
    <!-- FAQ Section -->
    <div class="mb-12 p-8 bg-zinc-900 rounded-lg shadow-lg">
      <h3 class="text-2xl font-bold text-red-500 text-center mb-4">Frequently Asked Questions</h3>
      <div class="space-y-6">
        <div>
          <p class="font-semibold text-red-500">1. How do I book Stage Fright for an event?</p>
          <p class="text-lg text-zinc-300">You can book Stage Fright by contacting us via the form above or visiting us directly <span class="text-red-500"><a href="https://www.gigsalad.com/Music-Groups/Party-Band" class="underline">Here</a></span>.</p>
        </div>
        <div>
          <p class="font-semibold text-red-500">2. What merchandise do you offer?</p>
          <p class="text-lg text-zinc-300">We offer a variety of merchandise including T-shirts, albums, hats, and more! You can view and purchase items on our Merchandise page.</p>
        </div>
        <div>
          <p class="font-semibold text-red-500">3. How can I get updates on upcoming shows?</p>
          <p class="text-lg text-zinc-300">Follow us on social media or subscribe to our newsletter to stay updated on our latest tours and events.</p>
        </div>
      </div>
    </div>
  </div>
</section>
