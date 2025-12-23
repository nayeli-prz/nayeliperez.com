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
@use '../styles/variables' as *;


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
      // @include breakpointMax('sm') {
      //   align-items: center;
      // }
      // @include breakpointMin('sm') {
      //   align-items: flex-start;
      // }
}

</style>
