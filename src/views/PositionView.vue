<template>
  <el-card class="box-card">
    <el-input
        v-model="searchText"
        placeholder="搜索成员..."
        class="search-input"
    >
      <template #append>
        <el-button icon="el-icon-search" @click="searchMembers">搜索</el-button>
      </template>
    </el-input>

    <el-table :data="filteredMembers" style="width: 100%">
      <el-table-column prop="name" label="成员姓名"></el-table-column>
      <el-table-column label="操作">
        <template #default="scope">
          <el-button size="mini" @click="goToChat(scope.row)">发送消息</el-button>
          <el-popover
              placement="top"
              width="200"
              trigger="click"
              v-model:visible="scope.row.popoverVisible"
          >
            <p><img :src="scope.row.avatar || defaultAvatar" alt="头像" style="width: 100%; height: auto;"></p>
            <p>ID: {{ scope.row.id }}</p>
            <p>电话: {{ scope.row.phone || '暂无' }}</p>
            <p>邮箱: {{ scope.row.email || '暂无' }}</p>
            <el-button size="mini" @click="scope.row.popoverVisible = false">关闭</el-button>
            <template #reference>
              <el-button size="mini" @click="fetchMemberDetails(scope.row)">查看详情</el-button>
            </template>
          </el-popover>
          <el-switch
              v-model="scope.row.isAdmin"
              active-text="管理员"
              inactive-text="非管理员"
              @change="updateAdminStatus(scope.row)"
          ></el-switch>
        </template>
      </el-table-column>
    </el-table>
  </el-card>
</template>

<script>
import axios from 'axios';
import { ref, computed, onMounted } from 'vue';
import { useRouter } from 'vue-router';

export default {
  name: 'ProjectMemberList',
  setup() {
    const defaultAvatar = 'path/to/default/avatar.jpg'; // 更换为默认头像的路径
    const members = ref([
      { name: '项目成员1', id: 1, popoverVisible: false },
      { name: '项目成员2', id: 2, popoverVisible: false },
      { name: '项目成员3', id: 3, popoverVisible: false },
      // ...更多默认成员
    ]);
    const searchText = ref('');
    const router = useRouter();

    onMounted(() => {
      fetchMembers();
    });

    const fetchMembers = async () => {
      try {
        const response = await axios.get('http://localhost:8091/projectMember?projectId=1');
        members.value = response.data.map(member => ({
          ...member,
          popoverVisible: false,
        }));
      } catch (error) {
        console.error('Error fetching members:', error);
        // 处理错误情况
      }
    };

    const fetchMemberDetails = async (member) => {
      try {
        const response = await axios.get(`http://localhost:8091/memberDetails?id=${member.id}`);
        Object.assign(member, response.data);
      } catch (error) {
        console.error('Error fetching member details:', error);
        // 处理错误情况
      }
    };

    const filteredMembers = computed(() => {
      if (!searchText.value) return members.value;
      return members.value.filter((member) =>
          member.name.toLowerCase().includes(searchText.value.toLowerCase())
      );
    });

    const goToChat = (member) => {
      console.log(`跳转到与 ${member.name} 的聊天界面`);
      router.push('/home/chat');
      // 根据需要，可以传递成员的ID或其他数据到聊天界面
    };

    const searchMembers = () => {
      console.log(`搜索: ${searchText.value}`);
      // 这里可以添加更多的搜索逻辑
    };
    const updateAdminStatus = async (member) => {
      try {
        const response = await axios.post(`http://localhost:8091/updateAdminStatus`, {
          memberId: member.id,
          isAdmin: member.isAdmin
        });
        console.log(response.data); // 可以根据需要处理响应
      } catch (error) {
        console.error('Error updating admin status:', error);
        // 处理错误情况
      }
    };
    return { members, searchText, filteredMembers, goToChat, fetchMemberDetails, defaultAvatar ,updateAdminStatus};

  },
};
</script>

<style scoped>
.search-input {
  margin-bottom: 20px;
}
</style>
