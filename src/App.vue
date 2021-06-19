<template>
  <div id="app">
    <div class="center examplex">
      <vs-navbar center-collapsed fixed v-model="active" class="navigation">
        <template #left>
          <img src="/logo2.png" alt="" />
        </template>
        <vs-navbar-item
          class="navigation_item"
          :active="active == 'music'"
          id="music"
        >
          <router-link class="router_link" to="/music">Музыка</router-link>
        </vs-navbar-item>
        <vs-navbar-item
          class="navigation_item"
          :active="active == 'podcasts'"
          id="podcasts"
        >
          <router-link class="router_link" to="/podcasts">Подкасты</router-link>
        </vs-navbar-item>
        <vs-navbar-item
          class="navigation_item"
          :active="active == 'books'"
          id="books"
        >
          <router-link class="router_link" to="/books">Аудиокниги</router-link>
        </vs-navbar-item>
        <vs-navbar-item
          class="navigation_item"
          :active="active == 'video'"
          id="video"
        >
          <router-link class="router_link" to="/movies">Видео</router-link>
        </vs-navbar-item>
        <vs-navbar-item
          class="navigation_item"
          :active="active == 'cinema'"
          id="cinema"
        >
          <router-link class="router_link" to="/cinema">Кино</router-link>
        </vs-navbar-item>
        <vs-navbar-item
          class="navigation_item"
          :active="active == 'series'"
          id="series"
        >
          <router-link class="router_link" to="/series">Сериалы</router-link>
        </vs-navbar-item>
        <template #right>
          <vs-navbar-group>
            <vs-avatar
              badge-color="danger"
              size="64"
              badge
              badge-position="top-right"
            >
              <img
                src="https://static.independent.co.uk/s3fs-public/thumbnails/image/2020/05/01/08/avatar-sigourney-weaver.jpg?width=1200&auto=webp&quality=75"
                alt=""
              />
              <template #badge> 28 </template>
            </vs-avatar>

            <template #items class="hello">
              <h5 class="title">Юзернейм</h5>
              <vs-navbar-item :active="active == 'favorite'" id="favorite">
                Избранное
              </vs-navbar-item>
              <vs-navbar-item :active="active == 'logout'" id="logout">
                Выход
              </vs-navbar-item>
            </template>
          </vs-navbar-group>
        </template>
      </vs-navbar>
      <div class="page_container">
        <router-view />
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "App",
  data() {
    return {
      active: "home",
      activeSidebar: false,
    };
  },
};
</script>
<style lang="stylus">
body {
  overflow-x: hidden;
  overflow-y: auto;
}

.vs-navbar__group__items {
  margin-left: -4em;
}

.vs-navbar__group__items {
  .vs-navbar__item {
    padding: 1em;
  }
}

*::-webkit-scrollbar {
  display: none;
}

.router_link {
  text-decoration: none;
  color: inherit;
}

.navigation_item {
  padding: 2em 2em;
}

.page_container {
  margin-top: 8em;
  padding: 0 4em;
  max-height: 100vh;
  max-width: 100vw;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
