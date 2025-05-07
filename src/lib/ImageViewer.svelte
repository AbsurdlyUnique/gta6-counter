<!--
  ImageViewer Component
  A fullscreen modal component for displaying images with animations and keyboard support
-->
<script>
  /**
   * Props for the ImageViewer component
   * @prop {string} src - URL of the image to display
   * @prop {string} alt - Alt text for accessibility
   * @prop {boolean} isOpen - Controls visibility of the viewer
   */
  export let src = '';
  export let alt = '';
  export let isOpen = false;

  /**
   * Closes the image viewer
   */
  function handleClose() {
    isOpen = false;
  }

  /**
   * Handles keyboard events for accessibility
   * @param {KeyboardEvent} event - The keyboard event
   */
  function handleKeydown(event) {
    if (event.key === 'Escape') {
      handleClose();
    }
  }
</script>

{#if isOpen}
  <div 
    class="image-viewer-overlay"
    on:click={handleClose}
    on:keydown={handleKeydown}
    role="dialog"
    aria-label="Image viewer"
    tabindex="0"
  >
    <button class="close-button" on:click={handleClose} aria-label="Close image viewer">×</button>
    <img {src} {alt} class="viewer-image" />
  </div>
{/if}

<style>
  /* Modal overlay with dark semi-transparent background */
  .image-viewer-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.9);
    z-index: 1000;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    animation: fadeIn 0.3s ease;
  }

  /* Main image display with size constraints and visual effects */
  .viewer-image {
    max-width: 90%;
    max-height: 90vh;
    object-fit: contain;
    border-radius: 4px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
    animation: scaleIn 0.3s ease;
  }

  /* Close button with hover effects */
  .close-button {
    position: absolute;
    top: 20px;
    right: 20px;
    background: none;
    border: none;
    color: white;
    font-size: 2rem;
    cursor: pointer;
    padding: 10px;
    line-height: 1;
    opacity: 0.8;
    transition: opacity 0.3s ease;
  }

  .close-button:hover {
    opacity: 1;
  }

  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }

  @keyframes scaleIn {
    from { 
      transform: scale(0.95);
      opacity: 0;
    }
    to { 
      transform: scale(1);
      opacity: 1;
    }
  }
</style>
