<script setup lang="ts">
import type { ContentNavigationItem } from '@nuxt/content'

const route = useRoute()
const navigation = inject<Ref<ContentNavigationItem[]>>('navigation')

const items = computed(() => [{
  label: 'Docs',
  to: '/docs',
  active: route.path.startsWith('/docs')
}, {
  label: 'Kinerja',
  to: '/kinerja',
  active: route.path.startsWith('/kinerja')
}, {
  label: 'Blog',
  to: '/blog',
  active: route.path.startsWith('/blog')
}, {
  label: 'Sejarah',
  to: '/sejarah',
  active: route.path.startsWith('/sejarah')
}])

const isDocs = computed(() => route.path.startsWith('/docs'))
</script>

<template>
  <UHeader>
    <template #left>
      <NuxtLink to="/" class="flex items-center gap-2">
        <AppLogo class="w-auto h-6 shrink-0" />
        <span class="font-bold text-lg hidden sm:block">OSIS SMK Assalaam</span>
      </NuxtLink>
    </template>

    <UNavigationMenu
      :items="items"
      variant="link"
    />

    <template #right>
      <UContentSearchButton />

      <UColorModeButton />

      <UButton
        icon="i-simple-icons-github"
        color="neutral"
        variant="ghost"
        to="https://github.com/DavinGM/OSIS_SMK_Assalaam_Bandung"
        target="_blank"
        aria-label="GitHub"
      />
    </template>

    <template #body>
      <UNavigationMenu
        :items="items"
        orientation="vertical"
        class="-mx-2.5"
      />

      <template v-if="isDocs">
        <USeparator class="my-6" />

        <UContentNavigation
          :navigation="navigation"
          highlight
        />
      </template>
    </template>
  </UHeader>
</template>
