<template>
    <!-- 视频卡片 -->
    <v-list-item>
        <!-- 视频封面 -->
        <v-list-item-avatar tile width="200" height="120">
            <v-img class="rounded-lg" :src="cover"></v-img>
        </v-list-item-avatar>
        <!-- 视频介绍 -->
        <v-list-item-content class="align-self-start">
            <!-- 标题 -->
            <v-list-item-title>{{ title }}</v-list-item-title>
            <!-- 副标题 -->
            <v-list-item-subtitle>
                <v-chip 
                    small 
                    color="success"
                    class="font-weight-black font-italic rounded-0 mr-2"
                    v-if="is_new"
                >
                    NEW
                </v-chip>
                <v-chip 
                    small 
                    color="warning"
                    class="font-weight-black font-italic rounded-0 mr-2"
                    v-if="is_hot"
                >
                    HOT
                </v-chip>
                <!-- 发布时间 -->
                <span>
                    {{ time }}
                </span>
                <!-- 介绍 -->
                <div class="text-caption grey--text text--lighten-1 line__3" v-html="desc">
                </div>
            </v-list-item-subtitle>
        </v-list-item-content>
        <!-- 学习 -->
        <v-list-item-action>
            <div class="text-center">
                <span class="text-caption grey--text text--lighten-1">{{ studyCount | numFormat }}已学</span>
                <br/>
                <v-btn block small color="info" class="rounded-pill">开始学习</v-btn>
            </div>
        </v-list-item-action>
    </v-list-item>
</template>
<script>
export default {
    name: 'SchoolVideoCardH',
    props: {
    // ID
    id: {
      type: Number,
      required: true
    },
    // 封面
    cover: {
      type: String,
      required: true
    },
    // 视频标题
    title: {
      type: String,
      required: true
    },
    // new 标签
    is_new: {
      type: Boolean,
      default: false
    },
    // hot 标签
    is_hot: {
      type: Boolean,
      default: false
    },
    // 发布时间
    time: {
      type: String,
      required: true
    },
    // 描述
    desc: {
      type: String,
      required: true
    },
    // 学习人数
    studyCount: {
      type: Number,
      required: true
    }
  }
}
</script>
<style scoped>
    .line__3 {
        display: -webkit-box;
        overflow: hidden;
        text-overflow: ellipsis;
        -webkit-line-clamp: 3;
        -webkit-box-orient: vertical;
    }
</style>