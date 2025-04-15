<script>
  import { Alert } from "flowbite-svelte";

  let content = document.documentElement.outerHTML;
</script>

<h2>Svelte</h2>
<div class="p-8">
  <Alert>
    <span class="font-medium">Info alert!</span>
    Change a few things up and try submitting again.
  </Alert>
</div>

<p class="text-sm">{content}</p>
