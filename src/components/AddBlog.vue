<template>
    <div id="add-blog">
        <h2>Add a New Blog Post</h2>
        <form v-if="!submitted">
            <label>Blog Title:</label>
            <input type="text" v-model.lazy="blog.title" required />
            <label>Blog Content:</label>
            <textarea v-model.lazy.trim="blog.content"></textarea>
            <div id="checkboxes">
                <p>Blog Categories:</p>
                <label>News</label>
                <input type="checkbox" value="news" v-model="blog.categories" />
                <label>Sports</label>
                <input type="checkbox" value="sports" v-model="blog.categories" />
                <label>Travel</label>
                <input type="checkbox" value="travel" v-model="blog.categories" />
                <label>Technology</label>
                <input type="checkbox" value="technology" v-model="blog.categories" />
            </div>
            <label>Author:</label>
            <select v-model="blog.author">
                <option v-for="(author, index) in authors" v-bind:key="index">{{ author }}</option>
            </select>
            <hr />
            <button v-on:click.prevent="post">Add Blog</button>
        </form>
        <div v-if="submitted">
            <h3>Thanks for adding your post</h3>
        </div>
        <div id="preview">
            <h3>Preview blog</h3>
            <p>Blog title: {{ blog.title }}</p>
            <p>Blog content:</p>
            <p style="white-space: pre;">{{ blog.content }}</p>
            <p>Blog Categories:</p>
            <ul>
                <li style="text-transform: capitalize;" v-for="(category, index) in blog.categories" v-bind:key="index">{{ category }}</li>
            </ul>
            <p>Author: {{ blog.author }}</p>
        </div>
    </div>
</template>

<script>
export default {
    data () {
        return {
            blog: {
                title: '',
                content: '',
                categories: [],
                author: ''
            },
            authors: ['Author 1', 'Author 2', 'Author 3'],
            submitted: false
        }
    },
    methods: {
        post: function(){
            this.$http.post('https://vuejs-1f6e8.firebaseio.com/posts.json', this.blog)
                .then(function(data){
                    this.submitted = true;
                });
        }
    }
}
</script>

<style>
#add-blog * {
    box-sizing: border-box;
}
#add-blog {
    margin: 20px auto;
    max-width: 500px;
}
label {
    display: block;
    margin: 20px 0 10px;
}
input[type="text"], textarea {
    display: block;
    width: 100%;
    padding: 8px;
}
#preview {
    padding: 10px 20px;
    border: 1px dotted #ccc;
    margin: 30px 0;
}
h3 {
    margin-top: 10px;
}
#checkboxes input {
    display: inline-block;
    margin-right: 10px;
}
#checkboxes label {
    display: inline-block;
    margin-top: 0;
}
</style>