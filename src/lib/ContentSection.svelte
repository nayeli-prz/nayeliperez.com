<script lang="ts">
  interface Props {
    heading: string;
    children: any;
  }

  let { heading, children }: Props = $props();
</script>

<section class="content-section">
  <h6>{heading}</h6>
  <div>
    {@render children()}
  </div>
</section>

<style lang="scss">
@import '../styles/variables';

.content-section {
  background: #{$white-6};
  // width: 100%;
  display: flex;
  padding: #{$space-md};
  flex-direction: column;
  align-items: flex-start;
  gap: #{$space-sm};
  align-self: stretch;
  color: #{$white};
  border-radius: 2px;
  
  // Mobile: center align items when inside centered content
  @media (max-width: 550px) {
      align-items: center;
  }
}

</style>
