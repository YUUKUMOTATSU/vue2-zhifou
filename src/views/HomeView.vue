<template>
  <v-app>
    <!-- 应用栏区域 -->
    <v-app-bar app
      color="#FFFFFF"
    >
      <!-- 应用栏菜单选项 -->
      <v-container fluid>
        <v-tabs
          slider-size="5"
          centered
        >
          <v-tab 
            v-for="tab in tabMenus"
            :key="tab.id"
            :to="tab.href"
          >
            {{ tab.name }}
          </v-tab>
        </v-tabs>
        <!-- 登陆按钮 -->
        <v-btn
          absolute
          right
          top
          text
          class="mr-16"
        >
          登陆
        </v-btn>
      </v-container>
    </v-app-bar>
    <v-main>
      <v-parallax
        height="600"
        src="https://cdn.vuetifyjs.com/images/parallax/material.jpg"
      >
        <div class="text-center">
          <h1 class="text-h2 font-weight-black mb-3">知否</h1>
          <p>为您打造全方位的影音，博学，教学，考证网站</p>
        </div>
      </v-parallax>
      <v-container
        class="text-center"
      >
        <h1 class="text-h2 font-weight-black mb-2">共享盛宴</h1>
        <p>知否为您打造全方位的影音，博学，教学，考证网站</p>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'Home',
  data: () => ({
    tabMenus: [], //应用栏菜单
    homeBackPic: '', // 首页背景图
  }),
  created() {
    // 获取应用栏菜单
    this.getAppBarMenus()
    this.getHomeBackPic()
  },
  methods: {
    // 获取首页的背景图
    getHomeBackPic() {
      // 请求服务器 -- 获取 -- 获取首页的背景图地址
      this.homeBackPic = 'https://pic3.zhimg.com/v2-fbb002ec83393f1b87a55cfb69c864db_r.jpg'
    },
    // 获取应用栏菜单
    getAppBarMenus() {
      // 请求服务器 -- 获取 -- 获取应用栏菜单
      this.tabMenus = [
        { id: 1, name: '首页', href: '/'},
        { id: 2, name: '博客', href: '/blog'},
        { id: 3, name: '学堂', href: '/school'},
        { id: 4, name: '影音', href: '/film'},
        { id: 5, name: '考证', href: '/exam'},
      ]
    }
  },
}
</script>