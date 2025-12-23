<script lang="ts">
  interface Props {
    onThemeChange?: (theme: string) => void;
  }

  let { onThemeChange }: Props = $props();

  let isHovering = $state(false);
  let barElement: SVGRectElement;
  let cursorX = $state(0);

  function getThemeAtPosition(percentage: number): string {
    // Map position to theme number based on gradient sections
    if (percentage <= 0.17) return '1';      // Green
    if (percentage <= 0.4) return '2';      // Purple
    if (percentage <= 0.60) return '3';      // Yellow
    if (percentage <= 0.82) return '4';      // Orange
    return '5';                              // Black
  }

  function handleMouseEnter() {
    isHovering = true;
  }

  function handleMouseLeave() {
    isHovering = false;
  }

  function handleMouseMove(e: MouseEvent) {
    if (!barElement) return;
    const rect = barElement.getBoundingClientRect();
    cursorX = e.clientX - rect.left;
  }

  function handleClick(e: MouseEvent) {
    if (!barElement) return;
    const rect = barElement.getBoundingClientRect();
    const clickX = e.clientX - rect.left;
    const percentage = clickX / rect.width;
    const theme = getThemeAtPosition(percentage);

    if (onThemeChange) {
      onThemeChange(theme);
    }
  }

  function handleKeyDown(e: KeyboardEvent) {
    if (e.key === 'Enter' || e.key === ' ') {
      e.preventDefault();
      // For keyboard, default to middle of bar (yellow/theme 3)
      if (onThemeChange) {
        onThemeChange('3');
      }
    }
  }
</script>

<div class="gradient-bar-wrapper">
  {#if isHovering}
    <div class="hover-label" style="left: {cursorX}px;">
      PICK
    </div>
  {/if}
  <svg class="gradient-bar-svg" width="100%" height="11">
    <defs>
      <linearGradient id="barGradient">
        <stop offset="0%" class="stop-green" />
        <stop offset="7%" class="stop-green" />
        <stop offset="15%" class="stop-green" />

        <stop offset="21%" class="stop-purple" />
        <stop offset="28%" class="stop-purple" />
        <stop offset="36%" class="stop-purple" />

        <stop offset="43%" class="stop-yellow" />
        <!-- <stop offset="48%" class="stop-yellow" /> -->
        <stop offset="58%" class="stop-yellow" />

        <stop offset="65%" class="stop-orange" />
        <!-- <stop offset="68%" class="stop-orange" /> -->
        <stop offset="80%" class="stop-orange" />

        <stop offset="87%" class="stop-black" />
        <!-- <stop offset="88%" class="stop-black" /> -->
        <stop offset="100%" class="stop-black" />
      </linearGradient>

      <linearGradient id="strokeGradient" x1="0%" y1="0%" x2="100%" y2="0%">
        <stop offset="0%" stop-color="rgba(255, 255, 255, 0.7)" stop-opacity="0.7" />
        <stop offset="40%" stop-color="rgba(255, 255, 255, 0.7)" stop-opacity="0.7" />
        <stop offset="50%" stop-color="rgba(255, 255, 255, 1)" stop-opacity="1" />
        <stop offset="60%" stop-color="rgba(255, 255, 255, 0.7)" stop-opacity="0.7" />
        <stop offset="100%" stop-color="rgba(255, 255, 255, 0.7)" stop-opacity="0.7" />
        {#if !isHovering}
          <animate
            attributeName="x1"
            values="-100%;200%"
            dur="2s"
            repeatCount="indefinite"
          />
          <animate
            attributeName="x2"
            values="0%;300%"
            dur="2s"
            repeatCount="indefinite"
          />
        {/if}
      </linearGradient>
    </defs>

    <rect
      x="0"
      y="0"
      width="100%"
      height="11"
      rx="5"
      fill="url(#barGradient)"
      stroke="url(#strokeGradient)"
      stroke-width="1.5"
      class="bar-rect"
      class:hovering={isHovering}
      bind:this={barElement}
      onmouseenter={handleMouseEnter}
      onmouseleave={handleMouseLeave}
      onmousemove={handleMouseMove}
      onclick={handleClick}
      onkeydown={handleKeyDown}
      role="slider"
      tabindex="0"
      aria-label="Theme selector"
      aria-valuenow="1"
      aria-valuemin="1"
      aria-valuemax="5"
    />
  </svg>
</div>

<style lang="scss">
@use '../styles/variables' as *;

.gradient-bar-wrapper {
  position: relative;
  width: 100%;
  display: flex;
  align-items: center;
}

.hover-label {
  position: absolute;
  top: -34px;
  transform: translateX(-50%);
  transition: top 0.2s ease;
  font-family: #{$font-sans};
  font-size: 1.1rem;
  font-weight: 300;
  letter-spacing: .05rem;
  text-transform: uppercase;
  color: #{$white-50};
  white-space: nowrap;
  pointer-events: none;
  user-select: none;
  @include breakpointMax('sm') {
      top: 24px;
      display: none;
  }
}

.gradient-bar-svg {
  width: 100%;
  height: 8px;
  cursor: pointer;
  filter: drop-shadow(0 1px 8px rgba(0, 0, 0, 0.1));
  transition: all 0.3s cubic-bezier(0.22, 0.9, 0.1, 1);
  overflow: visible;

  :global(.stop-green) {
    stop-color: #{$green-base};
  }

  :global(.stop-purple) {
    stop-color: #{$purple-bright};
  }

  :global(.stop-yellow) {
    stop-color: #{$yellow-bright};
  }

  :global(.stop-orange) {
    stop-color: #{$orange-bright};
  }

  :global(.stop-black) {
    stop-color: #{$black-base};
  }
}

.bar-rect {
  transition: all 0.8s cubic-bezier(0.22, 0.9, 0.1, 1);
  transform-origin: center;

  &.hovering {
    filter: drop-shadow(0 2px 12px rgba(0, 0, 0, 0.15));
    transform: scaleX(1.005) scaleY(1.2);
  }

  &:focus {
    outline: none;
  }
}
</style>