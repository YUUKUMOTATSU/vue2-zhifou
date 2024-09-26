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
                tile
                width="500"
                height="573"
            >
                1
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
        step: 1
    }),
}
</script>
<style scoped>
    
</style>