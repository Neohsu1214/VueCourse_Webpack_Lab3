<template>
  <div class="component">
    <h3>You may view the User Details here</h3>
    <p>Many Details</p>
    <p>User name: {{ myName }}</p>
    <p>{{ staticString }}</p>
    <p>Revered Name is {{ reverseName }}</p>
    <p>User age: {{ myAge }}</p>
    <button @click="resetName">Reset Name</button>
    <button @click="resetFn">Reset Name From Parent Function</button>
    <hr>
    <p>This is a data transfer on between siblings using eventBus: {{ dataForSibling }}</p>
    <button @click="changeDataFroSiblings">Change Data for siblings</button>
  </div>
</template>

<script>
// 註冊 eventBus 來進行跨 components 的資料傳遞
import { eventBus } from "../main.js";

export default {
  data: function() {
      return {
          dataForSibling: 'ABCDE'
      }
  },
  props: {
    // 由 parent 傳進來的參數，要宣告在 props
    myName: {
      // props可指定datatype來驗證傳進來的資料類別，此例允許 String 或 Array
      type: [String, Array],
      // 要求一定要有資料才能使用
      required: true
      // 當沒給值時的預設值，default 與 required 互斥，擇一使用即可
      //default: 'Zoe'
    },
    staticString: String,
    resetFn: {
      type: Function
    },
    myAge: {
      type: Number,
      required: true
    }
  },
  computed: {
    reverseName: function() {
      // 存取 props 的參數用法跟存取 data的方式依樣 this.xxx
      return this.myName
        .split("")
        .reverse()
        .join("");
    }
  },
  methods: {
    resetName: function() {
      // 當 Child component有資料要傳給 Parent Component 時，使用 this.$emit('事件名稱', 傳遞參數) 來達成
      this.myName = "NeoHsu";
      this.$emit("nameWasReset", this.myName); // 由於是事件，所以 parent component 也要用 v-on:事件名稱 來接收資料
    },
    changeDataFroSiblings: function() {
        this.dataForSibling = 'QWERT';
        eventBus.$emit('dataForSiblingsWasUpdated', this.dataForSibling);
    }
  }
};
</script>

<style scoped>
div {
  background-color: lightcoral;
}
</style>
