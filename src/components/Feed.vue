<script>
import QuestionVue from './Question.vue';
import axios from "axios";

import { ref } from "vue";

export default {
  components: {
    QuestionVue
  },
  data () {
    return {
      feedData: [],
      changedTag: undefined,
      tags: ["todas","c#","java","nodejs","javascript","python","php","android","ios","mysql","node.js"]
    }
  },
  computed: {
    computeTag() {
      if (this.changedTag !== undefined) {
        return this.changedTag;
      }

      return this.tag;
    }
  },
  mounted() {
    //setInterval(() => {
      this.fetchData()
    //}, 5000)
  },
  methods: {
    async fetchData() {
      const data = ref(null);
      const loading = ref(true);
      const error = ref(null);
      const tag = this.computeTag == 'todas' ? '' : this.computeTag;
      loading.value = true;
      let response = await axios.get(`http://127.0.0.1:3000/questionByTagNormal?tag=${tag}`)
      this.feedData = response.data.data
      console.log(this.feedData)
      return {
        data,
        loading,
        error
      }
    },
    onChange(event) {
      this.changedTag = event.target.value;
      this.fetchData();
    },  
    removeFeed() {
      this.$emit('removefeed', this.$props.feedid);
    }
  },
  props: ['tag','feedid']
}
</script>

<template>
  <div class="container">
    <div class="header">
        <select v-model="tag" @change="onChange($event)">
          <option v-for="tag in tags" :key="tag" :value="tag">{{tag}}</option>
        </select>
      <h3>
        <slot name="name"></slot>
      </h3>
      <button class="delete" @click="removeFeed()">
        <font-awesome-icon :icon='["fas", "trash"]' />
      </button>
    </div>
    <div class="body">
      <QuestionVue v-for="feed in feedData" :question="feed" :key="feed"></QuestionVue>
    </div>
  </div>
</template>

<style scoped>
.container {
  height: 97vh;
  min-width: 300px;
  max-width: 300px;
  background: var(--vt-c-white-mute);
  border-radius: .5rem;
}
.container:not(:last-of-type) {
  margin-right: .5rem;
}

.container .header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 3.5em;
  padding: .5rem;
  border-bottom: 1px solid var(--vt-c-divider-dark-2);
  color: var(--vt-c-black-mute);
}
.header .delete {
  padding: .3rem .45rem;
  background: transparent;
  border: none;
  cursor: pointer;
}

.container .body {
  height: 90%;
  overflow-y: scroll;
}
</style>