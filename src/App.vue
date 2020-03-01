<template>
  <div id="app">

    <img id="logo" alt="Vue logo" src="https://external-preview.redd.it/sAcvIebeiBWPryrpGDb7G4KaqgpRK3ZZ6dgozI__pK8.png?auto=webp&s=abd5e766710c80c8384da1d5fb0529f509986c01">

<form class="" action="index.html" method="post">
      <h1 id="home-heading">www.reddit.com/r/
        <input id="example" name="subreddit-input" v-model="subreddit" v-on:change="getNewPageData(subreddit)" autofocus/>

      <h3 id="current-sub-header">Currently Browsing /r/{{subreddit}}</h3>
    </h1>

</form>

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
computed: {

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

    },
      getNewPageData: function(subreddit) {
        this.listItemData = [];
        let newRequest = `https://www.reddit.com/r/${subreddit}/.json`;
        console.log(newRequest);
          fetch(newRequest)
          .then(response => response.json())
          .then((pageData) => {
            this.pageData = pageData;
            this.formatThreads(pageData.data.children);
          })
          console.log("After getNewPageData called:", this.pageData);
      }
  },

  mounted() {
    fetch(`https://www.reddit.com/r/iama/.json`)
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
display: block;
margin-left: auto;
margin-right: auto;
}
#home-heading {
  text-align: center;
  border-bottom: solid lightgray 2px;
  padding-bottom: 20px;
}

#example {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 24px;
  color: gray;
  border: none;
  /* border-bottom: solid #2c3e50 2px; */
  margin-top: 3px;
  margin-left: 10px;
  position: absolute;



}
#current-sub-header {
  color: red;
  font-size: 18px;
}
</style>
