<script>
  import { ask, confirm, message, open, save } from "@tauri-apps/plugin-dialog";

  import { Button, Dropdown, DropdownItem } from "flowbite-svelte";
  import { ChevronDownOutline } from "flowbite-svelte-icons";

  export async function askDialog() {
    const answer = await ask("根据点击的按钮返回 true / false.", {
      title: "提示",
      kind: "info", // kind: "error" | "warning" | "info"
    });
    alert("您选择了" + answer);
  }

  export async function confirmDialog() {
    const result = await confirm("你确定要删除吗？", {
      title: "警告",
      kind: "warning",
    });
    alert("您选择了" + result);
  }

  export async function messageDialog() {
    await message("操作失败", { title: "错误", kind: "error" });
  }

  export async function openDialog() {
    const file = await open({
      multiple: false,
      directory: false,
    });
    alert("您选择了" + file);
  }

  export async function saveDialog() {
    const path = await save({
      filters: [
        {
          name: "图片",
          extensions: ["png", "jpeg"],
        },
      ],
    });
    alert("您选择了" + path);
  }
</script>

<div class="flex flex-col justify-center items-center pt-[10vh]">
  <Button>系统弹窗<ChevronDownOutline /></Button>
  <Dropdown>
    <DropdownItem on:click={askDialog}>ask弹窗</DropdownItem>
    <DropdownItem on:click={confirmDialog}>confirm弹窗</DropdownItem>
    <DropdownItem on:click={messageDialog}>message弹窗</DropdownItem>
    <DropdownItem on:click={openDialog}>open弹窗</DropdownItem>
    <DropdownItem on:click={saveDialog}>save弹窗</DropdownItem>
  </Dropdown>
</div>
