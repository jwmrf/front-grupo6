<script>
export default {
  data() { 
    return {
      feeds: [{'id': 1, 'name': 'item 1', 'icon': 'list'}, {'id': 2, 'name': 'item 2', 'icon': 'list-check'}]
    }
  },
  methods: {
    addFeed() {
      this.feeds.push({'id': 1, 'name': 'item 1', 'icon': 'list'})
      this.$emit("addfeed", "")
      console.log(2)
    }
  }
}
</script>

<template>
  <ul class="icons_list">
    <li v-for="item in feeds" :key="item">
      <font-awesome-icon :icon='["fas", item.icon]' class="icon" />

      <span class="label">{{ item.name }}</span>
    </li>
  </ul>

  <button class="add_feed" @click="addFeed()">
    +

    <span class="label">Adicionar feed</span>
  </button>
</template>

<style scoped>
ul.icons_list {
  padding: 0 0 .5rem 0;
  margin: 0 .65rem;
  margin-bottom: 1rem;
  border-bottom: 1px solid #000;
}
ul.icons_list li {
  display: flex;
  list-style: none;
  justify-content: center;
  padding: .5rem 0;
  position: relative;
}
ul.icons_list li:hover {
  color: var(--vt-c-white);
}
ul.icons_list li .icon {
  font-size: 1rem;
}
ul.icons_list li .label, .add_feed .label {
  position: absolute;
  left: 110%;
  top: 0;
  background: var(--vt-c-black-mute);
  color: var(--color-text);
  white-space: nowrap;
  z-index: 9;
  padding: .5rem 1.5rem .5rem 1rem;
  display: none;
}
ul.icons_list li:hover .label, .add_feed:hover .label {
  display: initial;
}

.add_feed {
  background: transparent;
  color: var(--color-text);
  font-size: 2rem;
  line-height: 1rem;
  cursor: pointer;
  border: none;
}
.add_feed:hover {
  color: var(--vt-c-white);
}
.add_feed .label {
  font-size: 1rem;
  line-height: initial;
  left: 100%;
  top: -40%;
}
</style>