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
      <!-- 背景图 -->
      <v-parallax
        height="600"
        src="https://cdn.vuetifyjs.com/images/parallax/material.jpg"
      >
        <div class="text-center">
          <h1 class="text-h2 font-weight-black mb-3">知否</h1>
          <p>为您打造全方位的影音，博学，教学，考证网站</p>
        </div>
      </v-parallax>
      <!-- 标题介绍 -->
      <v-container
        class="text-center"
      >
        <h1 class="text-h2 font-weight-black mb-2">共享盛宴</h1>
        <p class="mb-0">知否为您打造全方位的影音，博学，教学，考证网站</p>
      </v-container>
      <!-- 主页卡片 -->
      <v-container fluid class="d-flex justify-center">
        <!-- 四张卡片 -->
        <v-card
          width="280"
          hover
          v-for="(card,index) in homeCards"
          :key="card.id"
          :to="card.href"
          :class="{'ml-3': (index !== 0)}"
        >
          <v-card-title>{{ card.name }}</v-card-title>
          <v-card-subtitle>{{ card.desc }}</v-card-subtitle>
          <v-card-text>
            <!-- 卡片的标签 -->
            <v-chip small lable color="transparent" v-for="lable in card.labels">{{ lable }}</v-chip>
          </v-card-text>
        </v-card>
      </v-container>
    </v-main>
    <!-- 网站页脚 -->
    <v-footer>
      <v-container fluid class="d-flex justify-center">
        <v-chip small lable color="transparent" v-for="link in footerLinks" :to="link.to">{{ link.text }}</v-chip>
      </v-container>
    </v-footer>
  </v-app>
</template>

<script>

export default {
  name: 'Home',
  data: () => ({
    tabMenus: [], //应用栏菜单
    homeBackPic: '', // 首页背景图
    homeCards: [], // 主页卡片信息
    footerLinks: [], // 页脚链接
  }),
  created() {
    // 获取应用栏菜单
    this.getAppBarMenus()
    // 获取首页的背景图
    this.getHomeBackPic()
    // 获取卡片信息
    this.getHomeCards()
    // 获取网页链接
    this.getFooterLinks()
  },
  methods: {
    // 获取首页的背景图
    getHomeBackPic() {
      // 请求服务器 -- 获取 -- 获取首页的背景图地址
      this.homeBackPic = "https://pic3.zhimg.com/v2-fbb002ec83393f1b87a55cfb69c864db_r.jpg"
    },
    // 获取应用栏菜单
    getAppBarMenus() {
      // 请求服务器 -- 获取 -- 获取应用栏菜单
      this.tabMenus = [
        { id: 1, name: "首页", href: "/"},
        { id: 2, name: "博客", href: "/blog"},
        { id: 3, name: "学堂", href: "/school"},
        { id: 4, name: "影音", href: "/film"},
        { id: 5, name: "考证", href: "/exam"},
      ]
    },
    // 获取主页的卡片信息
    getHomeCards() {
      // 请求服务器 -- 获取 -- 获取主页的卡片信息
      this.homeCards = [
        {
          id: 1,
          name: "博客",
          desc: "百万博主分享经验",
          href: "/blog",
          labels: [
            "Java",
            "Python",
            "Hadoop",
            "Liunx",
            "C++",
            "Unity",
            "UI 设计",
            "Android",
            "IOS",
            "HarmonyOs",
          ],
        },
        {
          id: 2,
          name: "学堂",
          desc: "百万教学视频畅游知识海洋",
          href: "/school",
          labels: [
            "VueJs",
            "前端",
            "后台",
            "大数据",
            "影视后期",
            "游戏开发",
            "人工智能",
            "物联网",
            "游戏建模",
            "应用开发",
          ],
        },
        {
          id: 3,
          name: "视频",
          desc: "百万影视视频畅享盛会",
          href: "/film",
          labels: [
            "电视剧",
            "电影",
            "纪录片",
            "少儿",
            "动漫",
            "短视频",
            "综艺",
            "港剧",
            "台剧",
            "韩剧",
            "恐怖片",
            "好莱坞",
          ],
        },
        {
          id: 4,
          name: "考证",
          desc: "千款认证考试线上测试",
          href: "/exam",
          labels: [
            "模拟考",
            "刷题",
            "期末考",
            "课堂考",
            "甲骨文认证",
            "华为认证",
            "三星认证",
            "TCL认证",
            "微软认证",
          ],
        },
      ]
    },
    // 获取页脚链接
    getFooterLinks() {
      // 请求服务器  -->  获取  -->  获取页脚链接
      this.footerLinks = [
        { id: 1, text: '增值电信业务经营许可证：合字B2-20090007', to: '' },
        { id: 2, text: '京ICP备10036305号-7', to: '' },
        { id: 3, text: '京公网安备11010802022657号', to: '' },
        { id: 4, text: '隐私声明和 Cookie', to: '' },
        { id: 5, text: '法律声明', to: '' },
        { id: 6, text: '广告', to: '' },
        { id: 7, text: '帮助', to: '' },
        { id: 8, text: '反馈', to: '' },
        { id: 9, text: '© 2022 Microsoft', to: '' },
      ]
    },
  },
}
</script>