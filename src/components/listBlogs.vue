<template>
  <div v-theme:column="'narrow'" id="show-blogs"> 
    <h1>List Blog Titles</h1>
    <input type="text" v-model="search" placeholder="search blogs" />
    <div v-for="blog in filteredBlogs" class="single-blog">
      <h3 v-rainbow>{{ blog.title | to-uppercase }}</h3>
    </div>
  </div>
</template>

<script>
import searchMixin from '../mixins/searchMixin';

export default {
  data() {
    return {
      blogs: [],
      search: ''
    }
  },
  methods: {
    
  },
  created() {
    this.$http.get('https://jsonplaceholder.typicode.com/posts')
    .then(data => {
      this.blogs = data.body.slice(0, 10);
    })
    .catch();
  },
  computed: {
 
  },
  filters: {
    'to-uppercase': value => value.toUpperCase(),
    'snippet': value => value.slice(0, 100) + '...'
  },
  directives: {
    'rainbow': {
      bind(el, binding, vNode) {
        el.style.color = "#" + Math.random().toString().slice(2, 8);
      }
    },
    'theme': {
      bind(el, binding, vNode) {
        if(binding.value == 'wide') {
          el.style.maxWidth = '1200px';
        }
        else if(binding.value == 'narrow') {
          el.style.maxWidth = '560px';
        }

        if(binding.arg == 'column') {
          el.style.background = '#ddd';
          el.style.padding = '20px';
        }
      }
    }
  },
  mixins: [searchMixin]
}
</script>

<style lang="scss">
#show-blogs {
  max-width: 500px;
  margin: 0 auto;
}

.single-blog {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eee;
}
</style>
