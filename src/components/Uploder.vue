<template>
  <div class="uploader">
    <p class="title">{{ title }}</p>
    <el-upload
      class="upload-demo"
      action="#"
      :http-request="upload"
      :on-preview="handlePreview"
      :on-remove="handleRemove"
      :before-remove="beforeRemove"
      multiple
      :limit="3"
      :on-exceed="handleExceed"
      :file-list="fileList"
      list-type="picture"
    >
      <el-button size="small" type="primary">選擇檔案</el-button>
      <div slot="tip" class="el-upload__tip">
        {{ msg }}
      </div>
    </el-upload>
  </div>
</template>

<script>
export default {
  name: 'Uploder',
  props: {
    limit: {
      type: Number,
      required: true
    },
    title: {
      type: String
    },
    msg: {
      type: String,
      default: '只能上傳jpg / png檔案且不超過500KB'
    },
    postUrl: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      fileList: []
    }
  },
  methods: {
    upload(param) {
      const formData = new FormData()
      let imgUrl = ''
      formData.append('image', param.file)
      formData.append('key', '058749e7e07d5a37482b895931d4a099')
      this.$http
        .post('https://api.imgbb.com/1/upload', formData)
        .then(function (res) {
          imgUrl = res.data?.data.display_url
          this.postToDatabase(imgUrl)
        })
        .catch(function (error) {
          alert('抓取資料錯誤，請確認後再試')
          console.log(error)
        })
    },
    postToDatabase(imgUrl) {
      this.$http
        .post('http://localhost:3000/productImg', { url: imgUrl })
        .then(function (res) {
          console.log(res.data)
        })
        .catch(function (error) {
          alert('抓取資料錯誤，請確認後再試')
          console.log(error)
        })
    },
    handleRemove(file, fileList) {
      console.log(file, fileList)
    },
    handlePreview(file) {
      console.log(file)
    },
    handleExceed(files, fileList) {
      this.$message.warning(
        `当前限制选择 ${this.limit} 个文件，本次选择了 ${
          files.length
        } 个文件，共选择了 ${files.length + fileList.length} 个文件`
      )
    },
    beforeRemove(file) {
      return this.$confirm(`确定移除 ${file.name}？`)
    }
  }
}
</script>

<style scoped lang="scss">
.title {
  color: #000;
}
</style>
