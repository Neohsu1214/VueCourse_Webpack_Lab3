<template>
  <div class="component">
    <h1>The User Component</h1>
    <p>I'm an awesome User!</p>
    <button @click="changeName">Change my name</button>
    <p>Name is: {{ name }}</p>
    <p>Age is: {{ age }}</p>
    <hr />
    <div class="row">
      <div class="col-xs-12 col-sm-6">
        <!-- 要傳遞給 child component 的參數，記得要在 template 用 v-bind: 綁定 ex: :myName -->
        <!-- 若沒加上 v-bind 的話，會變成單純傳字串給 child component，ex: staticString -->
        <app-user-detail 
            :myName="name" 
            staticString="Hello Child!" 
            @nameWasReset="name=$event"
            :resetFn="resetNameFromParent"
            :myAge="age"></app-user-detail>
      </div>
      <div class="col-xs-12 col-sm-6">
        <app-user-edit 
            :myAge="age"
            @ageWasUpdated="age = $event"></app-user-edit>
      </div>
    </div>
  </div>
</template>

<script>
import UserDetail from "./UserDetail.vue";
import UserEdit from "./UserEdit.vue";

export default {
  data: function() {
    return {
      name: "Neo",
      age: 41 // age同時傳遞給兩個 children component，並由 UserEdit 進行修改後，同步到 parent 與其他 children
    };
  },
  methods: {
    //ES6支援寫成 changeName() {}
    changeName: function() {
      this.name = "Viny";
    },
    resetNameFromParent: function() {
      this.name = "Zoe";
    }
  },
  components: {
    appUserDetail: UserDetail,
    appUserEdit: UserEdit
  }
};
</script>

<style scoped>
div {
  background-color: lightblue;
}
</style>
