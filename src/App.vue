<script>
import { RouterView } from "vue-router"
import UserLayout from "@/layouts/UserLayout.vue"

export default {
  name: "app",
  components: {
    UserLayout,
  },
}
</script>

<template>
  <UserLayout />

  <RouterView />
</template>
