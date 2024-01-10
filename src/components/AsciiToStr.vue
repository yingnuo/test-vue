<template>
  <div  style="width: 80%; border-radius: 4px">
    <h1>字符转换</h1>
    ASCII to STR: <el-input v-model="ascii" placeholder="请输入ASCII"></el-input>
    转换后:
    <el-input v-model="aToS"></el-input>
    STR to ASCII:<el-input v-model="str" placeholder="请输入字符串"></el-input>
    转换后:
    <el-input v-model="sToA"></el-input>
  </div>
</template>

<script>
export default {
  name: "AsciiToStr",
  data() {
    return {
      str: "",
      ascii: "",
    };
  },
  computed: {
    sToA() {
      var a = "";
      for (var i = 0; i < this.str.length; i++) {
        var charAscii = this.str[i].charCodeAt().toString(16);
        a += charAscii + " ";
      }
      return a;
    },
    aToS() {
      if (this.ascii != ""){
        var arr = this.ascii.trim().split(" ");
        var text = '';
        for (var i = 0; i < arr.length; i++) {
          text += String.fromCharCode(parseInt(arr[i],16));
        }
        return text;
      } 
      else return "";
    },
  },
  methods: {},
};
</script>
<style>
</style>