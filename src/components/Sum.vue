<template>
  <div style="width: 80%; margin-left: 20px"> 
    <H1>累加和</H1>
    <el-input v-model="arrStr" style= "margin-top: 20px"  placeholder="请输入内容"></el-input>
    <el-button @click="decClick()" style= "margin-top: 20px">转换</el-button>
    <el-tabs v-model="activeName" @tab-click="handleClick">
      <el-tab-pane label="按字" name="first">
        <div>
       <span> 十进制和(按字):</span>
        <el-input v-model="decSum4"  placeholder="请输入内容"></el-input>
        </div>

        十六进制和(按字):
        <el-input v-model="hexSum4" placeholder="请输入内容"></el-input>
      </el-tab-pane>
      <el-tab-pane label="按字节" name="second">
        十进制和(按字节):
        <el-input v-model="decSum" placeholder="请输入内容"></el-input>
        十六进制和(按字节):
        <el-input v-model="hexSum" placeholder="请输入内容"></el-input>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
export default {
  name: "Sum",
  data() {
    return {
      activeName: 'second',
      arrStr: "",
      decSum: "",
      decSum4: "",
    };
  },
  computed: {
    hexSum() {
      var str = this.decSum.toString(16);
      return str.substring(str.length - 2);
    },
    hexSum4() {
      var str = this.decSum4.toString(16);
      return str.substring(str.length - 2);
    },
  },
  methods: {
    decClick() {
      if (this.arrStr != "") {
        var sum = 0;
        var sum4 = 0;
        for (let i = 0; i < this.arrStr.length; i += 2) {
          sum += parseInt(this.arrStr.substr(i, 2), 16);
        }
        this.decSum = sum;
        for (let i = 0; i < this.arrStr.length; i += 4) {
          sum4 += parseInt(this.arrStr.substr(i, 4), 16);
        }
        this.decSum4 = sum4;
      }
    },
  },
};
</script>

<style>
</style>