<template>
  <div id="app">

    <img id="logo" alt="Vue logo" src="https://external-preview.redd.it/sAcvIebeiBWPryrpGDb7G4KaqgpRK3ZZ6dgozI__pK8.png?auto=webp&s=abd5e766710c80c8384da1d5fb0529f509986c01">
    <h1 id="home-heading">Page 1 of www.reddit.com/r/{{subreddit}}</h1>
    <list-item :listItemData="listItemData"/>

  </div>
</template>

<script>


import ListItem from './components/ListItem.vue'

export default {
  name: 'App',
  data() {
    return {
      pageData: {},
      listItemData: [],
      subreddit: ""
    }
},
  components: {
    "list-item": ListItem
    //
  },
  methods: {
      formatThreads: function(threadArray) {

        threadArray.forEach((thread) => {
          let newArray = [];
          newArray.push(thread.data);
          this.listItemData.push(newArray);
        })

      },
      getSubreddit: function(threadArray) {
      this.subreddit = threadArray[0].data.subreddit;

      }
  },

  mounted() {
    fetch('https://www.reddit.com/r/globaloffensive.json')
    .then(response => response.json())
    .then((pageData) => {
      this.pageData = pageData;
      this.formatThreads(pageData.data.children);
      this.getSubreddit(pageData.data.children);
    })


  }
}
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  color: #2c3e50;
  margin-top: 60px;
}
#logo {
height: 7em;
width: auto;
margin-left: 40%;
}
#home-heading {
  text-align: center;
}
</style>
