<script>
  import ImageViewer from './lib/ImageViewer.svelte';

  let selectedImage = $state({
    src: '',
    alt: '',
    isOpen: false
  });

  function openImageViewer(src, alt) {
    selectedImage = {
      src,
      alt,
      isOpen: true
    };
  }

  /**
   * Countdown Timer Configuration
   * Target date is set to GTA VI's announced release date
   * Using Svelte 5 Runes ($state and $derived) for reactive state management
   */
  let targetDate = new Date("2026-05-26T00:00:00Z");
  let now = $state(new Date());
  let timeRemaining = $derived(calculateTimeRemaining(targetDate, now));

  // Update current time every second
  setInterval(() => {
    now = new Date();
  }, 1000);

  /**
   * Calculate time remaining until the target date
   * @param {Date} endDate - The target date to count down to
   * @param {Date} currentDate - The current date to calculate from
   * @returns {Object} Object containing days, hours, minutes, and seconds remaining
   */
  function calculateTimeRemaining(endDate, currentDate) {
    const total = endDate.getTime() - currentDate.getTime();
    const seconds = Math.floor((total / 1000) % 60);
    const minutes = Math.floor((total / 1000 / 60) % 60);
    const hours = Math.floor((total / (1000 * 60 * 60)) % 24);
    const days = Math.floor(total / (1000 * 60 * 60 * 24));

    return {
      total,
      days,
      hours,
      minutes,
      seconds,
    };
  }


  /**
   * Asset Configuration
   * Contains paths to various images used throughout the site
   */
  const gta6KeyArtUrl = '/images/Jason_and_Lucia_02_With_Logos_landscape.jpg';
  const gta6TextLogoUrl = "https://www.rockstargames.com/VI/_next/image?url=%2FVI%2F_next%2Fstatic%2Fmedia%2FheroKeyArt.0338a8a4.png&w=1280";

  /**
   * Footer Character Images
   * Collection of transparent character silhouettes for the footer
   * One will be randomly selected to display above the footer
   */
  const footerImages = [
    '/images/Hero_FG.png',
    '/images/Hero_FG(1).png',
    '/images/Hero_FG(2).png',
    '/images/Hero_FG(3).png',
    '/images/Hero_FG(4).png',
    '/images/Hero_FG(5).png'
  ];

  const randomFooterImage = footerImages[Math.floor(Math.random() * footerImages.length)];

  // SVG strings for platform logos
  const ps5LogoSvg = `
    <svg xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 93 20" class="_1jyak1416 _1n4m2yu1 platform-svg-icon" aria-hidden="true" focusable="false">
      <g clip-path="url(#:r9v:)">
        <path d="M56.9502 16.0002C58.7302 16.0002 60.1802 14.5602 60.1802 12.7702V7.22023C60.1802 6.15023 61.0502 5.28023 62.1202 5.28023H68.3802C68.3802 5.28023 68.4702 5.24023 68.4702 5.19023V4.08023C68.4702 4.08023 68.4302 3.99023 68.3802 3.99023H60.8402C59.0602 3.99023 57.6102 5.43023 57.6102 7.22023V12.7702C57.6102 13.8402 56.7402 14.7102 55.6702 14.7102H49.5002C49.5002 14.7102 49.4102 14.7502 49.4102 14.8002V15.9102C49.4102 15.9102 49.4502 16.0002 49.5002 16.0002H56.9502Z" fill="currentColor"></path>
        <path d="M71.05 8.51V4.09C71.05 4.09 71.09 4 71.14 4H88.18C88.18 4 88.27 4.04 88.27 4.09V5.2C88.27 5.2 88.23 5.29 88.18 5.29H73.7C73.7 5.29 73.61 5.33 73.61 5.38V8.26C73.61 8.77 74.02 9.18 74.53 9.18H85.31C87.2 9.18 88.72 10.71 88.72 12.59C88.72 14.47 87.19 16 85.31 16H71.13C71.13 16 71.04 15.96 71.04 15.91V14.8C71.04 14.8 71.08 14.71 71.13 14.71H84.03C85.21 14.71 86.16 13.76 86.16 12.58C86.16 11.4 85.19 10.44 84.01 10.44H72.99C71.92 10.44 71.05 9.57 71.05 8.5V8.51Z" fill="currentColor"></path>
        <path d="M45.7401 9.17C46.8101 9.17 47.6801 8.3 47.6801 7.23C47.6801 6.16 46.8101 5.29 45.7401 5.29H32.6701C32.6701 5.29 32.5801 5.25 32.5801 5.2V4.09C32.5801 4.09 32.6201 4 32.6701 4H47.0301C48.8101 4 50.2601 5.44 50.2601 7.23C50.2601 9.02 48.8201 10.46 47.0301 10.46H37.1001C36.0301 10.46 35.1601 11.33 35.1601 12.4V15.92C35.1601 15.92 35.1201 16.01 35.0701 16.01H32.6801C32.6801 16.01 32.5901 15.97 32.5901 15.92V12.4C32.5901 10.62 34.0301 9.17 35.8201 9.17H45.7501H45.7401Z" fill="currentColor"></path>
        <path d="M9.69043 0V18.66L13.9204 20V4.35C13.9204 3.61 14.2504 3.12 14.7804 3.29C15.4704 3.48 15.6004 4.16 15.6004 4.89V11.14C18.2304 12.41 20.3004 11.14 20.3004 7.78C20.3004 4.42 19.0904 2.82 15.5104 1.59C14.1004 1.12 11.4904 0.33 9.69043 0Z" fill="currentColor"></path>
        <path d="M14.7207 17.2696L21.5107 14.8496C22.2807 14.5696 22.4007 14.1796 21.7707 13.9796C21.1407 13.7696 20.0107 13.8296 19.2407 14.1096L14.7207 15.6996V13.1596L14.9807 13.0696C14.9807 13.0696 16.2907 12.6096 18.1307 12.4096C19.9707 12.2096 22.2207 12.4396 23.9907 13.0996C25.9807 13.7296 26.2107 14.6596 25.7007 15.2996C25.1907 15.9396 23.9507 16.3996 23.9507 16.3996L14.7307 19.7096V17.2696H14.7207Z" fill="currentColor"></path>
        <path d="M1.94043 17.0095C-0.0995657 16.4395 -0.439566 15.2395 0.490434 14.5395C1.35043 13.9095 2.81043 13.4295 2.81043 13.4295L8.86043 11.2695V13.7295L4.51043 15.2895C3.74043 15.5695 3.62043 15.9495 4.24043 16.1595C4.87043 16.3695 5.99043 16.3095 6.77043 16.0295L8.86043 15.2795V17.4695C8.72043 17.4895 8.57043 17.5195 8.44043 17.5395C6.35043 17.8895 4.13043 17.7395 1.94043 17.0195V17.0095Z" fill="currentColor"></path>
        <path d="M24.2607 18C24.8507 18 25.2607 18.44 25.2607 19C25.2607 19.56 24.8607 20 24.2607 20C23.6607 20 23.2607 19.56 23.2607 19C23.2607 18.44 23.6707 18 24.2607 18ZM24.2607 19.85C24.7607 19.85 25.1007 19.47 25.1007 19C25.1007 18.53 24.7707 18.15 24.2607 18.15C23.7507 18.15 23.4207 18.53 23.4207 19C23.4207 19.47 23.7507 19.85 24.2607 19.85ZM23.8607 18.42H24.3207C24.5307 18.42 24.6907 18.48 24.6907 18.72C24.6907 18.86 24.6207 18.96 24.4807 19C24.5607 19.02 24.6107 19.08 24.6507 19.21C24.6907 19.34 24.7307 19.46 24.7607 19.57H24.5507C24.5207 19.48 24.4807 19.34 24.4607 19.26C24.4307 19.13 24.3907 19.08 24.2107 19.08H24.0707V19.57H23.8607V18.41V18.42ZM24.0707 18.94H24.2507C24.4007 18.94 24.4907 18.88 24.4907 18.75C24.4907 18.59 24.3807 18.57 24.2707 18.57H24.0707V18.94Z" fill="currentColor"></path>
        <path d="M91.3305 14.94H91.5105C91.6605 14.94 91.7505 14.88 91.7505 14.75C91.7505 14.59 91.6405 14.57 91.5305 14.57H91.3305V14.94ZM91.1205 14.42H91.5805C91.7905 14.42 91.9505 14.48 91.9505 14.72C91.9505 14.86 91.8805 14.96 91.7405 15C91.8205 15.02 91.8705 15.08 91.9105 15.21C91.9505 15.34 91.9905 15.46 92.0205 15.57H91.8105C91.7805 15.48 91.7405 15.34 91.7205 15.26C91.6905 15.13 91.6505 15.08 91.4705 15.08H91.3305V15.57H91.1205V14.41V14.42ZM91.5205 15.85C92.0205 15.85 92.3605 15.47 92.3605 15C92.3605 14.53 92.0205 14.15 91.5205 14.15C91.0205 14.15 90.6805 14.53 90.6805 15C90.6805 15.47 91.0105 15.85 91.5205 15.85ZM91.5205 14C92.1105 14 92.5205 14.44 92.5205 15C92.5205 15.56 92.1205 16 91.5205 16C90.9205 16 90.5205 15.56 90.5205 15C90.5205 14.44 90.9305 14 91.5205 14Z" fill="currentColor"></path>
      </g>
      <defs><clipPath id=":r9v:"><rect width="92.51" height="20" fill="currentColor" transform="translate(0 0.5)"></rect></clipPath></defs>
    </svg>
  `;
  const xboxLogoSvg = `
    <svg xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 158 20" class="_1jyak1416 _1n4m2yu1 platform-svg-icon" aria-hidden="true" focusable="false">
      <g clip-path="url(#:ra0:)">
        <path d="M10.5 8.02C10.5 8.02 10.53 8.02 10.53 8.04C13.52 10.31 18.64 15.94 17.08 17.53C15.32 19.07 13.02 20 10.5 20C7.98 20 5.68 19.07 3.92 17.53C2.36 15.94 7.48 10.31 10.47 8.04C10.47 8.04 10.49 8.02 10.5 8.02ZM15.71 1.46C14.18 0.55 12.52 0 10.5 0C8.48 0 6.82 0.55 5.29 1.46C5.27 1.47 5.26 1.49 5.27 1.51C5.27 1.53 5.3 1.53 5.32 1.53C7.26 1.11 10.2 2.78 10.48 2.95H10.5C10.5 2.95 10.51 2.95 10.52 2.95C10.8 2.78 13.74 1.11 15.68 1.53C15.7 1.53 15.72 1.53 15.73 1.51C15.73 1.49 15.73 1.47 15.71 1.46ZM3.5 2.87C3.5 2.87 3.47 2.89 3.46 2.9C1.63 4.71 0.5 7.22 0.5 10C0.5 12.28 1.26 14.38 2.54 16.06C2.55 16.08 2.58 16.09 2.59 16.08C2.61 16.08 2.61 16.05 2.6 16.03C1.84 13.67 5.74 7.96 7.75 5.56C7.75 5.56 7.76 5.54 7.76 5.53C7.76 5.52 7.76 5.51 7.74 5.5C4.7 2.46 3.67 2.78 3.5 2.87ZM13.25 5.49C13.25 5.49 13.23 5.51 13.23 5.52C13.23 5.53 13.23 5.54 13.24 5.55C15.25 7.95 19.15 13.66 18.39 16.02C18.39 16.04 18.39 16.06 18.4 16.07C18.42 16.08 18.44 16.07 18.45 16.05C19.73 14.37 20.49 12.27 20.49 9.99C20.49 7.22 19.36 4.7 17.53 2.89C17.52 2.88 17.5 2.86 17.49 2.86C17.32 2.77 16.29 2.45 13.24 5.49H13.25ZM35.3 16.16H33.25L29.73 11.31L26.21 16.16H24.16L28.71 9.9L24.52 4.14H26.57L29.74 8.5L32.91 4.14H34.96L30.77 9.9L35.32 16.16H35.3ZM45.92 12.74C45.92 13.8 45.57 14.64 44.88 15.24C44.19 15.85 43.19 16.15 41.9 16.15H36.26V10.8H33.58L34.69 9.27H36.25V4.14H41.65C42.86 4.14 43.8 4.43 44.45 5C45.1 5.57 45.42 6.34 45.42 7.27C45.42 8.43 44.9 9.3 43.86 9.88C44.53 10.14 45.04 10.52 45.38 11.01C45.73 11.51 45.9 12.09 45.9 12.75L45.92 12.74ZM38.1 9.27H41.55C42.24 9.27 42.77 9.11 43.12 8.81C43.47 8.5 43.64 8.04 43.64 7.42C43.64 6.89 43.46 6.47 43.1 6.17C42.74 5.87 42.22 5.72 41.55 5.72H38.1V9.27ZM44.07 12.71C44.07 12.08 43.88 11.6 43.5 11.28C43.12 10.96 42.55 10.8 41.79 10.8H38.09V14.57H41.79C42.52 14.57 43.09 14.41 43.48 14.09C43.87 13.77 44.06 13.3 44.06 12.71H44.07ZM58.27 10.15C58.27 11.08 58.14 11.93 57.87 12.69C57.6 13.44 57.2 14.12 56.67 14.7C56.13 15.28 55.5 15.72 54.8 16C54.09 16.29 53.29 16.43 52.42 16.43C51.55 16.43 50.73 16.28 50.02 16C49.31 15.71 48.69 15.27 48.16 14.7C47.62 14.13 47.21 13.46 46.94 12.7C46.67 11.95 46.53 11.09 46.53 10.16C46.53 9.23 46.67 8.38 46.94 7.62C47.21 6.86 47.62 6.18 48.16 5.6C48.69 5.03 49.31 4.59 50.02 4.31C50.73 4.02 51.53 3.88 52.42 3.88C53.31 3.88 54.09 4.02 54.8 4.31C55.51 4.6 56.14 5.03 56.67 5.6C57.2 6.18 57.61 6.86 57.87 7.62C58.14 8.38 58.27 9.23 58.27 10.16V10.15ZM48.44 10.15C48.44 11.56 48.81 12.7 49.53 13.52C50.24 14.35 51.21 14.78 52.41 14.78C53.61 14.78 54.58 14.36 55.29 13.52C56 12.71 56.36 11.57 56.36 10.15C56.36 8.73 56 7.58 55.29 6.76C54.57 5.94 53.6 5.52 52.41 5.52C51.22 5.52 50.25 5.94 49.53 6.76C48.81 7.61 48.44 8.75 48.44 10.15ZM64.07 9.9L68.26 4.14H66.21L63.04 8.5L59.87 4.14H57.82L62.01 9.9L57.46 16.16H59.51L63.03 11.31L66.55 16.16H68.6L64.05 9.9H64.07ZM83.9 5.79V9.27H89.87V10.8H83.9V14.5H90.65V16.15H82.06V4.14H90.65V5.79H83.9ZM79.68 10.59C79.08 10.04 78.08 9.61 76.72 9.32L75.68 9.1C74.69 8.89 74 8.63 73.63 8.33C73.27 8.05 73.08 7.64 73.08 7.1C73.08 6.56 73.29 6.16 73.7 5.87C74.11 5.58 74.71 5.44 75.49 5.44C76.49 5.44 77.23 5.62 77.68 5.98C78.13 6.34 78.38 6.91 78.44 7.68V7.7H80.26V7.68C80.24 6.5 79.82 5.56 79.03 4.89C78.24 4.22 77.04 3.88 75.48 3.88C74.18 3.88 73.13 4.18 72.37 4.77C71.61 5.36 71.22 6.16 71.22 7.15C71.22 8.14 71.54 8.92 72.17 9.49C72.8 10.05 73.74 10.46 74.97 10.71L76 10.93C77.01 11.15 77.73 11.41 78.11 11.69C78.5 11.97 78.69 12.38 78.69 12.9C78.69 13.54 78.45 14.04 77.98 14.38C77.51 14.72 76.82 14.89 75.95 14.89C74.89 14.89 74.08 14.66 73.54 14.22C73 13.78 72.72 13.1 72.7 12.21V12.19H70.86V12.21C70.87 13.59 71.32 14.65 72.2 15.37C73.08 16.09 74.33 16.45 75.91 16.45C77.37 16.45 78.52 16.13 79.35 15.49C80.18 14.85 80.59 13.96 80.59 12.85C80.59 11.92 80.29 11.17 79.68 10.61V10.59ZM101.7 14.68L101.58 12.81C101.56 12.15 101.41 11.61 101.14 11.21C100.88 10.82 100.46 10.54 99.91 10.37C100.52 10.17 101.01 9.81 101.35 9.33C101.7 8.83 101.88 8.21 101.88 7.48C101.88 6.45 101.51 5.62 100.77 5.03C100.04 4.44 99.01 4.14 97.74 4.14H92.49V16.16H94.33V11.23H97.8C98.49 11.23 98.99 11.39 99.3 11.7C99.61 12.02 99.78 12.56 99.82 13.33L99.87 14.61C99.88 15.31 100 15.82 100.23 16.15C100.46 16.48 102.12 16.15 102.12 16.15L102.1 16.12C101.89 15.76 101.75 15.27 101.7 14.66V14.68ZM94.33 5.72H97.65C98.41 5.72 98.99 5.88 99.4 6.2C99.8 6.52 100.01 7 100.01 7.63C100.01 8.26 99.81 8.79 99.42 9.15C99.03 9.5 98.48 9.68 97.79 9.68H94.34V5.71L94.33 5.72ZM103.54 16.16H105.38V4.14H103.54V16.16ZM115.8 5.79V4.14H107.21V16.16H115.8V14.51H109.05V10.81H115.02V9.28H109.05V5.8H115.8V5.79ZM125.59 10.59C124.99 10.04 123.99 9.61 122.63 9.32L121.59 9.1C120.6 8.89 119.91 8.63 119.54 8.33C119.18 8.05 118.99 7.64 118.99 7.1C118.99 6.56 119.2 6.16 119.61 5.87C120.02 5.58 120.62 5.44 121.4 5.44C122.4 5.44 123.14 5.62 123.59 5.98C124.04 6.34 124.29 6.91 124.35 7.68V7.7H126.17V7.68C126.15 6.5 125.73 5.56 124.94 4.89C124.15 4.22 122.95 3.88 121.39 3.88C120.09 3.88 119.04 4.18 118.28 4.77C117.52 5.36 117.13 6.16 117.13 7.15C117.13 8.14 117.45 8.92 118.08 9.49C118.71 10.05 119.65 10.46 120.88 10.71L121.91 10.93C122.92 11.15 123.64 11.41 124.02 11.69C124.41 11.97 124.6 12.38 124.6 12.9C124.6 13.54 124.36 14.04 123.89 14.38C123.42 14.72 122.73 14.89 121.86 14.89C120.8 14.89 119.99 14.66 119.45 14.22C118.91 13.78 118.63 13.1 118.61 12.21V12.19H116.77V12.21C116.78 13.59 117.23 14.65 118.11 15.37C118.99 16.09 120.24 16.45 121.82 16.45C123.28 16.45 124.43 16.13 125.26 15.49C126.09 14.85 126.5 13.96 126.5 12.85C126.5 11.92 126.2 11.17 125.59 10.61V10.59ZM145.14 2.64H144.22V17.67H145.14V2.64ZM136.73 9.9L140.92 4.14H138.87L135.7 8.5L132.53 4.14H130.48L134.67 9.9L130.12 16.16H132.17L135.69 11.31L139.21 16.16H141.26L136.71 9.9H136.73ZM156.91 10.59C156.31 10.04 155.31 9.61 153.95 9.32L152.91 9.1C151.92 8.89 151.23 8.63 150.86 8.33C150.5 8.05 150.31 7.64 150.31 7.1C150.31 6.56 150.52 6.16 150.93 5.87C151.34 5.58 151.94 5.44 152.72 5.44C153.72 5.44 154.46 5.62 154.91 5.98C155.36 6.34 155.61 6.91 155.67 7.68V7.7H157.49V7.68C157.47 6.5 157.05 5.56 156.26 4.89C155.47 4.22 154.27 3.88 152.71 3.88C151.41 3.88 150.36 4.18 149.6 4.77C148.84 5.36 148.45 6.16 148.45 7.15C148.45 8.14 148.77 8.92 149.4 9.49C150.03 10.05 150.97 10.46 152.2 10.71L153.23 10.93C154.24 11.15 154.96 11.41 155.34 11.69C155.73 11.97 155.92 12.38 155.92 12.9C155.92 13.54 155.68 14.04 155.21 14.38C154.74 14.72 154.05 14.89 153.18 14.89C152.12 14.89 151.31 14.66 150.77 14.22C150.23 13.78 149.95 13.1 149.93 12.21V12.19H148.09V12.21C148.1 13.59 148.55 14.65 149.43 15.37C150.31 16.09 151.56 16.45 153.14 16.45C154.6 16.45 155.75 16.13 156.58 15.49C157.41 14.85 157.82 13.96 157.82 12.85C157.82 11.92 157.52 11.17 156.91 10.61V10.59Z" fill="currentColor"></path>
      </g>
      <defs><clipPath id=":ra0:"><rect width="157.32" height="20" fill="currentColor" transform="translate(0.5)"></rect></clipPath></defs>
    </svg>
  `;

  const bentoItems = [

    // Lucia's Section
    {
      id: 'lucia-main',
      type: 'character',
      characterName: 'Lucia Caminos',
      tagline: "Fresh out of prison and ready to change the odds in her favor.",
      description: "Life has been coming at her swinging ever since. Fighting for her family landed her in the Leonida Penitentiary. Sheer luck got her out. Lucia's learned her lesson — only smart moves from here.",
      imageUrl: '/images/Lucia_Caminos_01.jpeg',
      colSpan: 'md:col-span-2',
      rowSpan: 'md:row-span-2',
    },
    {
      id: 'lucia-quote1',
      type: 'character',
      characterName: 'Lucia Caminos',
      tagline: "The only thing that matters is who you know and what you got.",
      imageUrl: '/images/Lucia_Caminos_02.jpeg',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'lucia-action1',
      type: 'image',
      imageUrl: '/images/Lucia_Caminos_03.jpeg',
      alt: 'Lucia in action',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'lucia-quote2',
      type: 'character',
      characterName: 'Lucia Caminos',
      tagline: "A life with Jason could be her way out.",
      imageUrl: '/images/Lucia_Caminos_04.jpeg',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'lucia-action2',
      type: 'image',
      imageUrl: '/images/Lucia_Caminos_05.jpeg',
      alt: 'Lucia ready for action',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'lucia-story',
      type: 'character',
      characterName: 'Lucia Caminos',
      tagline: "More than anything, Lucia wants the good life her mom has dreamed of since their days in Liberty City.",
      imageUrl: '/images/Lucia_Caminos_06.jpeg',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },

    // Jason's Section
    {
      id: 'jason-main',
      type: 'character',
      characterName: 'Jason Duval',
      tagline: "Jason wants an easy life, but things just keep getting harder.",
      description: "Jason grew up around grifters and crooks. After a stint in the Army trying to shake off his troubled teens, he found himself in the Keys doing what he knows best, working for local drug runners. It might be time to try something new.",
      imageUrl: '/images/Jason_Duval_01.jpeg',
      colSpan: 'md:col-span-2',
      rowSpan: 'md:row-span-2',
    },
    {
      id: 'jason-quote1',
      type: 'character',
      characterName: 'Jason Duval',
      tagline: "If anything happens, I'm right behind you.",
      imageUrl: '/images/Jason_Duval_02.jpeg',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'jason-action1',
      type: 'image',
      imageUrl: '/images/Jason_Duval_03.jpeg',
      alt: 'Jason in action',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'jason-quote2',
      type: 'character',
      characterName: 'Jason Duval',
      tagline: "Another day in paradise, right?",
      imageUrl: '/images/Jason_Duval_04.jpeg',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'jason-action2',
      type: 'image',
      imageUrl: '/images/Jason_Duval_05.jpeg',
      alt: 'Jason driving',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'jason-story',
      type: 'character',
      characterName: 'Jason Duval',
      tagline: "Meeting Lucia could be the best or worst thing to ever happen to him.",
      imageUrl: '/images/Jason_Duval_06.jpeg',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },

    // Location & Story Context
    {
      id: 'vice-city-main',
      type: 'character',
      characterName: 'Only in Leonida',
      tagline: "When the sun fades and the neon glows, everyone has something to gain — and more to lose.",
      imageUrl: '/images/Hero_BG(1).jpeg',
      colSpan: 'md:col-span-2',
      rowSpan: 'md:row-span-2',
    },
    {
      id: 'vice-city-night',
      type: 'image',
      imageUrl: '/images/Hero_BG(2).jpeg',
      alt: 'Vice City at night',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'vice-city-day',
      type: 'image',
      imageUrl: '/images/Hero_BG(3).jpeg',
      alt: 'Vice City during day',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },

    // Supporting Characters
    {
      id: 'cal-hampton',
      type: 'character',
      characterName: 'Cal Hampton',
      tagline: "What if everything on the internet was true?",
      description: "Jason's friend and a fellow associate of Brian's, Cal feels safest hanging at home, snooping on Coast Guard comms with a few beers and some private browser tabs open.",
      imageUrl: '/images/Cal_Hampton_01.jpeg',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'trailer',
      type: 'trailer',
      videoId: 'QdBZY2fkU-0',
      colSpan: 'md:col-span-2',
      rowSpan: 'md:row-span-2',
      title: 'Official Trailer 1'
    },
    {
      id: 'lucia',
      type: 'character',
      characterName: 'Lucia',
      tagline: "A life with Jason could be her way out.",
      imageUrl: '/images/Lucia_Caminos_03.jpeg',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'jason',
      type: 'character',
      characterName: 'Jason',
      tagline: "He's got a plan to reach the top.",
      imageUrl: '/images/Jason_Duval_04.jpeg',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'image-jason-driving',
      type: 'image',
      imageUrl: '/images/Jason_Duval_05.jpeg',
      alt: 'Jason driving a car',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'image-lucia-posing',
      type: 'image',
      imageUrl: '/images/Lucia_Caminos_05.jpeg',
      alt: 'Lucia posing with a gun',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'image-cal-hampton',
      type: 'image',
      imageUrl: '/images/Cal_Hampton_01.jpeg',
      alt: 'Cal Hampton character art',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'image-dre-quan',
      type: 'image',
      imageUrl: '/images/DreQuan_Priest_02.jpeg',
      alt: 'DreQuan Priest character art',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'image-raul-bautista',
      type: 'image',
      imageUrl: '/images/Raul_Bautista_03.jpeg',
      alt: 'Raul Bautista character art',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'image-vice-city-skyline',
      type: 'image',
      imageUrl: '/images/Hero_BG(1).jpeg',
      alt: 'Vice City skyline',
      colSpan: 'md:col-span-2',
      rowSpan: 'md:row-span-2',
    },
    {
      id: 'image-boobie-ike',
      type: 'image',
      imageUrl: '/images/Boobie_Ike_02.jpeg',
      alt: 'Boobie Ike character art',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'image-brian-heder',
      type: 'image',
      imageUrl: '/images/Brian_Heder_02.jpeg',
      alt: 'Brian Heder character art',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'image-real-dimez',
      type: 'image',
      imageUrl: '/images/Real_Dimez_02.jpeg',
      alt: 'Real Dimez character art',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'image-hero-fg-1',
      type: 'image',
      imageUrl: '/images/Hero_FG(3).png',
      alt: 'Hero Foreground Art 1',
      colSpan: 'md:col-span-2',
      rowSpan: 'md:row-span-1',
    },
    {
      id: 'image-hero-fg-2',
      type: 'image',
      imageUrl: '/images/Hero_FG(4).png',
      alt: 'Hero Foreground Art 2',
      colSpan: 'md:col-span-1',
      rowSpan: 'md:row-span-1',
    },
  ];

