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
      this.feeds.push({'id': Math.floor(Date.now() / 1000), 'name': `Feed ${this.feeds.length + 1}`, 'icon': 'list'})
    },
    removeFeed(id) {
      console.log(id);
      this.feeds.splice(0, this.feeds.length, this.feeds.filter(el => el.id != id));
    }
  },
  mounted() {
    this.feeds = this.$props.feeds
    //this.$root.$on('addFeed', this.addFeed())

  }
}
</script>

<template>
  <div class="main" @addfeed="addFeed" @removefeed="removeFeed">
    <FeedVue v-for="feed in feeds" :tag="feed.name" :feedid="feed.id" :key="feed">
      <template #name>
        <select>
          <option v-for="tag in tags" :key="tag" :value="tag">{{tag}}</option>
        </select>
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