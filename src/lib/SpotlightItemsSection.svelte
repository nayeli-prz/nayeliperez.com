<script lang="ts">
  import SpotlightItem from './SpotlightItem.svelte';
  let {variant} = $props<{variant: 'desktop' | 'mobile'}>();

  // Carousel state for mobile
  let currentIndex = $state(0);
  let carouselContainer = $state<HTMLDivElement | undefined>(undefined);
  let isDragging = $state(false);
  let startX = $state(0);
  let scrollLeft = $state(0);
  let lastDragDistance = $state(0); // Track drag distance for direction-based snapping
  let lastX = $state(0); // Track last position for delta-based movement

  const items: {heading?: string; content: string}[] = [
    {
      //heading: "Currently",
      content: `Available for product design, strategy, and systems-thinking work - let's talk about your project!`,
    },
    {
      heading: "In the works",
      content: `Building <a href="https://www.circularsanantonio.org/projects/directory" target="blank"><span class="text-base-500">San Antonio's Circular Directory</span></a> in partnership with Circular San Antonio.`,
    }
    // Add more items here as needed
  ];

  function goToItem(index: number) {
    currentIndex = index;
    if (carouselContainer) {
      const itemWidth = carouselContainer.querySelector('.carousel-item')?.clientWidth || 0;
      const targetScrollLeft = index * itemWidth;
      carouselContainer.scrollTo({
        left: targetScrollLeft,
        behavior: 'smooth'
      });
    }
  }

  function handleScroll() {
    if (!carouselContainer || isDragging) return;
    const itemWidth = carouselContainer.querySelector('.carousel-item')?.clientWidth || 0;
    const newIndex = Math.round(carouselContainer.scrollLeft / itemWidth);
    if (newIndex !== currentIndex) {
      currentIndex = newIndex;
    }
  }

  // Touch/drag handlers
  function handleTouchStart(e: TouchEvent) {
    isDragging = true;
    // Use pageX directly (viewport-relative) instead of offsetLeft which is relative to offsetParent
    startX = e.touches[0].pageX;
    lastX = e.touches[0].pageX; // Initialize last position for delta calculation
    scrollLeft = carouselContainer!.scrollLeft;
    lastDragDistance = 0; // Reset drag distance
    // Disable scroll-snap during drag to prevent interference
    carouselContainer!.style.scrollSnapType = 'none';
  }

  function handleMouseDown(e: MouseEvent) {
    isDragging = true;
    // Use pageX directly (viewport-relative) instead of offsetLeft which is relative to offsetParent
    startX = e.pageX;
    lastX = e.pageX; // Initialize last position for delta calculation
    scrollLeft = carouselContainer!.scrollLeft;
    lastDragDistance = 0; // Reset drag distance
    // Disable scroll-snap during drag to prevent interference
    carouselContainer!.style.scrollSnapType = 'none';
    carouselContainer!.style.cursor = 'grabbing';
  }

  function handleTouchEnd() {
    isDragging = false;
    lastX = 0; // Reset last position
    // Re-enable scroll-snap after drag ends
    carouselContainer!.style.scrollSnapType = '';
    snapToNearestItem();
  }

  function handleMouseUp() {
    isDragging = false;
    lastX = 0; // Reset last position
    // Re-enable scroll-snap after drag ends
    carouselContainer!.style.scrollSnapType = '';
    carouselContainer!.style.cursor = 'grab';
    snapToNearestItem();
  }

  function handleTouchMove(e: TouchEvent) {
    if (!isDragging) return;
    e.preventDefault();
    const currentX = e.touches[0].pageX;
    // Calculate delta from last position for 1:1 responsive movement
    // On first move, use startX; on subsequent moves, use lastX
    const deltaX = lastX === 0 ? startX - currentX : lastX - currentX;
    // Apply delta to current scroll position for immediate, responsive movement
    const currentScrollLeft = carouselContainer!.scrollLeft;
    const newScrollLeft = currentScrollLeft + deltaX;
    lastDragDistance += deltaX; // Accumulate total drag distance for direction-based snapping
    lastX = currentX; // Update last position for next delta calculation
    carouselContainer!.scrollLeft = newScrollLeft;
  }

  function handleMouseMove(e: MouseEvent) {
    if (!isDragging) return;
    e.preventDefault();
    const currentX = e.pageX;
    // Calculate delta from last position for 1:1 responsive movement
    // On first move, use startX; on subsequent moves, use lastX
    const deltaX = lastX === 0 ? startX - currentX : lastX - currentX;
    // Apply delta to current scroll position for immediate, responsive movement
    const currentScrollLeft = carouselContainer!.scrollLeft;
    const newScrollLeft = currentScrollLeft + deltaX;
    lastDragDistance += deltaX; // Accumulate total drag distance for direction-based snapping
    lastX = currentX; // Update last position for next delta calculation
    carouselContainer!.scrollLeft = newScrollLeft;
  }

  function snapToNearestItem() {
    const itemWidth = carouselContainer!.querySelector('.carousel-item')?.clientWidth || 0;
    if (!itemWidth) return;
    
    // Determine snap direction based on drag distance
    // If drag was even slightly (>15% of item width), snap in that direction
    const dragThreshold = itemWidth * 0.15;
    let newIndex: number;
    
    if (Math.abs(lastDragDistance) > dragThreshold) {
      // Significant drag - snap in drag direction
      if (lastDragDistance > 0) {
        // Dragged left - go to next item (higher index)
        newIndex = Math.min(currentIndex + 1, items.length - 1);
      } else {
        // Dragged right - go to previous item (lower index)
        newIndex = Math.max(currentIndex - 1, 0);
      }
    } else {
      // Small drag - snap to nearest item
      newIndex = Math.round(carouselContainer!.scrollLeft / itemWidth);
      // Clamp to valid range
      newIndex = Math.max(0, Math.min(newIndex, items.length - 1));
    }
    
    goToItem(newIndex);
    // Reset drag distance
    lastDragDistance = 0;
  }
