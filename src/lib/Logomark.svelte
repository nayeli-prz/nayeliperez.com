<script context="module" lang="ts">
  // Export the type from the module script to avoid Svelte compiler errors in some setups
  export type LogomarkType = 'IconOnly35' | 'Vertical' | 'Horizontal';
  
</script>

<script lang="ts">
    import LogomarkIcon from '$lib/LogomarkIcon.svelte';
    export let type: 'Horizontal' | 'Vertical' | 'IconOnly35' = 'Horizontal';
</script>

{#if type === 'Vertical'}
		<div class="logomark vertical" role="img" aria-label="Nayeli Pérez logo">
	    <div class="icon" aria-hidden="true">
	      <div class="rays">
	        <LogomarkIcon />
	      </div>
	    </div>

	    <div class="name name--vertical">Nayeli Pérez</div>
	  </div>
	 {:else if type === 'IconOnly35'}
			 <div class="logomark icononly" role="img" aria-label="Nayeli Pérez logo">
		    <div class="icon" aria-hidden="true">
		      <div class="rays">
		        <LogomarkIcon />
		      </div>
		    </div>
		  </div>
	{:else}
		 <div class="logomark horizontal" role="img" aria-label="Nayeli Pérez logo">
	    <div class="icon" aria-hidden="true">
	      <div class="rays">
	        <LogomarkIcon />
	      </div>
	    </div>

	    <div class="name">Nayeli Pérez</div>
	  </div>
  {/if}


<style lang="scss">
/* Scoped styles translated from the exported design. Sizes and line-heights match the Figma export. */
.logomark {
  display: flex;
  align-items: center;
  color: #fff;
  font-family: 'STIX Two Text', Georgia, serif; /* explicit font stack from project variables */

  .icon {
    position: relative;
    overflow: hidden;
    border-radius: 95px;
    background: transparent;
    width: 35px;
    height: 35px;

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
    &.name--vertical { 
        margin-left: 0; 
        text-align: center; 
        font-size: 14px; 
        line-height: 0.9rem;
        font-weight: 500; 
        width: 55px; 
    }
  }

  &.vertical {
    flex-direction: column;
    gap: 8px;
    .name { font-size: 14px; font-weight: 500; }
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
</style>
