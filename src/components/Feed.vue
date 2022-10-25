<script setup>
import QuestionVue from './Question.vue'
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