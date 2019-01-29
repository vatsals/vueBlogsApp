<template>
  <div class="hello">
    <h1 :class="{red: true, blue: false}">Name: {{ fname }}</h1>
    <p>{{ greet('Morning') }}</p>
    <input type="text" v-model="fname" v-on:input="weblink" @keyup.enter="logDetails" @keyup.alt.enter="alertDetails" />
    <a :href="link" target="_blank">Website</a>
    <br />
    <p>{{ age }}</p>
    <button @click.once="age++">Age Inc Once</button>
    <button v-on:dblclick="age-=2">Age Dec Dbl</button>
  </div>
</template>

<script>
export default {
  name: 'Tutorial',
  data: function() {
    return {
      fname: 'Vatsals',
      lname: 'Shrivastav',
      link: 'https://github.com/vatsals',
      age: 22
    }
  },
  methods: {
    greet: function(time) {
      return 'Hi, Good ' + time + ' ' + this.fname + ' ' + this.lname + '!';
    },
    weblink: function(event) {
      this.link = 'https://github.com/' + event.target.value.toLowerCase();
    },
    logDetails: function(event) {
      console.log(event.target.value);
    },
    alertDetails: function() {
      alert(this.link);
    }
  }
}
</script>

<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
