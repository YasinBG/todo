<template>
  <div class="w-3/5 bg-gray-800 mx-auto flex flex-col rounded ">
    <h1 class="text-center text-white">Todo-List</h1>

    <input class="w-96 mx-auto my-6 border-4 border-indigo-600 h-12 rounded-lg" type="text" @change="addToList" v-model="text" />

    <ul class="mx-auto my-4 text-white ">
      <li v-for="(item, index) in list" :key="index" class="">
        <span @click="toggleCheck(item)" class=" mx-12 mb-2  ">
          <input type="checkbox" :checked="item.done" class="w-5
          h-5 mr-2 mb-4"  />
          <span :class="{ done: item.done }" class="mx-2">{{ item.label }}</span>
        </span>
        <button @click="deleteFromList(index)" class=" flex-none border-4 border-indigo-600 bg-indigo-300 w-20 rounded">Delete</button>
      
      </li>
    </ul>
  </div>
</template>

<script>

import { ref } from 'vue';
export default {
  name: 'HelloWorld',
  components:{

  },
  setup() {
     let list=ref([])
     let  text =ref("")

    return {
      list,
      text

    }
  },
  created() {
    this.list = JSON.parse(localStorage.getItem("list")) || [];
  },
  methods: {
    addToList() {
      this.list.unshift({ label: this.text, done: false });
      this.updateLocalStorage();
      this.text = "";
    },
    deleteFromList(index) {
      this.list.splice(index, 1);
      this.updateLocalStorage();
    },
    updateLocalStorage() {
      localStorage.setItem("list", JSON.stringify(this.list));
    },
    toggleCheck(item) {
      item.done = !item.done;
      this.updateLocalStorage();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

</style>
