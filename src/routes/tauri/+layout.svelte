<script>
  import {
    Navbar,
    NavBrand,
    NavLi,
    NavUl,
    NavHamburger,
  } from "flowbite-svelte";

  let { children } = $props();
  import { page } from "$app/state";
</script>

<!-- {#if page.url.pathname.startsWith("/chart")}
  {@render children()}
{:else} -->
<div class="h-screen flex flex-col">
  <Navbar>
    <NavBrand href="/tauri">
      <img src="/tauri.svg" class="me-3 h-6 sm:h-9" alt="Tauri Logo" />
      <span
        class="self-center whitespace-nowrap text-xl font-semibold dark:text-white"
        >Tauri</span
      >
    </NavBrand>
    <NavHamburger />
    <NavUl activeUrl={page.url.pathname}>
      <NavLi href="/tauri/http">HTTP客户端</NavLi>
      <NavLi href="/tauri/sql">SQL</NavLi>
      <NavLi href="/tauri/store">Store</NavLi>
      <NavLi href="/tauri/dialog">Dialog</NavLi>
      <NavLi href="/tauri/os">操作系统信息</NavLi>
    </NavUl>
  </Navbar>

  <div class="bg-lightgray flex-1 p-4">
    {@render children()}
  </div>
</div>
<!-- {/if} -->
