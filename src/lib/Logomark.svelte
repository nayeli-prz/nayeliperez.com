<script context="module" lang="ts">
  // Export the type from the module script to avoid Svelte compiler errors in some setups
  export type LogomarkType = 'IconOnly35' | 'Vertical-Sm' | 'Vertical-Lg' | 'Horizontal';
  
</script>

<script lang="ts">
    import LogomarkIcon from '$lib/LogomarkIcon.svelte';
    export let type: 'Horizontal' | 'Vertical-Sm' | 'Vertical-Lg' | 'IconOnly35' = 'Horizontal';
    let className: string = '';

    //Enable setting mobile or desktop class based on layout via class
    export { className as class };
</script>

{#if type === 'Vertical-Sm'}
		<div class="logomark vertical-sm {className}" role="img" aria-label="Nayeli Pérez logo">
	    <div class="icon" aria-hidden="true">
	      <div class="rays">
	        <LogomarkIcon />
	      </div>
	    </div>
	    <div class="name name--vertical">Nayeli Pérez</div>
	  </div>
    {:else if type === 'Vertical-Lg'}
			 <div class="logomark vertical-lg {className}" role="img" aria-label="Nayeli Pérez logo">
	    <div class="icon icon--vertical-lg" aria-hidden="true">
	      <div class="rays">
	        <LogomarkIcon />
	      </div>
	    </div>
	    <div class="name name--vertical-lg">Nayeli Pérez</div>
	  </div>
	 {:else if type === 'IconOnly35'}
			 <div class="logomark icononly {className}" role="img" aria-label="Nayeli Pérez logo">
		    <div class="icon" aria-hidden="true">
		      <div class="rays">
		        <LogomarkIcon />
		      </div>
		    </div>
		  </div>
	{:else}
  <!-- Default is horizontal -->
		 <div class="logomark horizontal {className}" role="img" aria-label="Nayeli Pérez logo">
	    <div class="icon" aria-hidden="true">
	      <div class="rays">
	        <LogomarkIcon />
	      </div>
	    </div>

	    <div class="name">Nayeli Pérez</div>
	  </div>
  {/if}


<style lang="scss">
  @use '../styles/variables' as *;
/* Scoped styles translated from the exported design. Sizes and line-heights match the Figma export. */
.logomark {
  display: flex;
  align-items: center;
  color: #fff;
  font-family: $font-serif;

  .icon {
    position: relative;
    overflow: hidden;
    border-radius: 95px;
    background: transparent;
    width: 35px;
    height: 35px;
    &.icon--vertical-lg {
      width: 55px;
      height: 55px;
    }

    .rays {
      position: absolute;
      inset: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      pointer-events: none;

      :global(svg) {
        display: block;
        width: 100%;
        height: 100%;
      }
    }
  }

  .name {
    margin-left: 4px;
    text-transform: uppercase;
    color: #fff;
    letter-spacing: 0.035rem;
    &.name--vertical { 
        margin-left: 0; 
        text-align: center; 
        font-size: 14px; 
        line-height: 1rem;
        font-weight: 500; 
        width: 55px; 
    }
    &.name--vertical-lg { 
        margin-left: 0; 
        width: 110px; 
    }
  }

  &.vertical-sm {
    flex-direction: column;
    gap: 8px;
    .name { font-size: 14px; font-weight: 500; }
  }

  &.vertical-lg {
    flex-direction: column;
    gap: 6px;
    .name { 
        font-size: 1.25rem; 
        line-height: 1.6rem; 
        font-weight: 400; 
        text-align: center; 
      }
  }

  &.horizontal {
    flex-direction: row;
    gap: 6px;
    .name { font-size: 24px; line-height: 20px; font-weight: 400; }
  }

  &.icononly {
    justify-content: center;
    .icon { width: 35px; height: 35px; }
  }
}

.logomark-desktop {
  display: none;
  @include breakpointMin('xs') {
    display: flex;
  }
}
.logomark-mobile {
  display: flex;
  padding-bottom: #{$space-sm};
  @include breakpointMin('xs') {
    display: none;
  }
}

</style>
