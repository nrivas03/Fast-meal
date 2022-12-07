<template>
    <div class="p-8 pb-0 text-purple-500">
      <h1 class="text-4xl font-bold mb-4">Saved Meals</h1>
    </div>
    <Meals :meals="meals" />
  </template>
  
  <script setup>
  import { computed, onMounted, ref } from "vue";
  import store from "../store";
  import Meals from "../components/Meals.vue";
  import axiosClient from "../axiosClient.js";
  
  //const meals = ref([]);
  </script>

<script>
export default{
  data(){
    return{
      meals: [],
      recipe:[],
    }
  },
  mounted() {
    this.getSave();
    this.showMeals();
  },
  methods:{
    async showMeals(){
      for (let i = 0; i < this.recipe.length; i++) {
        axiosClient
        .get(`lookup.php?i=${this.recipe[i]}`)
        .then(({ data }) => this.meals.push(data.meals[0]));
      }
    },
    async getSave(){
      let data = localStorage.getItem("recipes");
      if(data !=null){
        this.recipe = JSON.parse(data);
      }
    },

  }
};
</script>
  