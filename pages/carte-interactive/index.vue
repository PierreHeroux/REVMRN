<template>
  <ClientOnly>
    <Map :features="features" :options="{ geolocation: true }" class="h-full w-full" />
  </ClientOnly>
</template>

<script setup lang="ts">
import type { Collections } from '@nuxt/content';
const { getRevName } = useConfig();

// https://github.com/nuxt/framework/issues/3587
definePageMeta({
  pageTransition: false,
  layout: 'fullscreen'
});

const { data: geojsons } = await useAsyncData(() => {
  return queryCollection('voiesCyclablesGeojson').all();
});

const features: Ref<Collections['voiesCyclablesGeojson']['features']> = computed(() => {
  if (!geojsons.value) return [];
  return geojsons.value.flatMap(geojson => geojson.features);
});

const description =
  `Découvrez la carte interactive du ${getRevName()}. Itinéraires rue par rue. Plan régulièrement mis à jour pour une information complète.`;
const COVER_IMAGE_URL = 'https://sabinerouenvelo.org/wp-content/uploads/2023/02/logo_noir_texte.png';
useHead({
  title: `Carte à jour des ${getRevName()}`,
  meta: [
    // description
    { key: 'description', name: 'description', content: description },
    { key: 'og:description', property: 'og:description', content: description },
    { key: 'twitter:description', name: 'twitter:description', content: description },
    // cover image
    { key: 'og:image', property: 'og:image', content: COVER_IMAGE_URL },
    { key: 'twitter:image', name: 'twitter:image', content: COVER_IMAGE_URL }
  ]
});
</script>
