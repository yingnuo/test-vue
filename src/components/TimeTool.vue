<template>
  <div class="block" style="width: 90%">
    <h1>时间转换</h1>
    <el-tabs v-model="activeName" @tab-click="handleClick">
      <el-tab-pane label="1970-1-1 08:00:00开始计算" name="first">
        <el-date-picker
          v-model="timeStamp"
          type="datetime"
          placeholder="1970开始的"
          value-format="timestamp"
          @change="timeStampChange"
        >
        </el-date-picker>
        <el-form
          ref="form"
          :model="form"
          label-width="150px"
          style="margin-top: 20px; margin-right: 50px"
        >
          <el-form-item label="时间戳(秒)">
            <el-input
              v-model="timeS"
              placeholder="请输入秒数"
              @change="timeSChange"
            ></el-input>
          </el-form-item>
          <el-form-item label="16进制(秒)">
            <el-input
              v-model="timeStampHex"
              placeholder="请输入16进制秒"
              @change="timeStampHexChange"
            ></el-input>
          </el-form-item>
          <el-form-item label="16进制反转(秒)">
            <el-input v-model="reverseTSH"></el-input>
          </el-form-item>
        </el-form>
      </el-tab-pane>
      <el-tab-pane label="2000-1-1 00:00:00开始计算" name="second">
        <el-date-picker
          v-model="timeStamp2000"
          type="datetime"
          placeholder="2000开始的"
          value-format="timestamp"
          @change="timeStamp2000Change"
        >
        </el-date-picker>
        <el-form
          ref="form"
          :model="form"
          label-width="150px"
          style="margin-top: 20px; margin-right: 50px"
        >
        <el-form-item label="时间戳(秒)">
          <el-input
            v-model="timeS2000"
            placeholder="请输入秒数"
            @change="timeS2000Change"
          ></el-input>
        </el-form-item>
          
          <el-form-item label="16进制(秒)">
          <el-input
            v-model="timeStamp2000Hex"
            placeholder="请输入16进制秒"
            @change="timeStampHex2000Change"
          ></el-input>
          </el-form-item>
                    
          <el-form-item label="16进制反转(秒)">
          <el-input
            v-model="reverseTSH2000"
          ></el-input>
          </el-form-item>
        </el-form>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
export default {
  name: "TimeTool",
  data() {
    return {
      activeName: "second",
      timeStamp: "", //时间选择器的毫秒数
      timeS: "",
      timeStamp: "",
      timeStr: "",
      timeS2000: "",
      timeStamp2000: "",
      timeStampHex: "",
      timeStamp2000Hex: "",
      reverseTSH: "",
      reverseTSH2000: "",
    };
  },
  computed: {},
  methods: {
    //1970年16进制输入框改变的时候
    timeStampHexChange() {
      this.timeS = parseInt(this.timeStampHex, 16);
      this.timeStamp = this.timeS * 1000;
      this.timeStamp2000 = this.timeStamp + 946656000000;
      this.reverseTSH = this.reverseStr(this.timeS);
      this.timeS2000 = this.timeStamp2000 / 1000 - 946656000;
      this.timeStamp2000Hex = Number(this.timeS2000).toString(16);
      this.reverseTSH2000 = this.reverseStr(this.timeS2000);
    },
    //当1970年日期选择器发生改变时
    timeStampChange() {
      this.timeS = this.timeStamp / 1000;
      this.timeStamp2000 = this.timeStamp + 946656000000;
      this.timeStampHex = Number(this.timeS).toString(16);
      this.reverseTSH = this.reverseStr(this.timeS);
      this.timeS2000 = this.timeStamp2000 / 1000 - 946656000;
      this.timeStamp2000Hex = Number(this.timeS2000).toString(16);
      this.reverseTSH2000 = this.reverseStr(this.timeS2000);
    },
    //当1970年秒数显示框发生改变时
    timeSChange() {
      this.timeStamp = this.timeS * 1000;
      this.timeStamp2000 = this.timeStamp + 946656000000;
      this.timeStampHex = Number(this.timeS).toString(16);
      this.reverseTSH = this.reverseStr(this.timeS);
      this.timeS2000 = this.timeStamp2000 / 1000 - 946656000;
      this.timeStamp2000Hex = Number(this.timeS2000).toString(16);
      this.reverseTSH2000 = this.reverseStr(this.timeS2000);
    },
    timeS2000Change() {
      this.timeStamp2000 = this.timeS2000 * 1000 + 946656000000;
      this.timeStamp = this.timeStamp2000 - 946656000000;
      this.timeS = Number(this.timeStamp) / 1000;
      this.timeStampHex = Number(this.timeS).toString(16);
      this.reverseTSH = this.reverseStr(this.timeS);
      this.timeStamp2000Hex = Number(this.timeS2000).toString(16);
      this.reverseTSH2000 = this.reverseStr(this.timeS2000);
    },
    timeStamp2000Change() {
      this.timeStamp = this.timeStamp2000 - 946656000000;
      this.timeS = this.timeStamp / 1000;
      this.timeStampHex = Number(this.timeS).toString(16);
      this.reverseTSH = this.reverseStr(this.timeS);
      this.timeS2000 = this.timeStamp2000 / 1000 - 946656000;
      this.timeStamp2000Hex = Number(this.timeS2000).toString(16);
      this.reverseTSH2000 = this.reverseStr(this.timeS2000);
    },
    timeStampHex2000Change() {
      this.timeS2000 = parseInt(this.timeStamp2000Hex, 16);
      this.timeStamp2000 = this.timeS2000 * 1000 + 946656000000;
      this.timeStamp = this.timeStamp2000 - 946656000000;
      this.timeS = Number(this.timeStamp) / 1000;
      this.timeStampHex = Number(this.timeS).toString(16);
      this.reverseTSH = this.reverseStr(this.timeS);
      this.reverseTSH2000 = this.reverseStr(this.timeS2000);
    },

    reverseStr(str) {
      var dataHexString = Number(str).toString(16);
      const dataBytes = [];
      for (let i = 0; i < dataHexString.length; i += 2) {
        dataBytes.push(dataHexString.substr(i, 2) + "");
      }
      return dataBytes.reverse().join("");
    },
  },
};
</script>

<style>
</style>