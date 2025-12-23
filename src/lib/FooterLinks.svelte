<script lang="ts">
  import resumePdf from '$lib/assets/Resume-NayeliPerez-2025.pdf';

  let showCopiedToast = $state(false);
  let {variant} = $props<{variant: 'desktop' | 'mobile'}>();

  async function copyEmailToClipboard(event: MouseEvent) {
    event.preventDefault();
    const email = 'nayeliaperezt@gmail.com';

    try {
      await navigator.clipboard.writeText(email);
      showCopiedToast = true;

      // Hide toast after 2 seconds
      setTimeout(() => {
        showCopiedToast = false;
      }, 2000);
    } catch (err) {
      console.error('Failed to copy email:', err);
    }
  }
</script>
<div class={`footer-links ${variant}`}>
  <a href={resumePdf} download="Resume-NayeliPerez-2025.pdf" class="footer-link">Resume</a>
  <a href="https://www.linkedin.com/in/nayelip/" target="_blank" rel="noopener noreferrer" class="footer-link">LinkedIn</a>
  <div class="email-link-wrapper">
    <button type="button" onclick={copyEmailToClipboard} class="footer-link">Email</button>
    {#if showCopiedToast}
      <div class="copied-toast">
        <svg class="clipboard-icon" xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path>
          <rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect>
        </svg>
        <span>Copied</span>
      </div>
    {/if}
  </div>
  <a href="https://www.are.na/nayeli-perez" target="_blank" rel="noopener noreferrer" class="footer-link">Are.na</a>
</div>

<style lang="scss">
@use '../styles/variables' as *;

.footer-links {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  align-self: stretch;
  padding: 0 #{$space-sm} 0 #{$space-sm};

  &.desktop {
    @include breakpointMax('xs') {
            display: none;

    }
  }

  &.mobile {
    display: none;
    @include breakpointMax('xs') {
      display: flex;
    }
  }
}

.footer-link {
  font-family: #{$font-sans};
  font-size: 0.875rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: #{$white};
  text-decoration: none;
  transition: opacity 0.2s ease;
  background: none;
  border: none;
  padding: 0;
  cursor: pointer;

  &:hover {
    opacity: 0.7;
  }
}

.email-link-wrapper {
  position: relative;
  display: inline-flex;
  align-items: center;
}

.copied-toast {
  position: absolute;
  left: calc(100% + #{$space-md});
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  align-items: center;
  gap: 4px;
  padding: 4px 8px;
  background: #{$white-15};
  border-radius: 2px;
  font-family: #{$font-sans};
  font-size: 0.75rem;
  font-weight: 400;
  color: #{$white};
  white-space: nowrap;
  animation: toastFadeInDesktop 0.2s ease-out;

  @include breakpointMax('xs') {
    left: 50%;
    top: calc(100% + #{$space-md});
    transform: translateX(-50%);
    animation: toastFadeInMobile 0.2s ease-out;
  }
}

.clipboard-icon {
  width: 12px;
  height: 12px;
  color: #{$white};
}

@keyframes toastFadeInDesktop {
  from {
    opacity: 0;
    transform: translateY(-50%) scale(0.95);
  }
  to {
    opacity: 1;
    transform: translateY(-50%) scale(1);
  }
}

@keyframes toastFadeInMobile {
  from {
    opacity: 0;
    transform: translateX(-50%) scale(0.95);
  }
  to {
    opacity: 1;
    transform: translateX(-50%) scale(1);
  }
}

</style>
