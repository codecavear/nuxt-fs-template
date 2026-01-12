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

const availableLocales = computed(() => {
  return (locales.value as Array<{ code: string; name: string }>).map(l => ({
    label: l.name,
    value: l.code
  }))
})

function switchLocale(code: string) {
  setLocale(code)
}
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
      <UDropdownMenu
        :items="availableLocales.map(l => [{ label: l.label, click: () => switchLocale(l.value) }]).flat()"
        :ui="{ content: 'min-w-24' }"
      >
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
          v-for="l in availableLocales"
          :key="l.value"
          :label="l.label"
          :color="locale === l.value ? 'primary' : 'neutral'"
          :variant="locale === l.value ? 'solid' : 'ghost'"
          size="sm"
          @click="switchLocale(l.value)"
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
