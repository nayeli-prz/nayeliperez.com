<script lang="ts">
  interface Props {
    heading?: string | undefined;
    children: any;
  }

  let { heading, children }: Props = $props();
</script>

<section class="spotlight-item">
  <h6>{heading}</h6>
  <div>
    {@render children()}
  </div>
</section>

<style lang="scss">
@import '../styles/variables';

.spotlight-item {
  background: #{$white-6};
  // width: 100%;
  display: flex;
  padding: #{$space-md};
  flex-direction: column;
  align-items: flex-start;
  gap: #{$space-xs};
  align-self: stretch;
  color: #{$white};
  border-radius: 6px;
  flex-wrap: nowrap;
  height: 100%;
  justify-content: center;

  // Mobile: center align items when inside centered content
  @media (max-width: 550px) {
      align-items: center;
  }
}

</style>
