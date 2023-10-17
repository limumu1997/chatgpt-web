<script setup lang='ts'>
import { onMounted, ref } from 'vue'
import { NSpin } from 'naive-ui'
import { fetchChatConfig } from '@/api'
import pkg from '@/../package.json'

interface ConfigState {
  timeoutMs?: number
  reverseProxy?: string
  apiModel?: string
  socksProxy?: string
  httpsProxy?: string
  usage?: string
}

const loading = ref(false)

const config = ref<ConfigState>()

async function fetchConfig() {
  try {
    loading.value = true
    const { data } = await fetchChatConfig<ConfigState>()
    config.value = data
  }
  finally {
    loading.value = false
  }
}

onMounted(() => {
  fetchConfig()
})
</script>

<template>
  <NSpin :show="loading">
    <div class="p-4 space-y-4">
      <h2 class="text-xl font-bold">
        Version - {{ pkg.version }}
      </h2>
      <h3>免责声明</h3>
      <div class="p-2 space-y-2 rounded-md bg-neutral-100 dark:bg-neutral-700">
        <p>
          1. 本产品提供的信息仅供参考，不构成任何投资、法律或其他专业建议。任何人不应该根据本产品中的信息来做出任何决策。
        </p>
        <p>
          2. 本产品内所提供的链接和内容可能包含有第三方网站的信息，这些内容并不代表本产品赞同或推荐该网站。
        </p>
        <p>
          3. 本产品不保证网站服务将无中断、及时提供、安全可靠或不会出现错误。使用者承认其使用本产品的风险由其自行承担。
        </p>
        <p>
          4. 本产品不对用户因使用或不能使用本产品或其内容而遭受的任何直接、间接、意外、特殊或结果性损失负责。
        </p>
        <p>
          5. 本产品有权在不事先通知用户的情况下，在任何时间暂停或终止本产品的访问权限，或修改本声明。
        </p>
        <p>
          使用本产品，即表示您已经完全理解并且接受了上述免责声明中的所有条款和条件。如果您不同意这些条款和条件，请立刻停止使用本产品。
        </p>
      </div>
    </div>
  </NSpin>
</template>
