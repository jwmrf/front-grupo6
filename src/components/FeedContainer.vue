<script>
import FeedVue from './Feed.vue';

export default {
  props: {
    feeds : []
  },
  components: {
    FeedVue
  },
  data () {
    return {
      feeds: [],
      tags: ["todas","c#","java","nodejs","javascript","python","php","android","ios","mysql","node.js"]
    }
  },
  watch: {
    feeds : function(val) {
    }
  },
  methods: {
    addFeed(x) {
      this.feeds.push({'id': Math.floor(Date.now() / 1000), 'name': 'android', 'icon': 'list'})
    },
    removeFeed(id) {
      this.feeds.splice(this.feeds.findIndex(el => el.id == id), 1);
    },
    changeTag(newTag, feedId) {
      const id = this.feeds.findIndex(el => el.id == feedId);

      this.feeds[id].name = newTag;
    }
  },
  mounted() {
    this.feeds = this.$props.feeds
    //this.$root.$on('addFeed', this.addFeed())

  }
}
</script>

<template>
  <div class="main" @addfeed="addFeed">
    <FeedVue v-for="feed in feeds" :tag="feed.name" :feedid="feed.id" :key="feed" @removefeed="removeFeed" @change-tag="changeTag">
      <template #name>
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