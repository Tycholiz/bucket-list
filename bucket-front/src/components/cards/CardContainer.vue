<template lang="pug">
  .panel-container(
    fit-width="true",
    percent-position: true,
    item-selector='.item',
    :origin-top="true",
    :horizontal-order="false",
  )
    card.item(
      v-for='(post, index) in posts',
      :key='post.id',
      :style="{ backgroundImage: 'url(' + post.photo_url + ')', backgroundSize: 'cover' }",
      :post='post',
    )
</template>

<script>
import axios from 'axios';
import Card from './Card';

export default {
  components: {
    Card
  },
  data() {
    return {
      posts: [],
      errors: [],
    };
  },
  created() {
    axios.get('http://localhost:3000/posts')
      .then((response) => {
        this.posts = response.data.posts;
      })
      .catch((e) => {
        this.errors.push(e);
      });
  },
};
</script>

<style scoped lang="stylus">

</style>
