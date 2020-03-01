<template lang="html">

  <ul id="container">
    <li v-for="thread in listItemData" class="thread">
      <h2 id="thread-title"><a class="nostyle" :href="thread[0].url">{{thread[0].title}}</a></h2>
      <p>Upvotes:<div class="bold">{{thread[0].ups}}</div></p>
      <p>Author: <div class="bold">{{thread[0].author}}</div></p>
      <p id="text">{{thread[0].selftext.substring(0, 400)}} ...</p>
      <a id="reddit-link" :href="thread[0].url">View on Reddit</a>

    </li>
  </ul>
</template>

<script>
export default {
  name: 'list-item',
  props: ['listItemData'],
}

</script>

<style lang="css" scoped>
.thread {
  margin-left: 20px;
  margin-bottom: 30px;
    list-style-type: none;
}
#reddit-link {

  color: #2c3e50;
  font-weight: bold;
  text-decoration: none;
  border-bottom: solid red 2px;
  padding: 5px 10px;
  margin-top: 20px;


}

#reddit-link:hover {

  color: red;


}

#thread-title {

max-width: 45%;
text-align: center;
border-bottom: solid red 2px;
margin-top: 40px;


}
#thread-title:hover {
color: red;
border-radius: 5px;
}

#container {

}

#text {
  padding: 30px;
}
.bold {
  font-weight: bold;
  display: inline-block;
}
.nostyle{
  color: inherit;
  text-decoration: inherit;
}
</style>
