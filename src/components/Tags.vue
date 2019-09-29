<template>
  <div class="tag-container">
    <app-tag v-for="(tag,index) in tags" 
    :tag="tag" 
    :index="index" 
    @removeOneTagEvent="removeOneTag($event)" :key="tag"/>
    <input type="text" 
    @keydown.enter="addTag" 
    @keydown.backspace="removeTag" />
    <div class="error" v-if="error">This tag has already submitted!</div>
  </div>
</template>
<script>
import Tag from "./Tag"
export default {
    data (){
      return{
        tags: [],
        error: false
      }
    },
    components: {
        appTag: Tag,
    },
    methods:{
       addTag(event) {
        let text = event.target
        let submittedTag = false

        if (text.value.length > 0) {
          this.tags.forEach(tag => {
            if (tag.toLowerCase() === text.value.toLowerCase()) {
              submittedTag = true;
            }
          })
          if (!submittedTag) {
            this.tags.push(text.value);
            text.value = '';
          } else {
            this.error = true;
            setTimeout(() => {
              this.error = false;
            }, 2000)
          }
        }
      },
      removeTag(e){
        if(e.target.value.length <= 0){
          this.tags.splice(this.tags.length - 1, 1);
        }
      },
      removeOneTag(index){
        this.tags.splice(index, 1);
      }
    },
    props : {
      value : {
        required : false
      }
    },
      created(){
      if(this.value){
        if(this.value.length > 0){
          //to filter dublicants coming from input list
          this.tags = this.value.toLowerCase().split(",").filter((x, i, a) => a.indexOf(x) == i);
        }
      }
      },
    watch : {
      tags(){
        this.$emit("input", this.tags.join(","));
      }
    }

}
</script>

<style scoped>
.tag-container{
 /*   border: 1px solid #ccc;*/
    padding: 20px;
    display: flex;
    
}
input {
    outline: none;
    height: 20px;
    width: 100px;
    border-radius: 5px
}
  .error {
    font-size: 12px;
    color: red;
    margin-top: 5px;
  }


</style>