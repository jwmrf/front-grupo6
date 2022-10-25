<script>
import moment from 'moment'

import socketioService from '../services/socketio.service';

export default {
  created: function () {
    this.moment = moment
  },
  data() {
    return {
      datecreation: moment.unix(this.question.creation_date).fromNow()
    }
  },
  mounted() {
    const socket = socketioService.getSocket();

    socket.on("new_question", (data) => {
      this.datecreation = this.moment.unix(this.$props.question.creation_date).fromNow();
      console.log('update', this.datecreation);
    });
  },
  props: {
    question : {}
  }
}
</script>

<template>
  <div class="question_container">
    <img class="avatar" :src="question.owner.profile_image" />
    <div class="content">
      <span class="username">
        {{question.owner.display_name}}
        <span v-text="datecreation"></span>
      </span>
      <p class="question"><a :href="question.link" target="_blank">{{question.title}}</a></p>
      <ul class="tags">
        <li v-for="tag in question.tags" :key="tag">{{tag}}</li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.question_container {
  display: grid;
  grid-template-columns: 60px 1fr;
  padding: 1rem;
  border-bottom: 1px solid #ccc;
}
.question_container .avatar {
  width: 45px;
  height: 45px;
  border-radius: 50%;
}
.question_container .content {
  color: var(--vt-c-black-mute);
}
.question_container .username {
  display: flex;
  justify-content: space-between;
  font-size: .75rem;
}
.question_container .username span {
  font-style: italic;
}
.question_container .question {
  font-weight: bold;
  word-wrap: anywhere;
}
.question_container .question a {
  color: initial;
}
.question_container .question a:hover {
  text-decoration: none;
  background-color: transparent;
}
.question_container .tags {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
  flex-wrap: wrap;
}
.question_container .tags li {
  color: var(--vt-c-white-mute);
  background: var(--vt-c-indigo);
  padding: .2rem .4rem;
  border-radius: 1000px;
  font-size: .75rem;
  margin-top: .5rem;
}
.question_container .tags li:not(:last-of-type) {
  margin-right: .5rem;
}
</style>