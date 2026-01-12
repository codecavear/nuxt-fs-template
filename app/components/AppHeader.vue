<script setup lang="ts">
const { t, locale, locales, setLocale } = useI18n()
const route = useRoute()

const items = computed(() => [{
  label: t('nav.docs'),
  to: '/docs',
  active: route.path.startsWith('/docs')
}, {
  label: t('nav.pricing'),
  to: '/pricing'
}, {
  label: t('nav.blog'),
  to: '/blog'
}])

const localeItems = computed(() => {
  return (locales.value as Array<{ code: string; name: string }>).map(l => ({
    label: l.name,
    click: () => setLocale(l.code)
  }))
})
</script>

<template>
  <UHeader>
    <template #left>
      <NuxtLink
        to="/"
        class="flex items-center gap-2 text-xl font-bold"
      >
        <UIcon
          name="i-lucide-box"
          class="w-6 h-6 text-primary"
        />
        App
      </NuxtLink>
    </template>

    <UNavigationMenu
      :items="items"
      variant="link"
    />

    <template #right>
      <UDropdownMenu :items="[localeItems]">
        <UButton
          icon="i-lucide-globe"
          color="neutral"
          variant="ghost"
          size="sm"
        />
      </UDropdownMenu>

      <UColorModeButton />

      <UButton
        icon="i-lucide-log-in"
        color="primary"
        variant="ghost"
        to="/login"
        class="lg:hidden"
      />

      <UButton
        :label="t('nav.getStarted')"
        color="primary"
        to="/login"
        class="hidden lg:inline-flex"
      />
    </template>

    <template #body>
      <UNavigationMenu
        :items="items"
        orientation="vertical"
        class="-mx-2.5"
      />

      <USeparator class="my-6" />

      <div class="flex items-center gap-2 mb-4">
        <UButton
          v-for="l in (locales as Array<{ code: string; name: string }>)"
          :key="l.code"
          :label="l.name"
          :color="locale === l.code ? 'primary' : 'neutral'"
          :variant="locale === l.code ? 'solid' : 'ghost'"
          size="sm"
          @click="setLocale(l.code)"
        />
      </div>

      <UButton
        :label="t('nav.getStarted')"
        color="primary"
        to="/login"
        block
      />
    </template>
  </UHeader>
</template>