</script>

{#if variant === 'mobile'}
  <div class="spotlight-items-section mobile">
    <!-- Horizontal scrollable carousel -->
    <!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
    <div
      class="carousel-scroll-container"
      role="region"
      aria-label="Carousel of spotlight items"
      bind:this={carouselContainer}
      onscroll={handleScroll}
      ontouchstart={handleTouchStart}
      ontouchend={handleTouchEnd}
      ontouchmove={handleTouchMove}
      onmousedown={handleMouseDown}
      onmouseup={handleMouseUp}
      onmouseleave={handleMouseUp}
      onmousemove={handleMouseMove}
    >
      {#each items as item, index}
        <div class="carousel-item">
          <SpotlightItem heading={item.heading}>
            <div class="text-base">
              {@html item.content}
            </div>
          </SpotlightItem>
        </div>
      {/each}
    </div>

    <!-- Dot indicators -->
    {#if items.length > 1}
      <div class="carousel-indicators">
        {#each items as _, index}
          <button
            class="indicator-dot {index === currentIndex ? 'active' : ''}"
            onclick={() => goToItem(index)}
            aria-label="Go to item {index + 1}"
          ></button>
        {/each}
      </div>
    {/if}
  </div>
{:else}
  <div class="spotlight-items-section desktop">
    {#each items as item}
      <SpotlightItem heading={item.heading}>
        <div class="text-base">
          {@html item.content}
        </div>
      </SpotlightItem>
    {/each}
  </div>
{/if}

<style lang="scss">
@use '../styles/variables' as *;

.spotlight-items-section {
  &.desktop {
    display: none;
    @include breakpointMin('xs') {
      display: flex;
      flex-direction: column;
      gap: #{$space-sm};
      width: 100%;
    }
  }

  &.mobile {
    display: flex;
    flex-direction: column;
    gap: #{$space-md};
    width: 100%;

    @include breakpointMin('xs') {
      display: none;
    }
  }
}

.carousel-scroll-container {
  display: flex;
  overflow-x: auto;
  overflow-y: hidden;
  margin-left: 4vw;
  scroll-snap-type: x mandatory;
  scroll-behavior: smooth;
  -webkit-overflow-scrolling: touch;
  gap: #{$space-sm};
  width: 100%;
  cursor: grab;
  user-select: none;

  // Hide scrollbar but keep functionality
  scrollbar-width: none; /* Firefox */
  -ms-overflow-style: none; /* IE and Edge */

  &::-webkit-scrollbar {
    display: none; /* Chrome, Safari, Opera */
  }

  &:active {
    cursor: grabbing;
  }

  // Add padding to show peek effect
  padding-right: 20%; // Shows portion of next item
}

.carousel-item {
  flex: 0 0 89%; // Each item takes 85% of container width
  scroll-snap-align: start;
  scroll-snap-stop: always;
  height: 160px;

  // Ensure the item doesn't shrink
  min-width: 300px;
  max-width: 390px;
}

.carousel-indicators {
  display: flex;
  gap: #{$space-xs};
  justify-content: center;
  align-items: center;
  width: 100%;
  margin-top: #{$space-xs};
}

.indicator-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #{$white-40};
  border: none;
  cursor: pointer;
  padding: 0;
  transition: all 0.3s ease;

  &.active {
    background: #{$white};
    width: 10px;
    height: 10px;
  }

  &:hover {
    background: #{$white-70};
  }
}
</style>