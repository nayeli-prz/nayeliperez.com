<script lang="ts">
  import { Logomark } from '$lib';
</script>


<div class="wrapper type-system-page">
    <nav style="margin-bottom: 48px;">
        <a href="/">← Back</a>
    </nav>

    <h1>Design System Preview</h1>

    <div style="margin-top: 48px;">
        <h1>Heading 1: The quick brown fox jumps over the lazy dog</h1>
    </div>

    <div style="margin-top: 48px;">
        <h2>Heading 2: The quick brown fox jumps over the lazy dog</h2>
    </div>

    <div style="margin-top: 48px;">
        <h3>Heading 3: The quick brown fox jumps over the lazy dog</h3>
    </div>

    <div style="margin-top: 48px;">
        <h4>Heading 4: The quick brown fox jumps over the lazy dog</h4>
    </div>

    <div style="margin-top: 48px;">
        <h5>Heading 5: The quick brown fox jumps over the lazy dog</h5>
    </div>

    <div style="margin-top: 48px;">
        <h6>Heading 6: The quick brown fox jumps over the lazy dog</h6>
    </div>

    <div style="margin-top: 48px;">
        <p class="text-lg">Text Large: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
    </div>

    <div style="margin-top: 48px;">
        <p class="text-base">Text Base: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
    </div>

    <div style="margin-top: 48px;">
        <p class="text-base-500">Text Base 500: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
    </div>

    <div style="margin-top: 48px;">
        <p class="text-base-700">Text Base 700: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
    </div>

    <div style="margin-top: 48px;">
        <p class="text-sm">Text Small: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
    </div>

    <div style="margin-top: 48px;">
        <p class="text-sm-500">Text Small 500: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
    </div>

    <div style="margin-top: 48px;">
        <p class="text-sm-700">Text Small 700: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
    </div>
<!-- --- -->

<h2>Logomark preview</h2>

  <section style="align-items: start; display: flex; flex-direction: column; gap: 6px;">
    <h6>IconOnly35</h6>
    <div class="preview">
      <Logomark type="IconOnly35" />
    </div>
  </section>

  <section style="align-items: start; display: flex; flex-direction: column; gap: 6px;">
    <h6>Vertical</h6>
    <div class="preview">
      <Logomark type="Vertical" />
    </div>
  </section>

  <section style="align-items: start; display: flex; flex-direction: column; gap: 6px;">
    <h6>Horizontal (default)</h6>
    <div class="preview">
      <Logomark type="Horizontal" />
    </div>
  </section>
<!-- --- -->

</div>
