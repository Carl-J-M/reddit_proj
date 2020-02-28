<template lang="html">

  <ul>
    <li v-for="thread in listItemData" class="thread">
      {{thread[0].title}}
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
}
.thread:hover {
  color: blue;
}
</style>
