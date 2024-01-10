<template>
  <div class="hello" style="width: 80%; margin: 20px">
    <h1>CRC校验</h1>
    <el-input
      type="textarea"
      autosize
      style="margin-top: 20px"
      placeholder="输入校验字符"
      v-model="hexString"
    >
    </el-input>
    <el-input
      v-model="crcString"
      style="margin-top: 20px"
      placeholder="校验码:"
    ></el-input>
    <el-button @click="crc16ModbusClick()" style="margin-top: 20px"
      >确定</el-button
    >
  </div>
</template>

<script>
export default {
  name: "Crc",
  data() {
    return {
      hexString: "",
      crcString: "",
    };
  },
  props: {
    msg: String,
  },
  created() {},
  methods: {
    crc16ModbusClick() {
      this.crcString = this.calculateCRC16Modbus(this.hexString);
    },
    // 左侧补齐0
    pad(str, max) {
      str = str.toString();
      return str.length < max ? this.pad("0" + str, max) : str;
    },
    calculateCRC16Modbus(dataHexString) {
      const dataBytes = [];
      for (let i = 0; i < dataHexString.length; i += 2) {
        dataBytes.push(parseInt(dataHexString.substr(i, 2), 16));
      }

      let crc = 0xffff;
      const polynomial = 0xa001; // This is the polynomial x^16 + x^15 + x^2 + 1

      for (const byte of dataBytes) {
        crc ^= byte;
        for (let i = 0; i < 8; i++) {
          if (crc & 0x0001) {
            crc = ((crc >> 1) ^ polynomial) & 0xffff;
          } else {
            crc >>= 1;
          }
        }
      }

      crc = this.pad(crc.toString(16).toUpperCase(), 4); //补0(不然会出八阿哥)
      let crcArr = new Array(2);
      console.log("crc=" + crc);
      crcArr[0] = crc.substring(2, 4);
      crcArr[1] = crc.substring(0, 2);
      let code = crcArr[0] + crcArr[1];
      return code;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
