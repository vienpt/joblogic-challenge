
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
      <div class="flex flex-col md:col-span-3 gap-4">
        <div class="relative">
          <p class="text-4xl md:absolute -top-10">{{ employeeProfile.name }}</p>
        </div>
        <div class="flex items-center gap-3 max-w-[640px]">
          <p>Popularity</p>
          <input
            type="range"
            v-model="sliderPopularity"
            @input="updateSliderPopularity($event.target.value, employeeProfile.id)"
            min="1"
            max="9"
            class="w-full"
          />
        </div>
        <div class="bg-gray-900 p-5 max-w-[640px]">
          <p class="font-bold text-xl mb-2">Biography</p>
          <article class="text-gray-400">{{ employeeProfile.biography }}</article>
        </div>
      </div>
    </div>

</template>
