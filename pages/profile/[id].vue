
<script setup lang="ts">
import {Employee, useEmployeesStore} from "~/store/employees";

const route = useRoute()
const useEmployees = useEmployeesStore()
const profileId = +route.params?.id

const employeeProfile = computed(() => {
  return useEmployees.getEmployees.find((f) => f.id === profileId) as Employee
})

const sliderPopularity = ref(employeeProfile.value.popularity)

function updateSliderPopularity(popularity: string, id: number) {
  useEmployees.setPopularity(popularity, id)
}

onBeforeMount(() => {
  useEmployees.setCurrentActiveItem(profileId)
})
</script>


<template>
    <div class="grid md:grid-cols-4 place-content-center">
      <div class="md:col-span-1">
        <figure class="relative">
          <nuxt-picture
            :src="`/images/profile/${employeeProfile.image}`"
            width="128"
            height="128"
            sizes="xs:128px md:350px"
            class="md:absolute -top-10 shadow-xl shadow-black/40"
          />
        </figure>
      </div>
      <div class="flex flex-col md:col-span-3 gap-4 max-w-[640px] text-white">
        <div class="relative">
          <p class="text-4xl md:absolute -top-10 bg-gray-800/20">{{ employeeProfile.name }}</p>
        </div>
        <div class="inline-flex items-center gap-4">
          <span class="text-xl text-white">Popularity</span>
          <URange
            v-model="sliderPopularity"
            :min="1"
            :max="10"
            @input="updateSliderPopularity($event.target.value, employeeProfile.id)"
          />
        </div>
        <UCard
          :ui="{
            background: 'bg-gray-900',
          }"
        >
          <template #header>
            <p class="font-bold text-xl text-white">Biography</p>
          </template>

          <article class="text-gray-400">{{ employeeProfile.biography }}</article>
        </UCard>
      </div>
    </div>

</template>
