<template>
    <!-- 对话框 -->
    <v-dialog
        persistent
        width="1000"
        v-model="show"
        content-class="rounded-0"
    >
        <div class="d-flex">
            <!-- 网站信息 -->
            <v-card
                dark
                tile
                width="500"
                height="573"
                class="dialog_back pa-16 d-flex flex-column"
            >
                <!-- 网站标题 -->
                <v-container class="mb-auto">
                    <h1>ZHIFOU</h1>
                    <p class="text-caption text--lighten-2">全方位的教学 考证 博客 资讯网站</p>
                </v-container>
                <!-- 推荐博主 -->
                <v-container class="mb-auto">
                    <!-- 头像 名称 -->
                    <div>
                        <v-avatar size="40">
                            <v-img :src="recAutoor.head_pic"></v-img>
                        </v-avatar>
                        <span class="text-caption ml-2">{{ recAutoor.nickname }}</span>
                    </div>
                    <!-- 个性签名 -->
                    <p class="text-caption text--lighten-2 mt-2" v-html="recAutoor.canvases"></p>
                </v-container>
                <!-- 网站咨询标签 -->
                <v-container class="text-center">
                    <v-chip
                        label
                        small
                        link
                        color="transparent"
                        text-color="grey lighten-2"
                        v-for="link in footerLinks"
                        :key="link.id"
                        :to="link.to"
                    >
                        {{ link.name }}
                    </v-chip>
                </v-container>
            </v-card>
            <!-- 窗口（登陆 注册 注册成功） -->
            <v-window v-model="step">
                <v-window-item :value="1">
                    <v-card
                        tile
                        width="500"
                        height="573"
                    >
                        登陆
                    </v-card>
                </v-window-item>
                <v-window-item :value="2">
                    <v-card
                        tile    
                        width="500"
                        height="573"
                    >
                        注册
                    </v-card>
                </v-window-item>
                <v-window-item :value="3">
                    <v-card
                        tile
                        width="500"
                        height="573"
                    >
                        注册成功
                    </v-card>
                </v-window-item>
            </v-window>
        </div>
    </v-dialog>
</template>
<script>
export default {
    name: 'LoginRegisterDialog',
    data: () => ({
        show: true, // 显示隐藏对话框
        step: 1,
        recAutoor: {}, // 推荐博主
        footerLinks: [] // 脚部链接
    }),
    created() {
        this.getFooterLinks()
    },
    watch: {
        show: {
            immediate: true, // 初次实力化后
            handler(newData) {
                // 获取推荐的博主
                this.getRecommendAuthor()
            }
        }
    },
    methods: {
        // 获取脚步链接
        getFooterLinks() {
            // 请求服务器 -- 获取脚部的链接
            this.footerLinks = [
                { id: 1, name: '知否咨询', to: '' },
                { id: 2, name: '关于我们', to: '' },
                { id: 3, name: '使用条款', to: '' },
                { id: 4, name: '帮助文档', to: '' },
            ]
        },
        // 获取推荐的博主
        getRecommendAuthor() {
            // 请求服务器 -- 获取推荐的博主
            this.recAutoor = {
                head_pic: 'https://cdn.vuetifyjs.com/images/john.jpg', // 头像
                nickname: '落叶归根', // 昵称
                canvases:
                '编程是爱好，恭喜你发现宝藏男孩一枚~希望你们关注我是因为喜欢我，嘿嘿！<br>' +
                '私人微信：kuangshenya 备注来意<br>' +
                '公众号：狂神说' // 个性签名
            }
        }
    }
}
</script>
<style scoped>
    /* 对话框背景色 */
    .dialog_back {
        background-image: linear-gradient(to bottom, #3a485a, #607089);
    }
</style>