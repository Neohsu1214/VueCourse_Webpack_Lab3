<template>
  <div class="component">
    <h3>You may edit the User here</h3>
    <p>Edit me!</p>
    <p>My age is {{ myAge }}</p>
    <button @click="updateAge">Update Age</button>
    <hr />
    <p>This is a data transfer on between siblings using eventBus: {{ dataForSibling }}</p>
  </div>
</template>

<script>
// 註冊 eventBus 來進行跨 components 的資料傳遞
import { eventBus } from "../main.js";

export default {
  data: function() {
    return {
      dataForSibling: "ZXCVF"
    };
  },
  props: {
    myAge: {
      type: Number
    }
  },
  methods: {
    updateAge: function() {
      this.myAge = 30;
      this.$emit("ageWasUpdated", this.myAge);
    }
  },
  created() {
    // 必須在 component 建立時就預先註冊監聽 eventBus 的動作
    eventBus.$on("dataForSiblingsWasUpdated", eventData => {
      this.dataForSibling = eventData;
    });
  }
};
</script>

<style scoped>
div {
  background-color: lightgreen;
}
</style>
