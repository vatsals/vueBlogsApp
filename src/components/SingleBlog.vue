<template>
    <div id="single-blog">
        <h2 style="text-transform: capitalize;">{{ blog.title }}</h2>
        <article>{{ blog.content }}</article>
        <p>Author: {{ blog.author }}</p>
        <ul>
            <li v-for="(category, index) in blog.categories" v-bind:key="index" style="text-transform: capitalize;">
                {{ category }}
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    data () {
        return {
            id: this.$route.params.id,
            blog: {}
        }
    },
    created() {
        this.$http.get('https://vuejs-1f6e8.firebaseio.com/posts/' + this.id + '.json')
            .then(function(data){
                return data.json();
            }).then(function(data) {
                this.blog = data;
            });
    }
}
</script>

<style>
#single-blog {
    max-width: 960px;
    margin: 0 auto;
}
</style>