<script>
  // https://github.com/tauri-apps/plugins-workspace/blob/v2/plugins/sql/guest-js/index.ts

  import Database from "@tauri-apps/plugin-sql";
  import {
    Button,
    Card,
    Table,
    TableBody,
    TableBodyCell,
    TableBodyRow,
    TableHead,
    TableHeadCell,
    FloatingLabelInput,
  } from "flowbite-svelte";

  async function handleQuery() {
    const db = await Database.load("sqlite:test.db");
    const records = await db.select("SELECT * FROM users");
    await db.close();
    return records;
  }

  let name = $state("");
  let age = $state("");
  let promise = $state(handleQuery());

  async function handleSubmit() {
    const db = await Database.load("sqlite:test.db");
    await db.execute("INSERT INTO users (name, age) VALUES ($1, $2)", [
      name,
      age,
    ]);
    name = "";
    age = "";
    promise = db.select("SELECT * FROM users");
    await db.close();
  }
</script>

<div class="flex flex-col justify-center items-center pt-[1vh]">
  <Card>
    <form class="flex flex-col space-y-4" onsubmit={handleSubmit}>
      <h3 class="text-lg font-medium text-gray-900 dark:text-white">用户</h3>
      <FloatingLabelInput style="outlined" size="small" bind:value={name}
        >姓名</FloatingLabelInput
      >
      <FloatingLabelInput
        style="outlined"
        size="small"
        bind:value={age}
        type="number"
        min="0">年龄</FloatingLabelInput
      >
      <Button type="submit">插入</Button>
    </form>
  </Card>

  {#await promise then items}
    <br />
    <Table noborder striped {items}>
      <caption
        class="p-5 text-lg font-semibold text-left text-gray-900 bg-white dark:text-white dark:bg-gray-800"
      >
        数据库
        <p class="mt-1 text-sm font-normal text-gray-500 dark:text-gray-400">
          users表
        </p>
      </caption>
      <TableHead>
        <TableHeadCell>ID</TableHeadCell>
        <TableHeadCell>Name</TableHeadCell>
        <TableHeadCell>Age</TableHeadCell>
      </TableHead>
      <TableBody tableBodyClass="divide-y">
        <TableBodyRow slot="row" let:item>
          <TableBodyCell>{item.id}</TableBodyCell>
          <TableBodyCell>{item.name}</TableBodyCell>
          <TableBodyCell>{item.age}</TableBodyCell>
        </TableBodyRow>
      </TableBody>
    </Table>
  {/await}
</div>
