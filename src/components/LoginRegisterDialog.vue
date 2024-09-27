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
                <v-btn
                    absolute
                    fab
                    small
                    light
                    style="top: 10px;right: -20px;"
                    @click="dialogIsShow()"
                >
                    <v-icon color="grey" size="30">mdi-close-circle-outline</v-icon>
                </v-btn>
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
                        class="pa-16 d-flex flex-column"
                    >
                        <!--  标题 -->
                        <v-container class="d-flex align-center">
                            <h2>登陆</h2>
                            <span class="text-caption ml-auto">
                                没有账号？
                                <a class="text-decoration-none" @click="step = 2">点击注册</a>
                            </span>
                        </v-container>
                        <!-- 登陆区域 -->
                        <v-container>
                            <!-- 登陆表单 -->
                            <v-form
                                lazy-validation
                                v-model="login.value"
                                ref="login_form"
                            >
                                <!-- 账号文本框 -->
                                <v-text-field
                                    outlined
                                    dense
                                    :rules="login.account.rule"
                                    v-model="login.account.value"
                                    label="账号 / 邮箱 / 手机号"
                                    placeholder="账号 / 邮箱 / 手机号"
                                >
                                </v-text-field>
                                <!-- 密码输入框 -->
                                <v-text-field
                                    outlined
                                    dense
                                    :rules="login.password.rule"
                                    v-model="login.password.value"
                                    label="密码"
                                    placeholder="请输入账号密码"
                                    :type="login.password.showPW ? 'text' : 'password'"
                                    :append-icon="login.password.showPW ? 'mdi-eye-off' : 'mdi-eye'"
                                    @click:append="login.password.showPW = !login.password.showPW"
                                >
                                </v-text-field>
                                <!-- 条款和协议 -->
                                <v-checkbox
                                    dense
                                    :rules="login.tarm.rule"
                                    v-model="login.tarm.value"
                                    class="mt-0 mb-2"
                                >
                                    <!-- 标签插槽 -->
                                    <template #label>
                                        同意本公司的
                                        <a
                                            target="_blank"
                                            class="text-decoration-none"
                                            href="https://www.google.com/"
                                            @click.stop
                                        >
                                            条款与协议
                                        </a>
                                    </template>
                                </v-checkbox>
                                <!-- 登陆按钮 -->
                                <v-btn
                                    block
                                    color="success"
                                    :disabled="!login.value"
                                    @click="tologin"
                                >
                                    登陆
                                </v-btn>
                            </v-form>
                            <!-- 忘记密码 -->
                            <v-container class="text-center">
                                <a class="text-caption grey--text text-decoration-none" href="">忘记密码</a>
                            </v-container>
                        </v-container>
                        <!-- 其他登陆方式 -->
                        <v-container class="mt-auto">
                            <!-- 分隔符 -->
                            <v-container class="d-flex align-center py-0">
                                <v-divider></v-divider>
                                <v-subheader class="text-caption">其他登陆方式</v-subheader>
                                <v-divider></v-divider>
                            </v-container>
                            <!-- 图标 -->
                            <v-container class="d-flex justify-center py-0">
                                <v-btn
                                    fab
                                    small
                                    :color="i.color"
                                    v-for="i in otherMethods"
                                    :key="i.id"
                                    :to="i.to"
                                    :class="{'mx-2': (index !== 0)}"
                                >
                                    <v-icon>{{ i.icon }}</v-icon>
                                </v-btn>
                            </v-container>
                        </v-container>
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
        footerLinks: [], // 脚部链接
        login: {
            value: false,
            account: {
                value: '',
                rule: [
                    v => !!v || '请填写您的账号信息'
                ]
            },
            password: {
                value: '',
                showPW: false,
                rule: [
                    v => !!v || '请填写您的密码'
                ]
            },
            tarm: {
                value: false,
                rule: [
                    v => !!v || '请认真阅读条款协议'
                ]
            },
        },
        otherMethods: [],
    }),
    created() {
        // 获取脚部链接
        this.getFooterLinks()
        // 获取其他登陆方式数据
        this.getOtherLoginMethods()
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
        // 获取其他的登陆方式
        getOtherLoginMethods() {
            // 请求服务器 -- 获取其他的登陆方式
            this.otherMethods = [
                { id: 1, name: 'QQ', icon: 'mdi-qqchat', color: 'info', to: '' },
                { id: 2, name: '微信', icon: 'mdi-wechat', color: 'success', to: '' },
                { id: 3, name: '微博', icon: 'mdi-sina-weibo', color: 'error', to: '' }
            ]
        },
        // 登陆
        tologin() {
            // 手动验证表单的状态
            let isSuccess = this.$refs.login_form.validate()
            if (!isSuccess) {
                return
            } else {
                // 请求服务器 -- 登陆
                alert("验证成功，请求服务器进行登陆")
            }
        },
        // 展示密码
        showPW() {
            if (this.login.password.type == 'password') {
                this.login.password.type == 'text'
            }
        },
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
        },
        // 打开关闭对话框
        dialogIsShow() {
            this.show = !this.show
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