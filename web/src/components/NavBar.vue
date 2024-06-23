<template>
  <nav class="navbar navbar-expand-lg bg-body-tertiary">
    <div class="container bak">
      <router-link
        class="navbar-brand"
        :to="{ name: 'home' }"
        style="font-weight: bold; font-style: italic"
        >Simple gluttonous snake的相关说明和介绍</router-link
      >
      <div
        class="collapse navbar-collapse bak"
        id="navbarText"
        style="font-size: 19px"
      >
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item" style="font-weight: 510; font-style: italic">
            <router-link
              :class="route_name == 'pk_index' ? 'nav-link active' : 'nav-link'"
              :to="{ name: 'pk_index' }"
              >对战</router-link
            >
          </li>
          <li class="nav-item" style="font-weight: 510; font-style: italic">
            <router-link
              :class="
                route_name == 'record_index' ? 'nav-link active' : 'nav-link'
              "
              :to="{ name: 'record_index' }"
              >对局列表</router-link
            >
          </li>
          <li class="nav-item" style="font-weight: 510; font-style: italic">
            <router-link
              :class="
                route_name == 'ranklist_index' ? 'nav-link active' : 'nav-link'
              "
              :to="{ name: 'ranklist_index' }"
              >排行榜</router-link
            >
          </li>
        </ul>
        <form class="d-flex" role="search">
          <input
            class="form-control me-2"
            type="search"
            placeholder="Search"
            aria-label="Search"
          />
          <button class="btn btn-outline-success" type="submit">Search</button>
        </form>
        <ul class="navbar-nav" v-if="$store.state.user.is_login">
          <li class="nav-item dropdown">
            <a
              class="nav-link dropdown-toggle"
              href="#"
              id="navbarDropdown"
              role="button"
              data-bs-toggle="dropdown"
              aria-expanded="false"
            >
              {{ $store.state.user.username }}
            </a>
            <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
              <li>
                <router-link
                  class="dropdown-item"
                  :to="{ name: 'user_bot_index' }"
                  >我的Bot</router-link
                >
              </li>
              <li><hr class="dropdown-divider" /></li>
              <li>
                <a class="dropdown-item" href="#" @click="logout">退出</a>
              </li>
            </ul>
          </li>
        </ul>
        <ul class="navbar-nav" v-else>
          <router-link
            class="nav-link"
            :to="{ name: 'user_account_login' }"
            role="button"
          >
            登录
          </router-link>
          <router-link
            class="nav-link"
            :to="{ name: 'user_account_register' }"
            role="button"
          >
            注册
          </router-link>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import { useRoute } from "vue-router";
import { computed } from "vue";
import { useStore } from "vuex";

export default {
  setup() {
    const store = useStore();
    const route = useRoute();
    let route_name = computed(() => route.name);
    const logout = () => {
      store.dispatch("logout");
    };
    return {
      route_name,
      logout,
    };
  },
};
</script>

<style scoped>
div.bak {
  background-color: aliceblue;
}
</style>
