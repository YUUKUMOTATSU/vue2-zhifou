<template>
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
        <!-- 登陆对话框 -->
        <login-register-dialog></login-register-dialog>
    </v-container>
</template>

<script>
import LoginRegisterDialog from './LoginRegisterDialog.vue';

export default {
    name: 'HeadBar',
    components: {
      LoginRegisterDialog
    },
    data: () => ({
        tabMenus: [], //应用栏菜单
    }),
    created() {
        // 获取应用栏菜单
        this.getAppBarMenus()
    },
    methods: {
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
    },
}
</script>

<style scoped>
    
</style>