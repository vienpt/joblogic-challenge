<template>
  <nav class="sidebar">
<!--    header-->
    <header class="sidebar-header">
      <div class="py-4 px-8 grid gap-8">
        <NuxtLink to="/">
          <Logo id="logo" />
        </NuxtLink>
      </div>
    </header>
<!--    content-->
    <div class="sidebar-content">
      <div class="sidebar-content_items">
        <div v-for="emp in employees" :key="emp.id">
          <NuxtLink :to="`/profile/${emp.id}`" active-class="bg-blue-500">
            <span
              :style="{ fontSize: `${useEmployees.popularity && emp.popularity}em !important` }"
            >
              {{ emp.name }}
            </span>
          </NuxtLink>
          <ul class="sidebar-content_items-colleagues">
            <li class="cursor-default" v-for="(colleague, index) in emp.colleagues" :key="index">
              <span class="italic">{{ colleague }}</span>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup lang="ts">
import Logo from "~/components/Svg/Logo.vue";
import {useEmployeesStore} from "~/store/employees";

const useEmployees = useEmployeesStore()
const employees = computed(() => useEmployees.getEmployees)
</script>

<style lang="postcss" scoped>
  .sidebar {
    height: 100%;
    width: 260px;
    position: absolute;
    left: 0;
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 350px auto;
    grid-template-areas:
      "logo"
      "items";

    background-color: rgba(0,0,0, 0.4);

    &-header {
      grid-area: logo;
      @apply flex justify-center items-center;
    }

    &-content {
      grid-area: items;
      @apply mt-20 overflow-y-auto overflow-x-hidden text-center;

      &_items {
        @apply flex flex-col p-5;

        &-colleagues {
          grid-area: category;
          @apply flex flex-col px-10;
        }
      }
    }

    #logo {
      @apply fill-white;
    }
  }
</style>
