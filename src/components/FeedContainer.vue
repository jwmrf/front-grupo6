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
      console.log(x)
      console.log(1)
      this.feeds.push({'id': 1, 'name': 'item 1', 'icon': 'list'})
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
    <FeedVue v-for="feed in feeds" :tag="feed.name" :key="feed">
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