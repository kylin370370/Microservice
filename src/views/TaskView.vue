<template>
  <el-card class="box-card">
    <div class="text item">项目任务数量: {{ taskCount }}</div>
    <div class="text item">项目成员人数: {{ members.length }}</div>
    <el-divider></el-divider>
    <el-button type="primary" @click="goToChat">发送消息</el-button>
  </el-card>
</template>

<script>
import { ref } from 'vue';
import { useRouter } from 'vue-router';

export default {
  name: 'ProjectManagement',
  setup() {
    // 示例数据，实际应用中应从后端或其他数据源获取
    const taskCount = ref(10); // 假设项目有10个任务
    const members = ref([
      { name: '成员1', id: 1 },
      { name: '成员2', id: 2 },
      // ...更多成员
    ]);

    const router = useRouter();

    const goToChat = () => {
      router.push('/home/chat');
    };

    return { taskCount, members, goToChat };
  },
};
</script>

<style scoped>
.text.item {
  padding: 10px 0;
}
</style>
