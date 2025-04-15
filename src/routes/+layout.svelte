<script>
  let { children } = $props();
  import "/src/app.css";
</script>

{@render children()}


<style lang="postcss">
  @reference "tailwindcss";
  :global(html) {
    background-color: theme(--color-gray-100);
  }
</style>