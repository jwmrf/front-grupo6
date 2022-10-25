<script>
import FeedContainerVue from './components/FeedContainer.vue';
import SidebarListVue from './components/SidebarList.vue';
export default {
  name: "App",
  components: {
    FeedContainerVue,
    SidebarListVue,
  },
  data() {
    return {
      feeds: []
    }
  },
  methods: {
    addFeed() {
      this.feeds.push({'id': 1, 'name': 'android', 'icon': 'list'})
    }
  }
}
</script>

<template>
  <header>
    <img
      alt="Vue logo"
      class="logo"
      src="@/assets/logo.svg"
      width="30"
      height="30"
    />

    <div class="wrapper">
      <SidebarListVue @addfeed="addFeed" />
    </div>
  </header>

  <FeedContainerVue :feeds="feeds"/>
</template>

<style scoped>
header {
  height: 100vh;
  display: flex;
  flex-direction: column;
  background: var(--vt-c-black-mute);
  width: 60px;
  padding: 1rem 0;
}

header .wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin-top: 1rem;
}

.logo {
  display: block;
  margin: 0 auto;
}
</style>
