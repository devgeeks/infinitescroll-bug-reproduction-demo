<template>
  <f7-page @infinite="onInfiniteScroll" infinite-scroll
    @page:afteranimation="onPageAfterAnimation"
  >
    <f7-navbar back-link="Back" sliding title="Infinite Scroll"></f7-navbar>
    <f7-block-title>Infinite Scroll</f7-block-title>
    <f7-block>
      <div class="grid">
        <div class="cell" v-for="image in images" :key="image.id">
          <img
            :src="image.thumbnailUrl"
          />
        </div>
      </div>
    </f7-block>
    <div v-if="!images.length">
      <div class="placeholder" />
    </div>
  </f7-page>
</template>

<script>
  export default {
    name: 'Scroll',
    data () {
      return {
        images: []
      };
    },
    methods: {
      onInfiniteScroll () {
        // ...
      },
      onPageAfterAnimation () {
        // console.log('onPageAfterAnimation');
        const root = 'https://jsonplaceholder.typicode.com';

        this.$$.get(`${root}/albums/2/photos/`, {}, (data) => {
          // console.log(data);
          this.images = JSON.parse(data);
        }, (err) => {
          console.error(err);
          this.$f7.alert(error);
        });
      }
    }
  };
</script>
