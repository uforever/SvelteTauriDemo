<script>
  import { Card } from 'flowbite-svelte';
</script>

<!-- <div class="flex flex-col md:flex-row md:space-x-4 space-y-4"> -->
<div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-4">
  <Card href="/tauri/http">
    <h5 class="mb-2 text-lg font-bold tracking-tight text-gray-900 dark:text-white">HTTP客户端</h5>
    <p class="font-normal text-gray-700 dark:text-gray-400 leading-tight">发起 HTTP 请求</p>
  </Card>
  
  <Card href="/tauri/sql">
    <h5 class="mb-2 text-lg font-bold tracking-tight text-gray-900 dark:text-white">SQL</h5>
    <p class="font-normal text-gray-700 dark:text-gray-400 leading-tight">数据库通信接口</p>
  </Card>

  <Card href="/tauri/store">
    <h5 class="mb-2 text-lg font-bold tracking-tight text-gray-900 dark:text-white">Store</h5>
    <p class="font-normal text-gray-700 dark:text-gray-400 leading-tight">持久化键值存储</p>
  </Card>

  <Card href="/tauri/dialog">
    <h5 class="mb-2 text-lg font-bold tracking-tight text-gray-900 dark:text-white">Dialog</h5>
    <p class="font-normal text-gray-700 dark:text-gray-400 leading-tight">系统原生对话框</p>
  </Card>

  <Card href="/tauri/os">
    <h5 class="mb-2 text-lg font-bold tracking-tight text-gray-900 dark:text-white">操作系统信息</h5>
    <p class="font-normal text-gray-700 dark:text-gray-400 leading-tight">查看操作系统信息</p>
  </Card>
</div>