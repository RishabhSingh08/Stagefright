<script>
  import { onMount } from "svelte";
  let members = [
    {
      name: "Alex Carter",
      role: "Lead Vocals and Rhythm Guitar",
      bio: "Alex Carter, born and raised in Austin, TX, is the dynamic lead vocalist and rhythm guitarist of Stage Fright. Growing up in a musically rich environment, Alex was introduced to the world of music at a young age, learning guitar from his father, who was a local blues musician. Over the years, Alex has honed his skills, blending his love for classic rock with modern influences. Known for his powerful voice and energetic stage presence, Alex's passion for songwriting and performing is the heart of Stage Fright's sound. He is currently based in Austin, TX, where he continues to shape the band's direction with his creative input.",
      image: "https://xsgames.co/randomusers/assets/avatars/male/20.jpg"
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
      bio: "Ethan Brooks, originally from Seattle, WA, is the solid backbone of Stage Fright as the bass guitarist. With a deep passion for music that started in his teenage years, Ethan initially picked up the guitar before transitioning to bass, where he found his true calling. After meeting up with Ethan through school, it led to the formation of Stage Fright. Known for his steady grooves and melodic basslines, Ethan's contributions are integral to the band's sound, adding depth and rhythm that anchor their music. Ethan is also a songwriter and often contributes to the band’s original compositions, adding his own unique flavor to the mix.",
      image: "https://xsgames.co/randomusers/assets/avatars/male/10.jpg"
    },
    {
      name: "Jenna Anderson",
      role: "Drums and Percussion",
      bio: "Jenna Anderson, hailing from Chicago, IL, is the powerhouse drummer and percussionist of Stage Fright. Growing up in a family of musicians, Jenna was always surrounded by music, and by the age of 12, she was playing drums in her school band. Her love for rhythm grew as she explored different styles, from jazz to punk rock, which now influences her energetic and versatile drumming style. After moving to Austin, TX, Jenna joined Stage Fright, where her precision and intensity behind the kit became a defining feature of their live performances. Jenna’s enthusiasm for experimenting with new sounds keeps the band's music fresh and innovative, driving their sound forward with every beat.",
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

  onMount(() => {
    const interval = setInterval(changeImage, 3000);
    return () => clearInterval(interval);
  });

    let aboutCard;

  onMount(() => {
    const height = aboutCard.clientHeight;
    const width = aboutCard.clientWidth;

    const handleMove = (e) => {
      const xVal = e.layerX;
      const yVal = e.layerY;

      const yRotation = 20 * ((xVal - width / 2) / width);
      const xRotation = -20 * ((yVal - height / 2) / height);

      const transformString = `perspective(900px) scale(1.1) rotateX(${xRotation}deg) rotateY(${yRotation}deg)`;
      aboutCard.style.transform = transformString;
    };

    const resetTransform = () => {
      aboutCard.style.transform = "perspective(900px) scale(1) rotateX(0) rotateY(0)";
    };

    aboutCard.addEventListener("mousemove", handleMove);
    aboutCard.addEventListener("mouseout", resetTransform);
    aboutCard.addEventListener("mousedown", () => {
      aboutCard.style.transform = "perspective(900px) scale(0.9) rotateX(0) rotateY(0)";
    });
    aboutCard.addEventListener("mouseup", () => {
      aboutCard.style.transform = "perspective(900px) scale(1.1) rotateX(0) rotateY(0)";
    });

    return () => {
      aboutCard.removeEventListener("mousemove", handleMove);
      aboutCard.removeEventListener("mouseout", resetTransform);
    };
  });


  
</script>

<style>
  .aboutCard {
    transition: transform 0.1s, box-shadow 0.1s;
  }
  .aboutCard:hover {
    box-shadow: 0px 0px 30px rgba(0, 0, 0, 0.6);
    cursor: pointer;
  }

  @media (max-width: 640px){
  .aboutCard{
    margin-top: 5em;
    scale: .7;
  }
  }

  @keyframes modalPopup {
  from {
    transform: scale(0.9);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}

.modal {
  animation: modalPopup 0.3s ease-out forwards;
}

.memberCard::before{
  content:"";
  position:absolute;
  inset:0;
  background:linear-gradient(-45deg, hsla(0, 0%, 0%, 0) 60%, hsla(0, 0%, 100%, 0.5) 70%, hsla(0, 0%, 0%, 0), hsla(0, 0%, 0%, 0) 100% );
  transition:650ms ease;
  background-size: 250% 250%, 100% 100%;
  background-repeat:no-repeat;
  background-position: -500px -500px, 0 0;
}

.memberCard:hover{
  cursor:pointer;
}

.memberCard:hover::before{
  background-position: 280px 280px, 0 0;
}

</style>

<section class="relative w-full h-[40vh] sm:h-[60vh] md:h-[80vh] bg-zinc-900">
  <div class="w-full h-full relative overflow-hidden ">
    <div class="absolute inset-0 transition-opacity duration-1000" key={currentImageIndex}>
      <img
        src={carouselImages[currentImageIndex]}
        alt="Band"
        class="object-cover w-full h-full"
      />
    </div>
  </div>
<div
  class="absolute inset-0 flex items-center justify-center text-center text-white z-10 px-4"
>
  <div
    bind:this={aboutCard}
    class="aboutCard p-4 bg-black bg-opacity-75 rounded-lg transition-all duration-500 transform hover:scale-105 hover:shadow-2xl hover:border-4 hover:border-red-800 mt-4"
  >
    <img
      src="/images/logo.png"
      alt="Stage Fright Logo"
      class="h-24 sm:h-32 md:h-40 mx-auto"
    />
    <p
      class="mt-2 text-sm sm:text-base md:text-xl font-medium text-zinc-300 uppercase"
    >
      Rocking the world with fresh sounds and energy-packed performances
    </p>
  </div>
</div>
</section>


<section id="about" class="bg-black text-white py-8 sm:py-12 lg:py-16">
  <div class="container mx-auto px-4">
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
      {#each members as member}
<button
  type="button"
  class="memberCard bg-gradient-to-br from-zinc-800 to-zinc-900 p-6 rounded-lg shadow-lg border border-zinc-700 text-center transform transition-transform hover:scale-105 hover:shadow-2xl hover:border-red-500 cursor-pointer focus:outline-none"
  on:click={() => openModal(member)}
>
  <img
    src={member.image}
    alt={member.name}
    class=" w-28 h-28 md:w-32 md:h-32 rounded-full mx-auto mb-4 object-cover border-4 border-zinc-700"
  />
  <h3 class="text-lg font-semibold text-red-500">{member.name}</h3>
  <p class="text-sm text-zinc-400">{member.role}</p>
</button>

      {/each}
    </div>
    <h2 class="text-3xl sm:text-4xl lg:text-5xl font-bold text-center text-red-500 my-12">
      About Stage Fright
    </h2>
    <p class="text-base lg:text-lg text-center text-zinc-300 leading-relaxed max-w-3xl mx-auto">
      Stage Fright was born in a small garage in Austin, TX, where Alex and Ethan first began
      jamming together after school. What started as casual practice sessions quickly became a vision for something bigger. 
      The duo soon connected with Mia and Jenna through mutual friends, and their chemistry was instant. 
      United by a shared love for rock and an ambition to create something fresh and authentic, the band started writing and performing original songs at local gigs. 
      Over time, their energy-packed performances and heartfelt lyrics captured the attention of fans and critics alike.
    </p>
  </div>
</section>

{#if selectedMember}
<div class="fixed inset-0 bg-black bg-opacity-80 flex items-center justify-center z-50 px-4">
  <div class="modal bg-gradient-to-t from-zinc-800 to-zinc-900 p-8 sm:p-10 rounded-xl shadow-xl max-w-lg w-full relative border border-zinc-700">
    <button
      on:click={closeModal}
      class="absolute top-3 right-3 text-2xl text-zinc-400 hover:text-white transition transform hover:scale-110"
    >
      &times;
    </button>
    
    <div class="text-center">
      <img
        src={selectedMember.image}
        alt={selectedMember.name}
        class="w-36 h-36 sm:w-40 sm:h-40 md:w-48 md:h-48 rounded-full mx-auto mb-6 object-cover border-4 border-red-500 shadow-md"
      />
      <h2 class="text-xl sm:text-2xl lg:text-3xl font-bold text-red-500">{selectedMember.name}</h2>
      <h3 class="text-sm sm:text-base text-zinc-400 mt-2">{selectedMember.role}</h3>
      <p class="text-sm sm:text-base text-zinc-300 mt-4 leading-relaxed">
        {selectedMember.bio}
      </p>
    </div>
    
    <div class="mt-8 flex justify-center space-x-4">
      <button on:click={closeModal} class="px-4 py-2 bg-zinc-700 text-white rounded-md shadow-md hover:bg-zinc-600 transition">
        Close
      </button>
    </div>
  </div>
</div>
{/if}
