<script>
  let tourDates = [
    {
      date: "January 20, 2024",
      city: "Austin, TX",
      venue: "The Troubadour",
      ticketUrl: "https://example.com/tickets/austin",
      details: "Join us for an unforgettable night in the heart of Austin. Expect high energy and new tracks!"
    },
    {
      date: "February 10, 2024",
      city: "Los Angeles, CA",
      venue: "The Roxy Theatre",
      ticketUrl: "https://example.com/tickets/losangeles",
      details: "Stage Fright returns to LA! With special guests and new music, this show will be a blast."
    },
    {
      date: "March 5, 2024",
      city: "New York, NY",
      venue: "Madison Square Garden",
      ticketUrl: "https://example.com/tickets/newyork",
      details: "The big stage in New York awaits! Come experience Stage Fright live at one of the most iconic venues in the world."
    },
    {
      date: "April 10, 2024",
      city: "Chicago, IL",
      venue: "House of Blues",
      ticketUrl: "https://example.com/tickets/chicago",
      details: "Get ready for a rockin' night in Chicago with Stage Fright, at the legendary House of Blues!"
    },
    {
      date: "May 15, 2024",
      city: "San Francisco, CA",
      venue: "The Fillmore",
      ticketUrl: "https://example.com/tickets/sanfrancisco",
      details: "Stage Fright brings their electrifying live show to the Fillmore. You won't want to miss this one!"
    },
    {
      date: "June 22, 2024",
      city: "Nashville, TN",
      venue: "The Basement East",
      ticketUrl: "https://example.com/tickets/nashville",
      details: "Nashville, get ready for a night of high-energy rock with Stage Fright. Expect surprises and an unforgettable atmosphere!"
    },
    {
      date: "July 30, 2024",
      city: "Seattle, WA",
      venue: "Neumos",
      ticketUrl: "https://example.com/tickets/seattle",
      details: "Stage Fright hits the Pacific Northwest for an intense performance at Neumos. Be there to rock out!"
    },
    {
      date: "August 14, 2024",
      city: "Denver, CO",
      venue: "Bluebird Theater",
      ticketUrl: "https://example.com/tickets/denver",
      details: "Stage Fright takes the stage at Denver's iconic Bluebird Theater. Get ready for a night of unforgettable music!"
    },
    // Add more events as necessary
  ];
</script>

<section class="relative bg-black text-white py-24">
  <!-- Hero Image for Tour Section -->
  <div class="absolute inset-0">
    <!-- Background image for the tour section -->
    <img src="/images/band1.png" alt="Tour Hero Image" class="object-cover w-full h-full opacity-30" />
  </div>

  <!-- Content Container -->
  <div class="relative container mx-auto px-4">
    <!-- Title and Intro -->
    <h2 class="text-6xl font-bold text-center mb-12">TOURS & EVENTS</h2>
    <p class="text-xl text-center mb-12">Catch us live at one of these upcoming shows! Get your tickets today.</p>

    <!-- Highlighted Upcoming Show -->
    <div class="bg-gray-900 p-8 rounded-lg shadow-lg mb-12 border border-green-500">
      <h3 class="text-4xl font-semibold text-center text-green-400">{tourDates[0].city}</h3>
      <p class="text-lg text-gray-400 text-center mt-2">{tourDates[0].date}</p>
      <p class="text-lg text-gray-400 text-center mt-2">{tourDates[0].venue}</p>
      <p class="text-md mt-4 text-center">{tourDates[0].details}</p>
      <div class="flex justify-center mt-6">
        <a href={tourDates[0].ticketUrl} target="_blank" class="px-6 py-3 bg-green-500 text-black font-bold rounded-lg hover:bg-green-600 transition no-underline">Buy Tickets</a>
      </div>
    </div>

    <!-- Other Tour Dates -->
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-12">
      {#each tourDates.slice(1) as tour}
        <div class="bg-gray-900 p-6 rounded-lg shadow-lg transition-all duration-300 hover:scale-105 hover:border-green-500 border border-transparent">
          <h3 class="text-2xl font-semibold text-green-400">{tour.city}</h3>
          <p class="text-lg text-gray-400 mt-2">{tour.date}</p>
          <p class="text-lg text-gray-400 mt-2">{tour.venue}</p>
          <p class="text-sm mt-4">{tour.details}</p>
          <div class="mt-6">
            <a href={tour.ticketUrl} target="_blank" class="px-4 py-2 bg-gray-800 text-white rounded-lg hover:bg-green-600 transition no-underline text-sm">Buy Tickets</a>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>
