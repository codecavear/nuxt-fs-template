<script setup lang="ts">
const { t } = useI18n()

useSeoMeta({
  titleTemplate: '',
  title: t('home.seo.title'),
  ogTitle: t('home.seo.title'),
  description: t('home.seo.description'),
  ogDescription: t('home.seo.description')
})

const heroLinks = computed(() => [
  {
    label: t('home.hero.getStarted'),
    icon: 'i-lucide-arrow-right',
    trailing: true,
    to: '/login',
    size: 'xl' as const
  },
  {
    label: t('home.hero.viewDocs'),
    icon: 'i-lucide-book-open',
    size: 'xl' as const,
    color: 'neutral' as const,
    variant: 'subtle' as const,
    to: '/docs'
  }
])

const sections = computed(() => [
  {
    title: t('home.sections.production.title'),
    description: t('home.sections.production.description'),
    orientation: 'horizontal' as const,
    features: [
      { name: t('home.features.auth.title'), description: t('home.features.auth.description'), icon: 'i-lucide-shield-check' },
      { name: t('home.features.database.title'), description: t('home.features.database.description'), icon: 'i-lucide-database' },
      { name: t('home.features.i18n.title'), description: t('home.features.i18n.description'), icon: 'i-lucide-globe' }
    ]
  },
  {
    title: t('home.sections.developer.title'),
    description: t('home.sections.developer.description'),
    orientation: 'horizontal' as const,
    reverse: true,
    features: [
      { name: t('home.features.typescript.title'), description: t('home.features.typescript.description'), icon: 'i-lucide-code-2' },
      { name: t('home.features.fast.title'), description: t('home.features.fast.description'), icon: 'i-lucide-zap' },
      { name: t('home.features.darkMode.title'), description: t('home.features.darkMode.description'), icon: 'i-lucide-moon' }
    ]
  }
])

const featureItems = computed(() => [
  { title: t('home.features.components.title'), description: t('home.features.components.description'), icon: 'i-lucide-palette' },
  { title: t('home.features.seo.title'), description: t('home.features.seo.description'), icon: 'i-lucide-search' },
  { title: t('home.features.accessible.title'), description: t('home.features.accessible.description'), icon: 'i-lucide-accessibility' },
  { title: t('home.features.secure.title'), description: t('home.features.secure.description'), icon: 'i-lucide-lock' },
  { title: t('home.features.deploy.title'), description: t('home.features.deploy.description'), icon: 'i-lucide-cloud' },
  { title: t('home.features.customizable.title'), description: t('home.features.customizable.description'), icon: 'i-lucide-settings' }
])

const ctaLinks = computed(() => [
  { label: t('home.cta.getStarted'), to: '/login', trailingIcon: 'i-lucide-arrow-right' },
  { label: t('home.cta.readDocs'), to: '/docs', variant: 'subtle' as const, icon: 'i-lucide-book-open' }
])
</script>

<template>
  <div>
    <UPageHero
      :description="t('home.description')"
      :links="heroLinks"
    >
      <template #top>
        <HeroBackground />
      </template>

      <template #title>
        {{ t('home.title', { highlight: '' }) }}<span class="text-primary">{{ t('home.titleHighlight') }}</span>
      </template>

      <PromotionalVideo />
    </UPageHero>

    <UPageSection
      v-for="(section, index) in sections"
      :key="index"
      :title="section.title"
      :description="section.description"
      :orientation="section.orientation"
      :reverse="section.reverse"
      :features="section.features"
    >
      <ImagePlaceholder />
    </UPageSection>

    <UPageSection
      :title="t('home.features.title')"
      :description="t('home.features.description')"
    >
      <UPageGrid>
        <UPageCard
          v-for="(item, index) in featureItems"
          :key="index"
          v-bind="item"
          spotlight
        />
      </UPageGrid>
    </UPageSection>

    <USeparator />

    <UPageCTA
      :title="t('home.cta.title')"
      :description="t('home.cta.description')"
      :links="ctaLinks"
      variant="naked"
      class="overflow-hidden"
    >
      <LazyStarsBg />
    </UPageCTA>
  </div>
</template>
