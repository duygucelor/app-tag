<template>
  <div class="container">
    <app-tags v-model="tags1" > </app-tags>
  </div>
</template>

<script>
import Tags from "./components/Tags"
export default {
    components: {
        appTags: Tags,
    },
    data (){
        return{
         tags1: "JavaScript,PHP,C++,html,html,php,PHP"
        }
    }
}
</script>

<style>
body{
    font-family: sans-serif;
}
</style>
