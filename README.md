# MOVIE-KING-UG
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
<title>Movie King</title>
<style>
  /* Reset and base styles */
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  html {
    scroll-behavior: smooth;
  }

  body {
    font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
    background-color: #141414;
    color: #fff;
    overflow-x: hidden;
    min-height: 100vh;
  }

  /* Header */
  header {
    position: fixed;
    top: 0;
    width: 100%;
    height: 55px;
    background: rgba(20, 20, 20, 0.9);
    background: linear-gradient(to bottom, rgba(20,20,20,0.95), rgba(20,20,20,0.8));
    display: flex;
    align-items: center;
    padding: 0 20px;
    z-index: 1000;
  }

  header .logo {
    font-family: 'Bebas Neue', cursive, sans-serif;
    font-weight: 900;
    font-size: 28px;
    color: #FFD700;
    user-select: none;
    letter-spacing: 2px;
  }

  nav {
    margin-left: 40px;
    display: flex;
    gap: 20px;
    font-size: 14px;
  }

  nav a {
    color: #fff;
    text-decoration: none;
    font-weight: 600;
    cursor: pointer;
    white-space: nowrap;
  }

  nav a:hover,
  nav a:focus {
    color: #e50914;
    outline: none;
  }

  /* Focus outlines for accessibility */
  a:focus, button:focus, .thumbnail:focus {
    outline: 3px solid #ffd700;
    outline-offset: 2px;
  }

  /* Main Content */
  main {
    padding-top: 65px;
    padding-left: 10px;
    padding-right: 10px;
    max-width: 100%;
  }

  /* Section Title */
  section h2 {
    font-size: 20px;
    font-weight: 700;
    margin-bottom: 10px;
    padding-left: 10px;
  }

  section h3 {
    font-size: 18px;
    font-weight: 700;
    margin: 15px 0 10px 10px;
  }

  /* Row for thumbnails */
  .row {
    display: flex;
    overflow-x: auto;
    gap: 10px;
    padding-bottom: 20px;
    scroll-behavior: smooth;
  }
  .row::-webkit-scrollbar {
    display: none;
  }
  .row {
    -ms-overflow-style: none;
    scrollbar-width: none;
  }

  /* Thumbnail items */
  .thumbnail {
    flex: 0 0 auto;
    width: 140px;
    height: 200px;
    position: relative;
    cursor: pointer;
    border-radius: 6px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.6);
    transition: transform 0.3s ease;
    background-position: center;
    background-size: cover;
  }
  .thumbnail:hover,
  .thumbnail:focus {
    transform: scale(1.13);
    z-index: 10;
    box-shadow: 0 4px 16px rgba(229,9,20,0.9);
  }

  /* Hover overlay with movie title */
  .thumbnail .overlay {
    position: absolute;
    bottom: 0;
    width: 100%;
    background: rgba(0,0,0,0.7);
    color: #ffd700;
    font-weight: 600;
    font-size: 14px;
    padding: 6px 8px;
    border-bottom-left-radius: 6px;
    border-bottom-right-radius: 6px;
    opacity: 0;
    transition: opacity 0.3s ease;
    pointer-events: none;
  }
  .thumbnail:hover .overlay,
  .thumbnail:focus .overlay {
    opacity: 1;
    pointer-events: auto;
  }

  /* Modal overlay */
  .modal-overlay {
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    background-color: rgba(0,0,0,0.85);
    display: none;
    justify-content: center;
    align-items: center;
    z-index: 1500;
    padding: 20px;
  }
  .modal-overlay.active {
    display: flex;
  }

  /* Modal content */
  .modal-content {
    background-color: #222;
    border-radius: 10px;
    max-width: 350px;
    width: 100%;
    max-height: 580px;
    overflow-y: auto;
    box-shadow: 0 12px 40px rgba(229,9,20,0.8);
    outline: none;
  }

  /* Modal header */
  .modal-header {
    position: relative;
  }
  .modal-header img {
    width: 100%;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
    height: 200px;
    object-fit: cover;
  }

  /* Close button */
  .close-btn {
    position: absolute;
    top: 10px;
    right: 10px;
    background-color: rgba(229,9,20,0.9);
    border: none;
    border-radius: 50%;
    width: 28px;
    height: 28px;
    color: #fff;
    font-size: 20px;
    line-height: 28px;
    cursor: pointer;
    font-weight: 700;
    user-select: none;
    transition: background-color 0.3s ease;
  }
  .close-btn:hover,
  .close-btn:focus {
    background-color: #b0070f;
    outline: none;
  }

  /* Modal body */
  .modal-body {
    padding: 15px;
    line-height: 1.4;
  }
  .modal-body h3 {
    margin-bottom: 7px;
  }
  .modal-body p {
    font-size: 14px;
    margin-bottom: 6px;
  }

  /* Back to Top button */
  #back-to-top {
    position: fixed;
    bottom: 20px;
    right: 20px;
    background-color: #ffd700;
    color: #141414;
    padding: 10px 14px;
    border-radius: 50%;
    font-size: 18px;
    cursor: pointer;
    display: none;
    z-index: 2000;
    user-select: none;
    box-shadow: 0 4px 8px rgba(0,0,0,0.4);
    transition: background-color 0.3s ease;
  }
  #back-to-top:hover,
  #back-to-top:focus {
    background-color: #e5c100;
    outline: none;
  }

  /* Responsive adjustments */
  @media (max-width: 400px) {
    .thumbnail {
      width: 110px;
      height: 156px;
    }

    .modal-content {
      max-width: 320px;
      max-height: 560px;
    }
  }
