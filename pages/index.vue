<template>
  <div>
    <HomeHeroSection />
    <HomeStatSection />
    <div class="max-w-7xl mx-auto mt-14 px-4 sm:px-6 lg:px-8 lg:mt-24">
      <div class="space-y-8 sm:space-y-12">
        <div class="space-y-5 sm:mx-auto sm:max-w-xl sm:space-y-4 lg:max-w-5xl text-center">
          <h2 class="text-3xl font-extrabold tracking-tight sm:text-4xl">Où en est le projet ?</h2>
          <p class="text-xl text-gray-500">
            Ce projet est né au début de la mandature métropolitaine 2020-2026. 
            Après une phase de concertation, d'études techniques de faisabilité, l'élaboration du plan vélo 
            métropolitain, le projet est maintenant en phase de réalisation et de déploiment.<br /> 
            Les travaux se multiplient depuis l'année 2023.
          </p>
        </div>
      </div>
      <ProgressBar :voies="voies" class="mt-8 md:mt-10" />
      <Stats :voies="voies" class="mt-8" />
      <StatsQuality v-if="displayQuality() && displayQualityOnHomePage()" :voies="voies" class="mt-8" />
      <Typology :voies="voies" class="mt-8 max-w-2xl mx-auto" />
    </div>
    <div>
      <NuxtLink href="/tableau-de-bord" class="flex items-center justify-center text-lvv-blue-600 hover:underline">
        Voir le tableau de bord complet
        <Icon name="heroicons:arrow-right" class="ml-1 h-5 w-5" />
      </NuxtLink>
    </div>
    <div class="max-w-7xl mx-auto mt-14 px-4 sm:px-6 lg:px-8 lg:mt-24">
      <div class="space-y-8 sm:space-y-12">
        <div class="space-y-5 sm:mx-auto sm:max-w-xl sm:space-y-4 lg:max-w-5xl text-center">
          <h2 class="text-3xl font-extrabold tracking-tight sm:text-4xl">Avancement par ligne</h2>
          <p class="text-xl text-gray-500">
            Choisissez un itinéraire du {{ getRevName('singular') }} pour connaitre le détail du projet et voir son niveau
            d'avancement.
          </p>
        </div>
        <HomeLinesSection class="mt-5" />
      </div>
    </div>
    <div class="max-w-7xl mx-auto mt-14 px-4 sm:px-6 lg:px-8 lg:mt-24">
      <div class="space-y-8 sm:space-y-12">
        <div class="space-y-5 sm:mx-auto sm:max-w-xl sm:space-y-4 lg:max-w-5xl text-center">
          <h2 class="text-3xl font-extrabold tracking-tight sm:text-4xl">Contenu du site</h2>
          <p class="text-xl text-gray-500">
            Les informations figurant sur ce site ont été produites bénévolement de façon collaborative 
            par des citoyens engagés auprès de l'association Sabine. Certaines d'entre elles sont issues 
            des documents produits par la Métropole Rouen Normandie. D'autres, notammement celles 
            relatives à la qualification des tronçons ont été discutées au regard des critères définis 
            dans la <a href="https://revmrn.netlify.app/blog/methodo">méthodologie de caractérisation 
              des itinéraires</a>. Leur exactitude n'est pas garantie. Elles sont sujettes à discussion 
              et ont vocation à évoluer au rythme de l'avancement du projet. Les contributions pour les 
              tenir à jour sont les bienvenues.
          </p>
        </div>
        
      </div>
    </div>
    <div class="py-16">
      <LvvCta />
    </div>
  </div>
</template>

<script setup lang="ts">
import type { Collections } from '@nuxt/content';

const { getRevName, displayQuality, displayQualityOnHomePage } = useConfig();

const { geojsons } = await useVoiesCyclablesGeojson();
const voies: Ref<Collections['voiesCyclablesGeojson'][]> = computed(() => geojsons.value || []);
</script>
