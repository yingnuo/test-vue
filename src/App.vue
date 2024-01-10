<template>
  <div id="app">
    <el-row type="flex" class="row-bg" justify="center">
      <el-col :span="12"> <Crc /></el-col>

      <el-col :span="12"> <AsciiToStr /></el-col>
    </el-row>
    <el-row type="flex" class="row-bg" justify="center">
      <el-col :span="12"><Sum /></el-col>
      
      <el-col :span="12"> <TimeTool /></el-col>
    </el-row>
  </div>
</template>

<script>
import AsciiToStr from "./components/AsciiToStr.vue";
import Crc from "./components/Crc.vue";
import Sum from "./components/Sum.vue";
import TimeTool from "./components/TimeTool.vue";

export default {
  name: "App",
  components: {
    Crc,
    TimeTool,
    AsciiToStr,
    Sum,
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
.el-row {
  margin-bottom: 20px;
}
.el-col {
  border-radius: 4px;
}
.bg-purple-dark {
  background: #99a9bf;
}
.bg-purple {
  background: #ebf5dd;
}
.bg-purple-light {
  background: #ebf5dd;
}
.grid-content {
  border-radius: 4px;
  min-height: 36px;
}
.row-bg {
  padding: 10px 0;
  background-color: #ecf8dc;
}
</style>
