<!--<template>-->

<!--  <input type="file" id="fileInput" />-->
<!--  <button onclick="uploadFile()">上传文件</button>-->
<!--</template>-->
<template>
  <div>
    <input type="file" @change="handleFileChange" />
    <button @click="uploadFile">上传文件</button>
  </div>
</template>

<script>
import ObsClient from "esdk-obs-browserjs/src/obs";

export default {
  name: 'FileUpload',
  data() {
    return {
      selectedFile: null,
      obsClient: null
    };
  },
  mounted() {
    this.obsClient = new ObsClient({
      access_key_id: "4KRYQPZF013ZRMNNXVQT", // 你的ak
      secret_access_key: "yyKzh0mmJxgxtWDjuPa86rdPDPCs3KbfYK04BuE5", // 你的sk
      server: "https://obs.cn-north-4.myhuaweicloud.com", // 你的endPoint  记得加入https://
    });
  },
  methods: {
    handleFileChange(e) {
      this.selectedFile = e.target.files[0];
    },
    uploadFile() {
      if (!this.selectedFile) {
        alert('请选择一个文件');
        return;
      }

      this.obsClient.putObject({
        Bucket: 'test-micro',
        Key: this.selectedFile.name,
        Body: this.selectedFile
      }, (err, result) => {
        if (err) {
          console.error('Error-->' + err);
        } else {
          console.log('Status-->' + result.CommonMsg.Status);
        }
      });
    }
  }
};
</script>

<style>
/* 你的样式 */
</style>

<!--<script>-->
<!--import { uuid } from "vue-uuid";-->
<!--import ObsClient from "esdk-obs-browserjs/src/obs";-->
<!--var obsClient = new ObsClient({-->
<!--  access_key_id: "4KRYQPZF013ZRMNNXVQT", // 你的ak-->
<!--  secret_access_key: "yyKzh0mmJxgxtWDjuPa86rdPDPCs3KbfYK04BuE5", // 你的sk-->
<!--  server: "https://obs.cn-north-4.myhuaweicloud.com", // 你的endPoint  记得加入https://-->
<!--});-->
<!--function uploadFile(){-->
<!--  var fileInput = document.getElementById('fileInput');-->
<!--  var file = fileInput.files[0];-->
<!--  console.log("开始上传");-->

<!--obsClient.putObject({-->
<!--  Bucket : 'test-micro',-->
<!--  Key: file.name,-->
<!--  Body: file-->
<!--      // 'Hello OBS'-->
<!--}, function (err, result) {-->
<!--  if(err){-->
<!--    console.error('Error&ndash;&gt;' + err);-->
<!--  }else{-->
<!--    console.log('Status&ndash;&gt;' + result.CommonMsg.Status);-->
<!--  }-->
<!--});}-->


<!--      // obsClient.putObject({-->
<!--      //   Bucket : 'test-micro',-->
<!--      //   Key : '123',-->
<!--      //   SourceFile : this.file-->
<!--      // }, function (err, result) {-->
<!--      //   if(err){-->
<!--      //     console.error('Error&ndash;&gt;' + err);-->
<!--      //   }else{-->
<!--      //     console.log('Status&ndash;&gt;' + result.CommonMsg.Status);-->
<!--      //   }-->
<!--      // });-->

<!--</script>-->

<!--<style scoped lang="scss">-->
<!--.upload-file-uploader {-->
<!--  margin-bottom: 5px;-->
<!--}-->
<!--.upload-file-list .el-upload-list__item {-->
<!--  border: 1px solid #fff666;-->
<!--  line-height: 2;-->
<!--  margin-bottom: 10px;-->
<!--  position: relative;-->
<!--}-->
<!--.upload-file-list .ele-upload-list__item-content {-->
<!--  display: flex;-->
<!--  justify-content: space-between;-->
<!--  align-items: center;-->
<!--  color: inherit;-->
<!--}-->
<!--.ele-upload-list__item-content-action .el-link {-->
<!--  margin-right: 10px;-->
<!--}-->
<!--</style>-->
