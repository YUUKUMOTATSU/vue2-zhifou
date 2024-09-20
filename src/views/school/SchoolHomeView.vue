<template>
    <v-app>
        <!-- 应用栏区域 -->
        <v-app-bar app
            color="#FFFFFF"
        >
            <head-bar></head-bar>
        </v-app-bar>
        <v-main>
            <v-container fluid class="d-flex justify-center">
                <!-- 课程菜单 -->
                 <v-card>
                    <v-toolbar
                        color="blue"
                        dark
                        dense
                    >
                        <v-spacer></v-spacer>
                        热门课程
                        <v-spacer></v-spacer>
                    </v-toolbar>
                    <v-card-text>
                        <v-list dense>
                            <v-list-item-group color="blue" v-model="subValue">
                                <v-list-item v-for="subject in subMenus" :key="subject.id" :value="subject.id">
                                    {{ subject.name }}
                                </v-list-item>
                            </v-list-item-group>
                        </v-list>
                    </v-card-text>
                 </v-card>
                <!-- 课程阶段 -->
                 <v-card width="850" class="ml-8">1</v-card>
            </v-container>
        </v-main>
        <!-- 网站页脚 -->
        <v-footer app>
            <footer-bar></footer-bar>
        </v-footer>
    </v-app>
</template>

<script>

export default {
    name: 'SchoolHomeView',
    data: () => ({
        subMenus: [], // 课程菜单
        subValue: null, // 课堂菜单值
    }),
    created() {
        this.getSubjectMenus()
    },
    methods: {
        // 获取课程菜单
        getSubjectMenus() {
            this.subMenus = [
                { id: 1, name: 'JavaEE' },
                { id: 2, name: 'HTML&JS+前端' },
                { id: 3, name: 'Python+大数据开发' },
                { id: 4, name: '人工智能开发' },
                { id: 5, name: 'UI/UE设计' },
                { id: 6, name: '软件测试' }
            ]
        }
    },
}
</script>