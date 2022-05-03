<template>
  <v-app>
    <v-app-bar
      app
      color=""
      style="
        background: linear-gradient(
          to right,
          rgba(89, 89, 91, 1),
          rgba(5, 26, 31, 1)
        );
      "
      dark
    >
      <img class="mr-16 logo" alt="logo" src="/logo.png" width="125em" />
      <!-- <v-avatar color="" size="32"></v-avatar> -->
      <v-tabs color="white">
        <v-tab v-for="(item, i) in items" :key="i" :to="item.to" router>
          <v-icon small>{{ item.icon }}</v-icon>
          <p>&nbsp;&nbsp;</p>
          {{ item.title }}
        </v-tab>
      </v-tabs>
      <!-- <h4 class="subtitle">{{ $auth.user.name }}</h4> -->
      <v-btn
        icon
        class="ml-2 mr-1"
        :loading="loading"
        :disabled="loading"
        color="#9BA3A5"
        small
        @click="$auth.logout()"
      >
        <v-icon small>mdi-logout</v-icon>
      </v-btn>
      <!-- <v-avatar
        class="hidden-sm-and-down"
        color="grey darken-1 shrink"
        size="32"
      ></v-avatar> -->
    </v-app-bar>
    <v-main>
      <Nuxt />
    </v-main>
  </v-app>
</template>
<script>
export default {
  name: "DefaultLayout",
  data() {
    return {
      loader: null,
      loading: false,
      items: [
        {
          // icon: 'mdi-tablet',
          title: "即時監測",
          to: "/",
        },
        {
          // icon: 'mdi-google-analytics',
          title: "即時監測V2",
          to: "test2",
        },
        {
          // icon: 'mdi-clipboard-text-clock',
          title: "即時監測V3",
          to: "test3",
        },
                {
          // icon: 'mdi-clipboard-text-clock',
          title: "即時監測V3雙布料",
          to: "test4",
        },
                        {
          // icon: 'mdi-clipboard-text-clock',
          title: "即時監測V3濾波測試",
          to: "test5",
        },
        {
          // icon: 'mdi-clipboard-text-clock',
          title: "深度分析",
          to: "test6",
        },
        // {
        //   icon: 'mdi-chart-bubble',
        //   title: 'Inspire',
        //   to: '/inspire',
        // },
      ],
    };
  },
  // 登出
  watch: {
    loader() {
      const l = this.loader;
      this[l] = !this[l];

      setTimeout(() => (this[l] = false), 3000);

      this.loader = null;
    },
  },
};
</script>
<style scoped>
.subtitle {
  font-size: 12px;
  color: #9ba3a5;
}
.logout {
  border: #9ba3a5 2px solid;
  font-weight: 900;
}
.logo {
  margin-left: 0.8em;
}
</style>