</style>
</head>
<body>
<header>
  <div class="logo">MOVIE KING</div>
  <nav>
    <a href="#mosttrending-top" tabindex="0">Most Trending</a>
    <a href="#trending-top" tabindex="0">Trending Now</a>
    <a href="#toprated-top" tabindex="0">Top Rated</a>
    <a href="#movies-top" tabindex="0">Movies</a>
  </nav>
</header>

<main>
  <section id="mosttrending-top">
    <h2>Most Trending</h2>
    <div class="row" id="mosttrending-row">
      <!-- Most Trending thumbnails injected here -->
    </div>
  </section>
  <section id="trending-top">
    <h2>Trending Now</h2>
    <div class="row" id="trending-row">
      <!-- Trending thumbnails injected here -->
    </div>
  </section>
  <section id="toprated-top">
    <h2>Top Rated</h2>
    <div class="row" id="toprated-row">
      <!-- Top Rated thumbnails injected here -->
    </div>
  </section>
  <section id="movies-top">
    <h2>Movies</h2>
    <div id="movies-genres-container"></div>
  </section>
</main>

<button id="back-to-top" aria-label="Back to top" title="Back to top" tabindex="0">⬆</button>

<!-- Modal for detail -->
<div class="modal-overlay" id="modal" role="dialog" aria-modal="true" aria-labelledby="modal-title" aria-describedby="modal-description">
  <div class="modal-content" tabindex="0">
    <div class="modal-header">
      <button class="close-btn" id="close-modal" aria-label="Close modal">&times;</button>
      <img src="" alt="Title image" id="modal-img" loading="lazy" />
    </div>
    <div class="modal-body">
      <h3 id="modal-title"></h3>
      <p id="modal-description"></p>
      <p><strong>Year:</strong> <span id="modal-year"></span></p>
      <p><strong>Rating:</strong> <span id="modal-rating"></span></p>
    </div>
  </div>
</div>

