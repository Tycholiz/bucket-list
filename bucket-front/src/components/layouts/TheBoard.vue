<template>
  <div
    class="panel-container"
    fit-width="true"
    transition-duration="0.4s"
    percent-position:="percent-position:" true="true"
    item-selector=".item"
    :origin-top="true"
    :horizontal-order="false">
    <h3 class="panel-container__text">{{this.board.name}}</h3>
    <card class="item"
      v-for="post in posts" :key="post.id"
      :style="{ backgroundImage: 'url(' + post.photo_url + ')', backgroundSize: 'cover' }"
      :post="post">
    </card>
  </div>
</template>

<script>
import axios from 'axios';
import Card from '../cards/Card';

export default {
  components: {
    Card,
  },
  data() {
    return {
      posts: [],
      board: [],
      errors: [],
    };
  },
  created() {
    axios.get(`http://localhost:3000/boards/${this.$route.params.id}`)
      .then((response) => {
        this.posts = response.data.posts;
        this.board = response.data.board;
      })
      .catch((e) => {
        this.errors.push(e);
      });
  },
};
</script>

<style scoped lang="stylus">

</style>
