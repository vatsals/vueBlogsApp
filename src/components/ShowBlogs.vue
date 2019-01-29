<template>
    <div id="show-blogs">
        <h2>All Blog Articles</h2>
        <input type="text" class="srh" v-model="search" placeholder="Search blogs" />
        <div v-for="(blog, index) in filteredBlogs" class="single-blog" v-bind:key="index">
            <router-link v-bind:to="'/blog/' + blog.id" style="text-decoration: none;">
                <h3 v-rainbow>{{ blog.title | uppercase }}</h3>
            </router-link>
            <article>{{ blog.content | snippet }}</article>
        </div>
    </div>
</template>

<script>
import SearchMixin from '../mixins/SearchMixin';

export default {
    data () {
        return {
            blogs: [],
            search: ''
        }
    },
    methods: {
    },
    created() {
        this.$http.get('https://vuejs-1f6e8.firebaseio.com/posts.json')
            .then(function(data){
                return data.json();
            }).then(function(data) {
                const blogsArray = []
                for(let key in data) {
                    data[key].id = key;
                    blogsArray.push(data[key]);
                }
                this.blogs = blogsArray;
            });
    },
    computed: {

    },
    filters: {
        uppercase(value) {
            return value.toUpperCase();
        }
    }, 
    directives: {
        'rainbow': {
            bind(el) {
                el.style.color = '#' + Math.random().toString(16).slice(2, 8);
            }
        }
    },
    mixins: [SearchMixin]
}
</script>

<style>
#show-blogs {
    max-width: 800px;
    margin: 0px auto;
}
.single-blog {
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
}
.srh {
    width: 100%;
    padding: 5px;
}
</style>