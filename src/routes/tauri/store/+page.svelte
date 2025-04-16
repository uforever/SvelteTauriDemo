<script>
  import { LazyStore } from "@tauri-apps/plugin-store";
  import {
    A,
    CloseButton,
    Table,
    TableBody,
    TableBodyCell,
    TableBodyRow,
    TableHead,
    TableHeadCell,
    FloatingLabelInput,
  } from "flowbite-svelte";

  const store = new LazyStore("demo.json");
  let promise = $state(store.entries());

  let key = $state("");
  let value = $state("");

  async function handleInsert() {
    await store.set(key, value);
    promise = store.entries();
  }

  async function handleDelete(key) {
    await store.delete(key);
    promise = store.entries();
  }
</script>

{#await promise then items}
  <Table shadow {items}>
    <caption
      class="p-5 text-lg font-semibold text-left text-gray-900 bg-white dark:text-white dark:bg-gray-800"
    >
      持久化的键值存储
    </caption>
    <TableHead>
      <TableHeadCell>Key</TableHeadCell>
      <TableHeadCell>Value</TableHeadCell>
      <TableHeadCell>
        <span class="sr-only">操作</span>
      </TableHeadCell>
    </TableHead>
    <TableBody tableBodyClass="divide-y">
      <TableBodyRow>
        <TableBodyCell>
          <FloatingLabelInput size="small" bind:value={key}>
            键
          </FloatingLabelInput>
        </TableBodyCell>
        <TableBodyCell>
          <FloatingLabelInput size="small" bind:value>值</FloatingLabelInput>
        </TableBodyCell>
        <TableBodyCell>
          <A onclick={handleInsert}>插入</A>
        </TableBodyCell>
      </TableBodyRow>
      <TableBodyRow slot="row" let:item>
        <TableBodyCell>{item[0]}</TableBodyCell>
        <TableBodyCell>{item[1]}</TableBodyCell>
        <TableBodyCell>
          <CloseButton on:click={handleDelete(item[0])} />
        </TableBodyCell>
      </TableBodyRow>
    </TableBody>
  </Table>
{/await}
