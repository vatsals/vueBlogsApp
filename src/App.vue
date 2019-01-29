<template>
    <div>
        <app-header></app-header>
        <router-view></router-view>
    </div>
</template>

<script>
import Header from './components/Header.vue';
import AddBlog from './components/AddBlog.vue';
import ShowBlogs from './components/ShowBlogs.vue';

export default {
    components: {
      'app-header': Header,
      'add-blog': AddBlog,
      'show-blogs': ShowBlogs
    },
    data () {
        return {
        }
    },
    methods: {
    }
}
</script>

<style>
/* @import url('https://fonts.googleapis.com/css?family=Roboto'); */
@import url('https://fonts.googleapis.com/css?family=Open+Sans');

body {
  margin: 0;
  font-family: 'Open Sans', sans-serif;
}
</style>