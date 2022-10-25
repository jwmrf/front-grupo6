<script>
import QuestionVue from './Question.vue';
import axios from "axios";
//axios.defaults.headers.common['Access-Control-Allow-Origin'] = '*';
//axios.defaults.headers.common['Access-Control-Allow-Methods'] = "GET, POST, PATCH, PUT, DELETE, OPTIONS";
//axios.defaults.headers.common['Access-Control-Allow-Headers'] = "Origin, X-Requested-With, Content-Type, Accept";
import { ref, computed, onMounted } from "vue";

export default {
  components: {
    QuestionVue
  },
  props: ['tag'],
  setup(props) {
    const data = ref(null);
    const loading = ref(true);
    const error = ref(null);

    function fetchData() {
      loading.value = true;

      return axios.get(`http://127.0.0.1:3000/questionByTag?tag=${props.tag}`).then(function (response) {
        console.log(response);
      })
      .catch(function (error) {
        console.log(error);
      })
      .finally(function () {
        // always executed
      });
    }

    onMounted(() => {
      fetchData();
    });

    return {
      data,
      loading,
      error
    }
  },
  created: function() {
    //const connection = new WebSocket("ws://127.0.0.1:4000/");

    //connection.onmessage = event => {
      //console.log("received");
    //}
  }
}
</script>

<template>
  <div class="container">
    <div class="header">
      <h3>
        <slot name="name"></slot>
      </h3>
      <button class="delete">
        <font-awesome-icon :icon='["fas", "trash"]' />
      </button>
    </div>
    <div class="body">
      <QuestionVue></QuestionVue>
    </div>
  </div>
</template>

<style scoped>
.container {
  height: 100%;
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
  height: 100%;
  overflow-y: scroll;
}
</style>