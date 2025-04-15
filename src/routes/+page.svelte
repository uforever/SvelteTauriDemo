<script>
  import { invoke } from "@tauri-apps/api/core";

  // let name = $state("");
  // let greetMsg = $state("");

  // async function greet(event) {
  //   event.preventDefault();
  //   // Learn more about Tauri commands at https://tauri.app/develop/calling-rust/
  //   greetMsg = await invoke("greet", { name });
  // }
</script>

<main class="flex flex-col justify-center items-center pt-[10vh] bg-gray-50 dark:bg-gray-900">
  <h1 class="text-center text-3xl font-semibold text-gray-900 dark:text-white">Tauri + Svelte</h1>

  <div class="flex justify-center space-x-6 mt-6">
    <a href="/tauri">
      <img src="/tauri.svg" class="h-24 p-6 transition-all duration-300 ease-in-out hover:drop-shadow-[0_0_2em_#24c8db]" alt="Tauri Logo" />
    </a>
    <a href="/svelte">
      <img src="/svelte.svg" class="h-24 p-6 transition-all duration-300 ease-in-out hover:drop-shadow-[0_0_2em_#ff3e00]" alt="SvelteKit Logo" />
    </a>
  </div>

  <p>点击logo查看更多</p>
</main>
