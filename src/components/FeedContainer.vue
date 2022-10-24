<script>
import FeedVue from './Feed.vue';

export default {
  components: {
    FeedVue
  },
  data () {
    return {
      feeds: [{"id": 1, "name": "feed 1"}, {"id": 2, "name": "list 2"}]
    }
  }
}
</script>

<template>
  <div class="main">
    <FeedVue v-for="feed in feeds">
      <template #name>
        {{ feed.name }}
      </template>
    </FeedVue>
  </div>
</template>

<style scoped>
.main {
  display: flex;
  height: 100%;
  padding: .5rem;
  overflow-x: auto;
}
</style>