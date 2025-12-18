<script lang="ts">
  import { Logomark, GradientBar, ContentSection, FooterLinks } from '$lib';
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
        
          <GradientBar onThemeChange={setTheme} />
          <div class="wrapper-flex-col gap-lg">
            
            <div class="wrapper-flex-col gap-sm">
              <Logomark />
              <p class="text-base">Impact-focused designer, builder, product strategist, and systems-thinker, with 8+ years of experience designing complex platform products. Based in San Antonio, TX</p>
              <p class="text-base">Pondering: A future where evolving systems, platforms, and paradigms enable individual decisions and behaviors that contribute to the common good.</p>
              <!-- <p class="text-base">Pondering individual decision-making, collective action, and the tensions that exist between these. Passionate about designing a future (via new systems, platforms, and paradigms) that enable individual behaviors that support the collective good.</p> -->
            </div>
            
            <div class="wrapper-flex-col gap-sm">
              <ContentSection heading="">
                <div class="text-base">Currently offering product design, UX, research, design systems services and beyond. Let’s chat!
                </div>
              </ContentSection>
              <ContentSection heading="Coming Soon">
                <div class="text-base">
                Building <span class="text-base-500">San Antonio's Circular Directory</span> in partnership with <a href="https://www.circularsanantonio.org" target="blank">Circular San Antonio</a>
                </div>
              </ContentSection>
              
            </div>
            
            <FooterLinks variant="desktop" />

          </div>
          <div class="wrapper-flex-col gap-md">
              <FooterLinks variant="mobile" />
              <div class="empty-rectangle"></div>
          </div>
         
    </div>
</div>


<style lang="scss">
@import '../styles/variables';

.wrapper {
  min-height: 100vh;
  display: grid;
  grid-template-columns: repeat($grid-columns, 1fr);
  gap: $grid-gutter;
  padding-left: $grid-margin-offset;
  padding-right: $grid-margin-offset;
  align-items: center;
  width: 100%;
  box-sizing: border-box;

}


.home-page-content {
  opacity: 0;
  transform: translateY(12px);
  will-change: opacity, transform;
  animation: fadeUp 420ms cubic-bezier(.22,.9,.1,1) 160ms both;

  // Mobile is default: span full width, center aligned
  grid-column: 1 / -1;

  @media (max-width: 550px) {
    align-items: center;
    text-align: center;

    // Spacious layout when viewport height is sufficient (> content height + 50px)
    // Using container query approach with min-height
    @media (min-height: 600px) {
      height: 100%;
      // gap: #{$space-120}; // Override gap-lg for more vertical spacing
      justify-content: space-between;
      padding-top: #{$space-md};
      padding-bottom: #{$space-lg};
    }
  }

  @include breakpoint('sm') {
    grid-column: 2 / 10; // columns 2-9 (8 columns total, centered)
    align-items: flex-start;
    text-align: left;
  }

  @include breakpoint('lg') {
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

.empty-rectangle {
  width: 100%;
  height: 0.5rem;
  border-radius: 0.25rem;
  border: 1px solid #{$white-70};
  background: transparent;
}

</style>