<template>
  <div class="main">
    <h1>加密</h1>
    <button @click="jiami">加密</button>
    <button @click="jiemi">解密</button>
  </div>
</template>

<script>
import CryptoJS from "crypto-js";
export default {
  data() {
    return {
      str: ""
    };
  },
  methods: {
    jiami() {
      const key = CryptoJS.enc.Utf8.parse("1234123412ABCDEF"); //十六位十六进制数作为密钥
      const iv = CryptoJS.enc.Utf8.parse("ABCDEF1234123412"); //十六位十六进制数作为密钥偏移量
      //加密方法
      function Encrypt(word) {
        let srcs = CryptoJS.enc.Utf8.parse(word);
        let encrypted = CryptoJS.AES.encrypt(srcs, key, {
          iv: iv,
          mode: CryptoJS.mode.CBC,
          padding: CryptoJS.pad.Pkcs7
        });
        return encrypted.ciphertext.toString().toUpperCase();
      }
      let obj = {
        name: "zs",
        age: 18,
        id: "001"
      };
      let x = Encrypt(JSON.stringify(obj));
      this.str = x;
      console.log(x);
    },
    jiemi() {
      //解密方法
      const key = CryptoJS.enc.Utf8.parse("1234123412ABCDEF"); //十六位十六进制数作为密钥
      const iv = CryptoJS.enc.Utf8.parse("ABCDEF1234123412"); //十六位十六进制数作为密钥偏移量
      function Decrypt(word) {
        let encryptedHexStr = CryptoJS.enc.Hex.parse(word);
        let srcs = CryptoJS.enc.Base64.stringify(encryptedHexStr);
        let decrypt = CryptoJS.AES.decrypt(srcs, key, {
          iv: iv,
          mode: CryptoJS.mode.CBC,
          padding: CryptoJS.pad.Pkcs7
        });
        let decryptedStr = decrypt.toString(CryptoJS.enc.Utf8);
        return decryptedStr.toString();
      }
      let x = Decrypt(this.str)
      console.log(JSON.parse(x))
    }
  }
};
</script>
<style scoped>
</style>
