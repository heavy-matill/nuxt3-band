<script lang="ts" setup>
import type { QueryBuilderParams } from '@nuxt/content/dist/runtime/types'
// compiler micro
definePageMeta({ layout: 'page' })
useHead({ title: 'Events' })
// query
// const query: QueryBuilderParams = { path: '/post' }

function routeTo(event: MouseEvent, to: string) {
  const router = useRouter()
  if (to) {
    router.push(to)
  }
  event.preventDefault()
}
</script>

<template>
  <LayoutPageWrapper>
    <LayoutPageHeader>
      <LayoutPageTitle text="Tour" class="capitalize" />
    </LayoutPageHeader>
    <LayoutPageSection>
      <ContentList path="/tour">
        <template #default="{ list }">
          <div v-for="year in new Set(list.map(t => t.date.split('-')[0]))">
            <div class="mt-1 text-4xl text-gray-600 dark:text-gray-400 text-right">{{ year }}</div>
            <div v-for="tour in list.filter(t => t.date.startsWith(year))" :key="tour._path"
              class="pointer hover:no-underline p-6 flex space-x-6 rounded border border-gray-900/10 dark:border-gray-50/[0.2] mb-4"
              @click="(e) => routeTo(e, tour._path)">

              <div class="flex flex-col mt-1 text-5xl text-gray-600 dark:text-gray-400 ">
                <div>{{ String(new Date(tour.date)).split(" ").slice(1, 3).join(" ") }}</div>
              </div>
              <div class="mt-1 text-gray-600 dark:text-gray-400 text-right">
                <div>{{ String(new Date(tour.date)).split(" ")[0] }}</div>
                <div>{{ tour.time.split("-")[0] }}</div>
                <!--div>{{ String(new Date(tour.date)).split(" ")[3] }}</div-->
              </div>
              <div class="flex flex-col">
                <AwesomeLink class="text-md flex space-x-1 items-center text-primary-500" :to="tour._path">
                  <div class="text-2xl font-semibold text-gray-800 dark:text-gray-50">
                    {{ tour.title }}
                  </div>
                </AwesomeLink>
                <div class="text-gray-700 dark:text-gray-300 mb-1">
                  {{ tour.city }},
                  {{ tour.location }}
                </div>
              </div>
            </div>
          </div>
        </template>
        <template #not-found>
          <p>No articles found.</p>
        </template>
      </ContentList>
    </LayoutPageSection>
  </LayoutPageWrapper>
</template>
<style scoped>
.pointer {
  cursor: pointer
}
</style>
