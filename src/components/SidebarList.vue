<script>
export default {
  data() { 
    return {
      feeds: [{'id': 1, 'name': 'item 1', 'icon': 'list'}, {'id': 2, 'name': 'item 2', 'icon': 'list-check'}]
    }
  }
}
</script>

<template>
  <ul>
    <li v-for="item in feeds">
      <font-awesome-icon :icon='["fas", item.icon]' class="icon" />
      <span style="display: none">{{ item.name }}</span>
    </li>
  </ul>

  <button class="add_feed">+</button>
</template>

<style scoped>
ul {
  padding: 0 0 .5rem 0;
  margin: 0 .65rem;
  margin-bottom: 1rem;
  border-bottom: 1px solid #000;
}
ul li {
  display: flex;
  list-style: none;
  justify-content: center;
  padding: .5rem 0;
}
ul li:hover {
  color: var(--vt-c-white);
}
ul li .icon {
  font-size: 1rem;
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
</style>