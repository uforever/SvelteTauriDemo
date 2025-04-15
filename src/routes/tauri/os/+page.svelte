<script>
  import { platform, version, arch, locale } from "@tauri-apps/plugin-os";
  import { Listgroup, Spinner } from "flowbite-svelte";

  async function osInfo() {
    const currentArch = arch();
    const currentPlatform = platform();
    const currentVersion = version();
    const currentLocale = await locale();
    // return `${currentArch} ${currentPlatform} ${currentVersion} ${currentLocale}`;
    return [
      `平台: ${currentPlatform}`,
      `架构: ${currentArch}`,
      `版本: ${currentVersion}`,
      `语言: ${currentLocale}`,
    ];
  }
</script>

<main
  class="flex flex-col justify-center items-center pt-[10vh]"
>
  <h2 class="text-center text-xl font-semibold text-gray-900 dark:text-white">
    操作系统信息
  </h2>
  <br />

  {#await osInfo()}
    <Spinner />
  {:then osInfo}
    <Listgroup items={osInfo} let:item class="w-48">
      {item}
    </Listgroup>
  {/await}
</main>