</script>

<!-- Main container for the entire application -->
<div class="container">
  <!-- Header with logo and disclaimer -->
  <header>
    <!-- Simple text logo -->
    <span class="header-logo">VI</span>
    <!-- Disclaimer about unofficial status -->
    <div class="header-disclaimer">
      This project is not affiliated with Rockstar Games - 
      <a href="https://www.rockstargames.com/VI" target="_blank" rel="noopener noreferrer">visit their official GTA VI site here</a>
    </div>
    <!-- Spacer for three-column layout -->
    <div class="header-spacer"></div>
  </header>

<main>
    <section class="hero-section">
      <img src={gta6KeyArtUrl} alt="Grand Theft Auto VI Key Art" class="hero-key-art-background-img" />
      <div class="hero-content-overlay">
        <div class="release-date-text">
          COMING MAY 26 2026
        </div>
        {#if timeRemaining.total > 0}
          <div class="countdown-timer">
            <div><span>{timeRemaining.days}</span> Days</div>
            <div><span>{timeRemaining.hours}</span> Hours</div>
            <div><span>{timeRemaining.minutes}</span> Minutes</div>
            <div><span>{timeRemaining.seconds}</span> Seconds</div>
          </div>
        {:else}
          <h2 class="released-text">RELEASED!</h2>
        {/if}
  </div>
      
      <div class="hero-details-footer">
        <div class="platform-logo-container">
          <div class="platform-logo platform-ps5">
            {@html ps5LogoSvg}
          </div>
          <div class="platform-logo platform-xbox">
            {@html xboxLogoSvg}
          </div>
        </div>
  </div>

      <div class="scroll-indicator">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M12 17L12 7" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/><path d="M16 13L12 17L8 13" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
      </div>
    </section>

    <section class="bento-section">
      <h2 class="bento-title">Characters &amp; Story</h2>


      <!-- Lucia's Section -->
      <h2 class="character-section-title">Lucia Caminos</h2>
      <div class="bento-grid">
        {#each bentoItems.filter(item => item.id.startsWith('lucia-')) as item (item.id)}
          <div class={`bento-item ${item.colSpan || ''} ${item.rowSpan || ''} item-type-${item.type}`}>
            {#if item.type === 'character'}
              <button 
                class="character-button"
                onclick={() => openImageViewer(item.imageUrl, `${item.characterName} - ${item.tagline}`)}
                aria-label={`View full size image of ${item.characterName}`}
              >
                <div class="bento-content character-content" style="background-image: url({item.imageUrl});">
                  <div class="character-overlay">
                    <h4>{item.characterName}</h4>
                    <p>{item.tagline}</p>
                    {#if item.description}
                      <p class="description">{item.description}</p>
                    {/if}
                  </div>
                </div>
              </button>
            {:else}
              <div class="bento-content image-content">
                <button 
                  class="image-button"
                  onclick={() => openImageViewer(item.imageUrl, item.alt || `${item.characterName} image`)}
                  aria-label="View full size image"
                >
                  <img 
                    src={item.imageUrl} 
                    alt={item.alt || `${item.characterName} image`} 
                    class="bento-img"
                  />
                </button>
              </div>
            {/if}
          </div>
        {/each}
      </div>

      <!-- Jason's Section -->
      <h2 class="character-section-title">Jason Duval</h2>
      <div class="bento-grid">
        {#each bentoItems.filter(item => item.id.startsWith('jason-')) as item (item.id)}
          <div class={`bento-item ${item.colSpan || ''} ${item.rowSpan || ''} item-type-${item.type}`}>
            {#if item.type === 'character'}
              <button 
                class="character-button"
                onclick={() => openImageViewer(item.imageUrl, `${item.characterName} - ${item.tagline}`)}
                aria-label={`View full size image of ${item.characterName}`}
              >
                <div class="bento-content character-content" style="background-image: url({item.imageUrl});">
                  <div class="character-overlay">
                    <h4>{item.characterName}</h4>
                    <p>{item.tagline}</p>
                    {#if item.description}
                      <p class="description">{item.description}</p>
                    {/if}
                  </div>
                </div>
              </button>
            {:else}
              <div class="bento-content image-content">
                <button 
                  class="image-button"
                  onclick={() => openImageViewer(item.imageUrl, item.alt || `${item.characterName} image`)}
                  aria-label="View full size image"
                >
                  <img 
                    src={item.imageUrl} 
                    alt={item.alt || `${item.characterName} image`} 
                    class="bento-img"
                  />
                </button>
              </div>
            {/if}
          </div>
        {/each}
      </div>

      <!-- Vice City Section -->
      <h2 class="character-section-title">Vice City</h2>
      <div class="bento-grid">
        {#each bentoItems.filter(item => !item.id.startsWith('lucia-') && !item.id.startsWith('jason-') && item.type !== 'trailer') as item (item.id)}
          <div class={`bento-item ${item.colSpan || ''} ${item.rowSpan || ''} item-type-${item.type}`}>
            {#if item.type === 'character'}
              <div class="bento-content character-content" style="background-image: url({item.imageUrl});">
                <div class="character-overlay">
                  <h4>{item.characterName}</h4>
                  <p>{item.tagline}</p>
                </div>
              </div>
            {:else if item.type === 'image'}
              <div class="bento-content image-content">
                <button 
                  class="image-button"
                  onclick={() => openImageViewer(item.imageUrl, item.alt || 'GTA VI Image')}
                  aria-label="View full size image"
                >
                  <img 
                    src={item.imageUrl} 
                    alt={item.alt || 'GTA VI Image'} 
                    class="bento-img"
                  />
                </button>
              </div>
            {/if}
          </div>
        {/each}
      </div>
    </section>

</main>

  <div class="footer-character-container">
    <img
      src={randomFooterImage}
      alt="Character Silhouette"
      class="footer-character-image"
    />
  </div>
  <footer>
    <div class="footer-content">
      <p class="footer-text">All images and information are property of Rockstar Games. This is a fan project.</p>
      <p class="footer-text">Visit the official GTA VI website at <a href="https://www.rockstargames.com/VI" target="_blank" rel="noopener noreferrer">rockstargames.com/VI</a></p>
    </div>
  </footer>

<ImageViewer 
  src={selectedImage.src}
  alt={selectedImage.alt}
  bind:isOpen={selectedImage.isOpen}
/>
</div>

<style>
  /* Global theme variables for consistent styling */
  :root {
    /* Brand colors */
    --gta-pink: #ff1493;
    --gta-orange: #ff8c00;
    --gta-purple: #8000ff;
    
    /* UI colors */
    --text-color: #e0e0e0;
    --bg-color: #0c0c0c;
    
    /* Layout */
    --container-padding: 20px;
    --bento-gap: 1rem;
    
    /* Typography */
    --font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif;
  }

  :global(body) {
    margin: 0;
    padding: 0;
    font-family: var(--font-family);
    background-color: var(--bg-color);
    color: var(--text-color);
  }

  .container {
    max-width: 100%;
    margin: 0 auto;
    padding: 0;
  }

  header {
    display: grid;
    grid-template-columns: auto 1fr auto;
    align-items: center;
    gap: clamp(20px, 4vw, 40px);
    padding: clamp(15px, 2vw, 20px) clamp(20px, 4vw, 40px);
    background-color: rgba(0,0,0,0.6);
    position: fixed;
    top: 0;
    left: 0;
    width: calc(100% - 2 * clamp(20px, 4vw, 40px));
    z-index: 1000;
    border-bottom: 1px solid rgba(255,255,255,0.1);
  }

  .header-logo {
    font-size: clamp(28px, 4vw, 40px);
    font-weight: bold;
    color: white;
    letter-spacing: 2px;
  }

  .header-disclaimer {
    font-size: clamp(11px, 1.5vw, 13px);
    color: #ccc;
    text-align: center;
    flex: 1;
  }

  .header-disclaimer a {
    color: var(--gta-pink);
    text-decoration: none;
    font-weight: 500;
  }

  .header-disclaimer a:hover {
    text-decoration: underline;
  }



  main {
    padding-top: 80px; 
  }

  .hero-section {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-end;
    min-height: 100vh; 
    background-color: var(--bg-color);
    overflow: hidden;
    position: relative;
  }

  .hero-key-art-background-img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: contain;
    object-position: center center; 
    z-index: 1;
  }
  
  .hero-content-overlay {
    position: absolute;
    top: 60%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 2;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    padding: 0;
    box-sizing: border-box;
    text-align: center;
  }

  .hero-text-logo-img {
    max-width: clamp(300px, 50vw, 600px);
    width: 70%;
    height: auto;
    margin-bottom: clamp(40px, 8vh, 80px);
  }

  .release-date-text {
    font-size: clamp(2.2rem, 6vw, 4.5rem);
    font-weight: bold;
    background: linear-gradient(90deg, var(--gta-orange), var(--gta-pink), var(--gta-purple));
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    margin-bottom: clamp(20px, 4vh, 40px);
    line-height: 1.1;
    text-transform: uppercase;
  }
  
  .released-text {
    font-size: clamp(2.2rem, 6vw, 4.5rem);
    color: var(--gta-pink);
    margin-bottom: clamp(20px, 4vh, 40px);
  }

  .countdown-timer {
    display: flex;
    justify-content: center;
    gap: clamp(10px, 2vw, 15px);
    margin-top: clamp(20px, 4vh, 40px);
    flex-wrap: wrap;
  }

  .countdown-timer div {
    background-color: rgba(20,20,20,0.8);
    padding: clamp(10px, 1.5vw, 15px) clamp(15px, 2.5vw, 25px);
    border-radius: 8px;
    min-width: clamp(70px, 15vw, 110px);
    text-align: center;
    border: 1px solid rgba(100,100,100,0.2);
  }

  .countdown-timer span {
    display: block;
    font-size: clamp(1.5rem, 3.5vw, 2.5rem);
    font-weight: bold;
    color: var(--text-color);
    line-height: 1.1;
  }


  .hero-details-footer {
    position: absolute;
    top: clamp(20px, 4vh, 40px);
    right: clamp(20px, 4vw, 40px);
    z-index: 2;
    display: flex;
    align-items: center;
  }

  .platform-logo-container {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 25px; 
    margin-bottom: clamp(10px, 2vh, 15px);  
  }

  .platform-logo {
    display: flex;
    align-items: center;
    color: #ccc;
  }

  .platform-logo :global(svg.platform-svg-icon) {
    height: clamp(24px, 3vh, 28px); 
    width: auto;
    fill: currentColor;
  }

  .release-notice {
    font-size: clamp(1.2rem, 2vw, 1.6rem);
    color: #fff;
    position: absolute;
    top: calc(50% + 80px);
    left: 50%;
    transform: translateX(-50%);
    z-index: 2;
    white-space: nowrap;
    text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
    background: linear-gradient(90deg, var(--gta-orange), var(--gta-pink), var(--gta-purple));
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    font-weight: bold;
  }

  .scroll-indicator {
    position: absolute;
    bottom: clamp(10px, 2vh, 20px);
    left: 50%;
    transform: translateX(-50%);
    z-index: 3; 
    animation: bounce 2s infinite;
  }

  @keyframes bounce {
    0%, 20%, 50%, 80%, 100% {
      transform: translate(-50%, 0);
    }
    40% {
      transform: translate(-50%, -10px);
    }
    60% {
      transform: translate(-50%, -5px);
    }
  }

  .bento-section {
    padding: clamp(30px, 5vw, 60px) var(--container-padding);
    background-color: #101010;
  }

  .bento-section h2.character-section-title {
    font-size: clamp(1.5rem, 3vw, 2.5rem);
    color: #fff;
    margin: clamp(40px, 6vh, 80px) 0 clamp(20px, 3vh, 40px);
    text-align: center;
    background: linear-gradient(90deg, var(--gta-orange), var(--gta-pink), var(--gta-purple));
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    font-weight: bold;
  }

  .bento-section h2.character-section-title:first-of-type {
    margin-top: 0;
  }

  .bento-title {
    font-size: clamp(2rem, 5vw, 3rem);
    color: var(--gta-pink);
    text-align: center;
    margin-bottom: clamp(20px, 4vw, 40px);
    font-weight: bold;
  }

  .bento-grid {
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    gap: var(--bento-gap);
    max-width: 1200px;
    margin: 0 auto;
  }
  @media (min-width: 768px) {
    .bento-grid {
      grid-template-columns: repeat(3, 1fr);
      grid-auto-rows: minmax(250px, auto); 
    }
  }

  .bento-item {
    background-color: #1a1a1a;
    border-radius: 12px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    border: 1px solid rgba(255,255,255,0.05);
  }
  .bento-item:hover {
      transform: translateY(-5px) scale(1.01);
      box-shadow: 0 10px 20px rgba(0,0,0,0.3);
  }

  .bento-content {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
  }
  

  .character-content {
    background-size: cover;
    background-position: center;
    position: relative;
    min-height: clamp(250px, 30vh, 400px);
    box-shadow: 0 10px 30px rgba(0,0,0,0.3);
    transition: transform 0.3s ease;
  }

  .image-button,
  .character-button {
    padding: 0;
    border: none;
    background: none;
    cursor: pointer;
    width: 100%;
    height: 100%;
    display: block;
    transition: transform 0.2s ease;
  }

  .image-button:hover,
  .character-button:hover {
    transform: scale(1.02);
  }

  .image-button:focus,
  .character-button:focus {
    outline: 2px solid var(--gta-pink);
    outline-offset: 2px;
  }

  .character-content:hover {
    transform: scale(1.02);
  }

  .character-content::before {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 70%;
    background: linear-gradient(to top, rgba(0,0,0,0.9), transparent);
    z-index: 1;
  }

  .character-overlay {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    padding: clamp(1rem, 2vw, 1.5rem);
    color: white;
    z-index: 2;
    color: #fff;
  }
  .character-overlay h4 {
    margin: 0 0 0.25rem 0;
    font-size: 1.3rem;
    font-weight: bold;
  }
  .character-overlay p {
    margin: 0;
    font-size: 0.9rem;
    color: #ccc;
  }

  .bento-img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
  }
  
  /* Spanning classes for grid items (applied based on bentoItems data) */
  @media (min-width: 768px) {
    .md\:col-span-1 { grid-column: span 1 / span 1; }
    .md\:col-span-2 { grid-column: span 2 / span 2; }
    .md\:col-span-3 { grid-column: span 3 / span 3; }
    .md\:row-span-1 { grid-row: span 1 / span 1; }
    .md\:row-span-2 { grid-row: span 2 / span 2; }
  }


  /* Footer Styles */
  .footer-character-container {
    position: relative;
    height: 400px;
    margin-top: -200px;
    display: flex;
    justify-content: flex-end;
    align-items: flex-end;
    pointer-events: none;
    padding-right: 0%;
  }

  .footer-character-image {
    height: 100%;
    width: auto;
    object-fit: contain;
    filter: drop-shadow(0 0 15px rgba(255, 255, 255, 0.15));
  }

  footer {
    position: relative;
    text-align: center;
    padding: 2rem;
    background-color: rgba(0, 0, 0, 0.8);
    border-top: 1px solid rgba(255, 255, 255, 0.1);
  }

  .footer-content {
    position: relative;
    z-index: 2;
    background: linear-gradient(to top, rgba(0, 0, 0, 0.9), rgba(0, 0, 0, 0.7));
    padding: 1rem;
    border-radius: 8px;
    max-width: 800px;
    margin: 0 auto;
  }

  .footer-text {
    color: #ccc;
    font-size: 0.9rem;
    margin: 0.5rem 0;
  }

  footer a {
    color: var(--gta-pink);
    text-decoration: none;
  }

  footer a:hover {
    text-decoration: underline;
  }

  /* Responsive Adjustments for Hero and general */
  @media (max-width: 767px) {
    main {
      padding-top: 70px; 
    }
    .hero-key-art-background-img {
      object-fit: cover; /* Cover might be better on mobile to fill screen */
      /* max-height: 60vh; Consider if contain makes it too small */
    }
    .hero-content-overlay {
        justify-content: center; 
        padding-bottom: clamp(20px, 5vh, 40px); 
    }
    .hero-details-footer {
        padding-bottom: clamp(40px, 8vh, 80px); /* Ensure space for scroll indicator if it was here */
    }
    .platform-logo-container {
        flex-direction: column;
        gap: 10px;
        margin-bottom: 10px;
    }
  }

</style>
