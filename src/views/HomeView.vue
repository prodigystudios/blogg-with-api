<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <blogg-posts-list/>
  </div>
</template>


<script>
import BloggPostsList from '@/components/BloggPostsList.vue'
export default {
  components: {
    BloggPostsList,
  }
}
</script>