<script>
  // Sample data for movies/shows
  const movies = {
    mosttrending: [
      {
        title: "Money Heist",
        year: "2017",
        rating: "TV-MA",
        description: "A criminal mastermind who goes by 'The Professor' plans the biggest heist in recorded history, to print billions of euros in the Royal Mint of Spain.",
        img: "https://occ-0-116-1723.1.nflxso.net/art/697f9/f2907012b742d3ff41b1c97e47a85a24e8a697f9.jpg"
      },
      {
        title: "Lupin",
        year: "2021",
        rating: "TV-MA",
        description: "Inspired by the adventures of Arsène Lupin, gentleman thief Assane Diop sets out to avenge his father for an injustice inflicted by a wealthy family.",
        img: "https://occ-0-116-1723.1.nflxso.net/art/5e067/216a32a7e91827aad7cc1a605d1fbc588345e067.jpg"
      },
      {
        title: "Cobra Kai",
        year: "2018",
        rating: "TV-14",
        description: "Decades after their 1984 fight, the rivalry between Johnny and Daniel reignites in a new Karate Kid saga.",
        img: "https://occ-0-116-1723.1.nflxso.net/art/e8d2e/09e0475ccbb4984b2dd9d2d5e77e2a6d225e8d2e.jpg"
      },
      {
        title: "The Umbrella Academy",
        year: "2019",
        rating: "TV-14",
        description: "A dysfunctional family of adopted sibling superheroes reunite to solve the mystery of their father's death and the threat of an apocalypse.",
        img: "https://occ-0-116-1723.1.nflxso.net/art/aea24/ade2e10fcbf586987654fe2335443c3a3a2aea24.jpg"
      }
    ],
    trending: [
      {
        title: "Stranger Things",
        year: "2016",
        rating: "TV-14",
        description: "When a young boy vanishes, a small town uncovers a mystery involving secret experiments, terrifying supernatural forces and one strange little girl.",
        img: "https://occ-0-116-1723.1.nflxso.net/art/a91ad/80b8df18093e2955d4a190c6821332aa828a91ad.jpg"
      },
      {
        title: "The Witcher",
        year: "2019",
        rating: "TV-MA",
        description: "Geralt, a mutated monster-hunter for hire, journeys toward his destiny in a turbulent world where people often prove more wicked than beasts.",
        img: "https://occ-0-116-1723.1.nflxso.net/art/6275f/24610c3737c311d50755a2177faaabd3f6a6275f.jpg"
      },
      {
        title: "Squid Game",
        year: "2021",
        rating: "TV-MA",
        description: "Hundreds of cash-strapped players accept a strange invitation to compete in children's games—with high stakes. But no one escapes deadly consequences.",
        img: "https://occ-0-116-1723.1.nflxso.net/art/e5f86/f423382c7e43d573f48d93762fc03bb1c6ee5f86.jpg"
      },
      {
        title: "Bridgerton",
        year: "2020",
        rating: "TV-MA",
        description: "Wealth, lust, and betrayal set in the backdrop of Regency-era London’s high society, as told through the powerful Bridgerton family.",
        img: "https://occ-0-116-1723.1.nflxso.net/art/e6e10/8e7ba26f4dd54a591b4fe075a7db7bff36ce6e10.jpg"
      }
    ],
    toprated: [
      {
        title: "Breaking Bad",
        year: "2008",
        rating: "TV-MA",
        description: "A chemistry teacher diagnosed with cancer starts producing crystal meth to secure his family's future, but gets drawn into a dangerous drug underworld.",
        img: "https://occ-0-116-1723.1.nflxso.net/art/58fd0/cd3bebdb0c317e5b7ecf920b2d78f9bddf158fd0.jpg"
      },
      {
        title: "Narcos",
        year: "2015",
        rating: "TV-MA",
        description: "A chronicled look at the criminal exploits of Colombian drug lord Pablo Escobar, as well as the many other drug kingpins who plagued the country.",
        img: "https://occ-0-116-1723.1.nflxso.net/art/4a73a/4606a1a2f5fdf9dff4db17cc8350d3f65064a73a.jpg"
      },
      {
        title: "Mindhunter",
        year: "2017",
        rating: "TV-MA",
        description: "In the late 1970s, two FBI agents expand criminal science by delving into the psychology of murder and getting uneasily close to all-too-real monsters.",
        img: "https://occ-0-116-1723.1.nflxso.net/art/cddbd/c31401e1e6ffc82a03ed63c4be5f35bf5f6cddbd.jpg"
      }
    ],
    genres: {
      Action: [
        {
          title: "Extraction",
          year: "2020",
          rating: "TV-MA",
          description: "A fearless black ops mercenary embarks on the most deadly mission of his career when he's enlisted to rescue the kidnapped son of an international crime lord.",
          img: "https://occ-0-116-1723.1.nflxso.net/art/d9788/7bf4bd3bbf4d15e5eacb1ffa46896f0ef18d9788.jpg"
        },
        {
          title: "6 Underground",
          year: "2019",
          rating: "TV-MA",
          description: "A tech billionaire fakes his death and secretly forms an elite squad to take down notorious criminals all over the world.",
          img: "https://occ-0-116-1723.1.nflxso.net/art/4fc3d/a2ddfb48564a8a1d858a6d124adfa1caf1b4fc3d.jpg"
        },
        {
          title: "John Wick",
          year: "2014",
          rating: "R",
          description: "An ex-hitman comes out of retirement to track down the gangsters that took everything from him.",
          img: "https://occ-0-116-1723.1.nflxso.net/art/414ae/7a9193679a79d0fbe664ebb3ab1a1bf6fe7414ae.jpg"
        }
      ],
      Comedy: [
        {
          title: "The Office",
          year: "2005",
          rating: "TV-14",
          description: "A mockumentary on a group of typical office workers, where the workday consists of ego clashes, inappropriate behavior, and tedium.",
          img: "https://occ-0-116-1723.1.nflxso.net/art/7f55d/8f5fe2fa928007fae47d6719babd89f0e0657f55d.jpg"
        },
        {
          title: "Parks and Recreation",
          year: "2009",
          rating: "TV-14",
          description: "The absurd antics of an Indiana town's public officials as they pursue sundry projects to make their city a better place.",
          img: "https://occ-0-116-1723.1.nflxso.net/art/3bcd7/a3807b067daae8b56da4d38c56af66bc3c053bcd7.jpg"
        }
      ],
      Horror: [
        {
          title: "The Haunting of Hill House",
          year: "2018",
          rating: "TV-MA",
          description: "Flashing between past and present, a fractured family confronts haunting memories of their old home and the terrifying events that drove them from it.",
          img: "https://occ-0-116-1723.1.nflxso.net/art/d7b30/f2e4f0dfda7d3f7d4c7c6c1e9e3d9606cc9d7b30.jpg"
        },
        {
          title: "Bird Box",
          year: "2018",
          rating: "R",
          description: "Five years after an ominous unseen presence drives most of society to suicide, a mother and her two children make a desperate bid to reach safety.",
          img: "https://occ-0-116-1723.1.nflxso.net/art/9ce82/91c6db55a46c5341d934c5a0c6af4f4c10439ce82.jpg"
        }
      ],
      Romance: [
        {
          title: "To All the Boys I've Loved Before",
          year: "2018",
          rating: "TV-14",
          description: "A teenage girl's secret love letters are exposed and wreak havoc on her life.",
          img: "https://occ-0-116-1723.1.nflxso.net/art/fb2e2/2204abcf10a9d283b72b8a497d7acb9a5d1fb2e2.jpg"
        },
        {
          title: "The Kissing Booth",
          year: "2018",
          rating: "TV-14",
          description: "A high school student is forced to confront her secret crush at a kissing booth.",
          img: "https://occ-0-116-1723.1.nflxso.net/art/4f1c0/c10a0e8a30fad3aaeb86a8442917bda6b2534f1c0.jpg"
        }
      ]
    }
  };

  // Creates a thumbnail element with overlay showing title
  function createThumbnail(movie) {
    const div = document.createElement('div');
    div.className = 'thumbnail';
    div.style.backgroundImage = `url('${movie.img}')`;
    div.setAttribute('tabindex', 0);
    div.setAttribute('aria-label', `${movie.title} (${movie.year})`);

    // Create overlay
    const overlay = document.createElement('div');
    overlay.className = 'overlay';
    overlay.textContent = movie.title;
    div.appendChild(overlay);

    // Interaction handlers
    div.addEventListener('click', () => openModal(movie));
    div.addEventListener('keypress', e => {
      if (e.key === 'Enter' || e.key === ' ') {
        e.preventDefault();
        openModal(movie);
      }
    });
    return div;
  }

  // Populate all rows and genres
  function populateRows() {
    const mostTrendingRow = document.getElementById('mosttrending-row');
    const trendingRow = document.getElementById('trending-row');
    const topratedRow = document.getElementById('toprated-row');
    const moviesGenresContainer = document.getElementById('movies-genres-container');

    movies.mosttrending.forEach(movie => {
      mostTrendingRow.appendChild(createThumbnail(movie));
    });
    movies.trending.forEach(movie => {
      trendingRow.appendChild(createThumbnail(movie));
    });
    movies.toprated.forEach(movie => {
      topratedRow.appendChild(createThumbnail(movie));
    });

    // Clear genres container if previously populated
    moviesGenresContainer.innerHTML = '';

    for (const genre in movies.genres) {
      // Create container for each genre row
      const genreSection = document.createElement('div');

      // Genre title
      const genreTitle = document.createElement('h3');
      genreTitle.textContent = genre;
      genreSection.appendChild(genreTitle);

      // Row container
      const rowDiv = document.createElement('div');
      rowDiv.className = 'row';

      movies.genres[genre].forEach(movie => {
        rowDiv.appendChild(createThumbnail(movie));
      });

      genreSection.appendChild(rowDiv);
      moviesGenresContainer.appendChild(genreSection);
    }
  }

  // Modal open functionality
  function openModal(movie) {
    const modal = document.getElementById('modal');
    const modalImg = document.getElementById('modal-img');
    const modalTitle = document.getElementById('modal-title');
    const modalDescription = document.getElementById('modal-description');
    const modalYear = document.getElementById('modal-year');
    const modalRating = document.getElementById('modal-rating');

    modalImg.src = movie.img;
    modalImg.alt = `${movie.title} image`;
    modalTitle.textContent = movie.title;
    modalDescription.textContent = movie.description;
    modalYear.textContent = movie.year;
    modalRating.textContent = movie.rating;

    modal.classList.add('active');
    document.body.style.overflow = 'hidden';

    // Trap focus inside modal
    trapFocus(modal.querySelector('.modal-content'));
  }

  // Modal close functionality
  function closeModal() {
    const modal = document.getElementById('modal');
    modal.classList.remove('active');
    document.body.style.overflow = '';
  }

  // Trap keyboard focus inside a container
  function trapFocus(element) {
    const focusableSelectors = 'a[href], area[href], input:not([disabled]), select:not([disabled]), textarea:not([disabled]), button:not([disabled]), iframe, object, embed, [tabindex]:not([tabindex="-1"]), [contenteditable]';
    const focusableElements = element.querySelectorAll(focusableSelectors);
    if (focusableElements.length === 0) return;
    const firstFocusable = focusableElements[0];
    const lastFocusable = focusableElements[focusableElements.length - 1];

    function handleKeyDown(e) {
      if (e.key === 'Tab') {
        if (e.shiftKey) { // Shift+Tab
          if (document.activeElement === firstFocusable) {
            e.preventDefault();
            lastFocusable.focus();
          }
        } else { // Tab
          if (document.activeElement === lastFocusable) {
            e.preventDefault();
            firstFocusable.focus();
          }
        }
      }
      if (e.key === 'Escape') {
        closeModal();
      }
    }

    element.addEventListener('keydown', handleKeyDown);

    // Focus first element initially
    firstFocusable.focus();

    // Remove listener on modal close
    const modal = document.getElementById('modal');
    function cleanup() {
      element.removeEventListener('keydown', handleKeyDown);
      modal.removeEventListener('transitionend', cleanup);
    }
    modal.addEventListener('transitionend', cleanup);
  }

  // Back to top button
  const backToTopBtn = document.getElementById('back-to-top');
  window.addEventListener('scroll', () => {
    if (window.scrollY > 300) {
      backToTopBtn.style.display = 'block';
    } else {
      backToTopBtn.style.display = 'none';
    }
  });

  backToTopBtn.addEventListener('click', () => {
    window.scrollTo({top: 0, behavior: 'smooth'});
  });
  backToTopBtn.addEventListener('keydown', e => {
    if (e.key === 'Enter' || e.key === ' ') {
      e.preventDefault();
      window.scrollTo({top: 0, behavior: 'smooth'});
    }
  });

  // Setup modal close event listeners
  document.getElementById('close-modal').addEventListener('click', closeModal);
  document.getElementById('modal').addEventListener('click', e => {
    if (e.target === e.currentTarget) {
      closeModal();
