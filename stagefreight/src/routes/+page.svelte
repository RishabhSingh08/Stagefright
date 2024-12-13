<script>
  let members = [
    {
      name: "Alex Carter",
      role: "Lead Vocals and Rhythm Guitar",
      bio: "Alex Carter, born and raised in Austin, TX, is the dynamic lead vocalist and rhythm guitarist of Stage Fright. Growing up in a musically rich environment, Alex was introduced to the world of music at a young age, learning guitar from his father, who was a local blues musician. Over the years, Alex has honed his skills, blending his love for classic rock with modern influences. Known for his powerful voice and energetic stage presence, Alex's passion for songwriting and performing is the heart of Stage Fright's sound. He is currently based in Portland, OR, where he continues to shape the band's direction with his creative input.",
      image: "https://xsgames.co/randomusers/assets/avatars/male/2.jpg"
    },
    {
      name: "Mia Torres",
      role: "Lead Guitar and Backing Vocals",
      bio: "Mia Torres, born and raised in Los Angeles, CA, is the virtuoso lead guitarist and backing vocalist of Stage Fright. A child prodigy on the guitar, Mia started playing at the age of six, influenced by her mother, a former rock band guitarist herself. With over 12 years of experience, Mia has developed a unique style that fuses technical precision with raw emotion, drawing inspiration from iconic guitarists like Jimmy Page and Jimi Hendrix. Her intricate solos and harmonies provide a perfect complement to Alex’s vocals. Mia's adventurous spirit and love for exploring new musical genres make her an integral part of the band's ever-evolving sound.",
      image: "https://xsgames.co/randomusers/assets/avatars/female/20.jpg"
    },
    {
      name: "Ethan Brooks",
      role: "Bass Guitar",
      bio: "Ethan Brooks, originally from Seattle, WA, is the solid backbone of Stage Fright as the bass guitarist. With a deep passion for music that started in his teenage years, Ethan initially picked up the guitar before transitioning to bass, where he found his true calling. After relocating to Portland, OR, Ethan met Alex and began jamming, which led to the formation of Stage Fright. Known for his steady grooves and melodic basslines, Ethan's contributions are integral to the band's sound, adding depth and rhythm that anchor their music. Ethan is also a songwriter and often contributes to the band’s original compositions, adding his own unique flavor to the mix.",
      image: "https://xsgames.co/randomusers/assets/avatars/male/7.jpg"
    },
    {
      name: "Jenna Patel",
      role: "Drums and Percussion",
      bio: "Jenna Patel, hailing from Chicago, IL, is the powerhouse drummer and percussionist of Stage Fright. Growing up in a family of musicians, Jenna was always surrounded by music, and by the age of 12, she was playing drums in her school band. Her love for rhythm grew as she explored different styles, from jazz to punk rock, which now influences her energetic and versatile drumming style. After moving to Portland, OR, Jenna joined Stage Fright, where her precision and intensity behind the kit became a defining feature of their live performances. Jenna’s enthusiasm for experimenting with new sounds keeps the band's music fresh and innovative, driving their sound forward with every beat.",
      image: "https://xsgames.co/randomusers/assets/avatars/female/2.jpg"
    }
  ];

  let selectedMember = null;

  const openModal = (member) => {
    selectedMember = member;
  };

  const closeModal = () => {
    selectedMember = null;
  };

  let carouselImages = [
    "/images/band1.png",
    "/images/band2.png",
    "/images/band3.png",
    "/images/band4.png",
    "/images/band5.png",
    "/images/band6.png",

  ];

  let currentImageIndex = 0;

  const changeImage = () => {
    currentImageIndex = (currentImageIndex + 1) % carouselImages.length;
  };

  import { onMount } from "svelte";
  onMount(() => {
    const interval = setInterval(changeImage, 3000);
    return () => clearInterval(interval);
  });
</script>

<section class="relative w-full h-[60vh] md:h-[80vh] bg-gray-900">
  <div class="w-full h-full relative overflow-hidden">
    <div class="absolute inset-0 transition-opacity duration-1000" key={currentImageIndex}>
      <img
        src={carouselImages[currentImageIndex]}
        alt="Band image"
        class="object-cover w-full h-full"
      />
    </div>
  </div>
<div class="absolute inset-0 flex items-center justify-center text-center text-white z-10">
  <div class="p-6 bg-black bg-opacity-75 rounded-lg transition-all duration-500 transform hover:scale-105 hover:shadow-2xl hover:border-4 hover:border-green-400 hover:ring-2 hover:ring-green-400">
    <img src="/images/logo.png" alt="Stage Fright Logo" class="h-56 mx-auto" />
    <p class="mt-2 mb-2 text-xl font-medium text-gray-300 uppercase">Rocking the world with fresh sounds and energy-packed performances</p>
  </div>
</div>

</section>

<section id="about" class="bg-black text-white py-16">
  <div class="container mx-auto px-4">
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
      {#each members as member}
        <div
          class="bg-gray-900 p-6 rounded-lg shadow-lg text-center transform transition-transform hover:scale-105 hover:shadow-xl hover:border-2 hover:border-green-400 cursor-pointer"
          on:click={() => openModal(member)}
        >
          <img
            src={member.image}
            alt={member.name}
            class="w-32 h-32 rounded-full mx-auto mb-4 object-cover"
          />
          <h3 class="text-xl font-semibold text-green-400">{member.name}</h3>
          <p class="text-sm text-gray-400">{member.role}</p>
        </div>
      {/each}
    </div>
    <h2 class="text-3xl font-bold text-center text-green-400 mb-8 mt-16">About Stage Fright</h2>
    <p class="text-lg mb-8 text-center">Stage Fright was born in a small garage in Austin, TX, where Alex and Ethan first began jamming together after school.<br><br>What started as casual practice sessions quickly became a vision for something bigger. The duo soon connected with Mia and Jenna through mutual friends, and their chemistry was instant.<br><br>United by a shared love for rock and an ambition to create something fresh and authentic, the band started writing and performing original songs at local gigs. Over time, their energy-packed performances and heartfelt lyrics captured the attention of fans and critics alike.<br><br>Today, Stage Fright is on a mission to bring their music to stages everywhere, blending classic rock influences with a modern twist. Each member brings their own unique flair to the group, making Stage Fright a band that stands out and leaves a lasting impression.
  </div>
</section>

{#if selectedMember}
  <div class="fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center z-50 mt-8">
    <div class="bg-gray-900 text-white p-8 rounded-lg shadow-lg max-w-lg w-full">
      <div class="flex justify-between items-center mb-4">
        <h2 class="text-2xl font-bold text-green-400">{selectedMember.name}</h2>
        <button
          on:click={closeModal}
          class="text-xl text-gray-400 hover:text-white transition"
        >
          &times;
        </button>
      </div>
      <div class="text-center">
        <img
          src={selectedMember.image}
          alt={selectedMember.name}
          class="w-48 h-48 rounded-full mx-auto mb-4 object-cover border-4 border-green-400"
        />
        <h3 class="text-xl font-semibold text-green-400">{selectedMember.role}</h3>
        <p class="text-lg mt-4 text-gray-300">{selectedMember.bio}</p>
      </div>
    </div>
  </div>
{/if}
