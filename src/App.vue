<template>
  <div>
    <app-header />
    <router-view />
  </div>
</template>

<script>
import addBlog from './components/addBlog.vue';
import showBlogs from './components/showBlogs.vue';
import listBlogs from './components/listBlogs.vue';
import header from './components/header.vue';

export default {
  components: {
    'add-blog': addBlog,
    'show-blogs': showBlogs,
    'list-blogs': listBlogs,
    'app-header': header
  },
  data() {
    return {
    }
  },
  methods: {
 
  }
}
</script>

<style lang="scss">
body {
  margin: 0;
  font-family: 'Arial';
}
</style>
