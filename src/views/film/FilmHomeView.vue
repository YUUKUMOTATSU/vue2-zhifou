<template>
    <v-app>
        <!-- 应用栏区域 -->
        <v-app-bar app
            color="#FFFFFF"
        >
            <head-bar></head-bar>
        </v-app-bar>
        <v-main>
            影音首页界面
        </v-main>
        <!-- 网站页脚 -->
        <v-footer app>
            <footer-bar></footer-bar>
        </v-footer>
    </v-app>
</template>

<script>

export default {
    name: 'ExamHomeView',
}
</script>