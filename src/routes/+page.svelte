<script lang="ts">
  import { Logomark, GradientBar, SpotlightItemsSection, FooterLinks } from '$lib';
  import { onMount } from 'svelte';

  let currentTheme = $state('1');

  function setTheme(theme: string) {
    currentTheme = theme;
    if (typeof document !== 'undefined') {
      document.documentElement.setAttribute('data-theme', theme);
      console.log('Theme set to:', theme);
      console.log('HTML element data-theme:', document.documentElement.getAttribute('data-theme'));
    }
  }

  onMount(() => {
    // Set initial theme
    document.documentElement.setAttribute('data-theme', currentTheme);
    console.log('Initial theme set to:', currentTheme);
  });
</script>

<div class="wrapper">
    <div class="home-page-content wrapper-flex-col gap-lg">
        
          <!-- Add wrapper for gradient bar + footer links in mobile -->
          <div class="wrapper-flex-col gap-lg"> 
            <GradientBar onThemeChange={setTheme} />
            <FooterLinks variant="mobile" />
          </div>
          
          <div class="wrapper-flex-col gap-lg">
            
            <div class="wrapper-flex-col gap-sm">
              <Logomark type="Vertical-Lg" class="logomark-mobile" />
              <Logomark type="Horizontal" class="logomark-desktop" />
              <p class="text-base">Impact-focused designer, builder, product strategist, and systems-thinker, with 8+ years of experience designing complex platform products. Based in San Antonio, TX</p>
              <p class="text-base paragraph-2">Pondering: A future where evolving systems, platforms, and paradigms enable individual decisions and behaviors that contribute to the common good.</p>
              <!-- <p class="text-base">Pondering individual decision-making, collective action, and the tensions that exist between these. Passionate about designing a future (via new systems, platforms, and paradigms) that enable individual behaviors that support the collective good.</p> -->
            </div>
            <SpotlightItemsSection variant="desktop" />
            <FooterLinks variant="desktop" />

          </div>
          
          <!-- Add wrapper for bar + footer links in mobile // currently not using -->
          <div class="wrapper-flex-col gap-md empty-bar-wrapper">
              <SpotlightItemsSection variant="mobile" />
              <div class="empty-bar"></div>
          </div>
         
    </div>
</div>


<style lang="scss">
@import '../styles/variables';

.wrapper {
  min-height: 100vh;
  min-height: 100dvh; // Dynamic viewport height - accounts for mobile browser UI
  display: grid;
  grid-template-columns: repeat($grid-columns, 1fr);
  gap: $grid-gutter;
  padding-left: $grid-margin-offset;
  padding-right: $grid-margin-offset;
  padding-bottom: #{$space-lg}; // Extra padding at bottom for mobile browsers
  align-items: center;
  width: 100%;
  box-sizing: border-box;
  @include breakpointMax('xs') {
    align-items: start;
    height: 96dvh;
  }

}

.paragraph-2 {
  display: none;
  @include breakpointMin('sm') {
    display: flex;
  }
}




.home-page-content {
  opacity: 0;
  transform: translateY(12px);
  will-change: opacity, transform;
  animation: fadeUp 420ms cubic-bezier(.22,.9,.1,1) 160ms both;

  // Mobile is default: span full width, center aligned
  grid-column: 1 / -1;

  @include breakpointMax('xs') {
    // Spacious layout when viewport height is sufficient (> 500px)
    align-items: center;
    text-align: center;
    margin-top: #{$space-xl};
    height: 96%;
    
    @media (min-height: 500px) {
      justify-content: space-between;
      padding-top: #{$space-md};
      padding-bottom: #{$space-lg};
    }
  }

  @include breakpointMin('sm') {
    grid-column: 2 / 10; // columns 2-9 (8 columns total, centered)
    align-items: flex-start;
    text-align: left;
    // height: 100%;
  }

  @include breakpointMin('lg') {
    // Span 4 columns in the center of the 10-column grid
    grid-column: 4 / 8; // columns 4-7 (4 columns total, centered)
  }
}

.home-page-content > * {
  animation: fadeUp 420ms cubic-bezier(.22,.9,.1,1) both;
}

.home-page-content > *:nth-child(1) { animation-delay: 120ms; }
.home-page-content > *:nth-child(2) { animation-delay: 240ms; }
.home-page-content > *:nth-child(3) { animation-delay: 360ms; }
.home-page-content > *:nth-child(4) { animation-delay: 480ms; }
.home-page-content > *:nth-child(5) { animation-delay: 600ms; }

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(12px); }
  to { opacity: 1; transform: translateY(0); }
}

@media (prefers-reduced-motion: reduce) {
  .home-page-content,
  .home-page-content > * {
    animation: none !important;
    opacity: 1;
    transform: none;
  }
}

.empty-bar {
  width: 100%;
  height: 0.5rem;
  border-radius: 0.25rem;
  border: 1px solid #{$white-70};
  background: transparent;
  display: flex;
  @include breakpointMax('xs') {
    display: none;
  }
}

// .empty-bar-wrapper {
//   display: none;
//   @include breakpointMin('sm') {
//   display: flex;
//   }
// }

</style>