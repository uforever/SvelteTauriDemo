<script>
  import { fetch } from "@tauri-apps/plugin-http";

  import {
    Button,
    FloatingLabelInput,
    Input,
    Label,
    Listgroup,
    Hr,
    Spinner,
  } from "flowbite-svelte";

  let input = $state("");
  let url = $state("https://echo.hoppscotch.io");

  let status = $state(0);
  let statusText = $state("");
  let output = $state("");
  let complete = $state(false);
  let start = $state(false);

  function truncateString(str) {
    if (!str) {
      return "";
    }
    if (str.length > 55) {
      return str.slice(0, 55) + "...";
    } else {
      return str;
    }
  }

  async function handleSubmit(event) {
    event.preventDefault();
    start = true;
    complete = false;
    fetch(url, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({ data: input }),
    })
      .then((response) => {
        status = response.status;
        statusText = response.statusText;
        return response.json();
      })
      .then((data) => {
        output = truncateString(JSON.stringify(data));
        complete = true;
      })
      .catch((e) => alert(`Error: ${e}`));
  }

  let list = $derived([
    `状态码: ${status}`,
    `状态文本: ${statusText}`,
    `响应数据: ${output}`,
  ]);
</script>

<form onsubmit={handleSubmit}>
  <div class="mb-6">
    <Label class="mb-2">URL</Label>
    <Input class="mb-6" disabled bind:value={url} type="text" />
  </div>
  <div class="mb-6">
    <FloatingLabelInput style="outlined" bind:value={input} type="text">
      数据
    </FloatingLabelInput>
  </div>
  <div class="flex justify-center">
    <Button type="submit">发送请求</Button>
  </div>
</form>

{#if start}
  {#if complete}
    <Hr classHr="my-8 w-64">响应</Hr>
    <div class="flex flex-col justify-center items-center">
      <Listgroup items={list} let:item class="w-48">
        {item}
      </Listgroup>
    </div>
  {:else}
    <Hr classHr="my-8 w-64">响应</Hr>
    <div class="flex flex-col justify-center items-center">
      <Spinner />
    </div>
  {/if}
{/if}
