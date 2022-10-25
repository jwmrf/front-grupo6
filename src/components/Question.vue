<script>
import moment from 'moment'

export default {
  created: function () {
    this.moment = moment
  },
  mounted() {
  },
  props: {
    question : {}
  }
}
</script>

<template>
  <div class="question_container">
    <img class="avatar" src="https://www.gravatar.com/avatar/975b7da3f157788aa827cf1c6b23a4cd?s=256&d=identicon&r=PG" />
    <div class="content">
      <span class="username">
        {{question.owner.display_name}}
        <span>{{moment.unix(1666675010).fromNow()}}</span>
      </span>
      <p class="question">{{question.title}}</p>
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
  margin-bottom: .5rem;
}
.question_container .tags {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}
.question_container .tags li {
  color: var(--vt-c-white-mute);
  background: var(--vt-c-indigo);
  padding: .2rem .4rem;
  border-radius: 20%/50%;
  font-size: .75rem;
}
.question_container .tags li:not(:last-of-type) {
  margin-right: .5rem;
}
</style>