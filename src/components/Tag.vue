<template>
  <div>
      <span class="tag" :class="randomTheme(themes)">
      <span class="content">{{ tag }}</span>
      <span class="close" @click="$emit('removeOneTagEvent', index)"> x </span>
      </span>
  </div>
</template>

<script>
export default {
    props: ["tag","index"],
    data() {
      return {
        themes: ["success","primary","secondary","info","warning","danger"]
      }
    },
    methods: {
      randomTheme(arr) {
       return arr[Math.floor(Math.random() * arr.length)];
       }
    }

}
</script>

<style scoped>
.tag{
    padding: 10px;
    cursor:default;
    margin-right: 10px;
    border-radius: 5px;
}
  .tag * {
    font-size: 15px;
  }
.tag .close{
    font-weight: bold;
    font-size: 12px;
    cursor: pointer;
    vertical-align: 8px;
}
.success {
    background-color: #D5EDDB;
    border: 1px solid #c3e6cb;
    color: #155724;
  }

  .primary {
    color: #004085;
    background-color: #cce5ff;
    border-color: #b8daff;
  }

  .secondary {
    color: #383d41;
    background-color: #e2e3e5;
    border-color: #d6d8db;
  }

  .info {
    color: #0c5460;
    background-color: #d1ecf1;
    border-color: #bee5eb;
  }

  .warning {
    color: #856404;
    background-color: #fff3cd;
    border-color: #ffeeba;
  }

  .danger {
    color: #721c24;
    background-color: #f8d7da;
    border-color: #f5c6cb;
  }


</style>