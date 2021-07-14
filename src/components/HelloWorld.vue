<template>
  <div class="hello">
    <!-- <button v-on:click="reverseMessage">{{ message }}</button> -->
 
    <el-row class="smallMargin">
      <el-button icon="el-icon-search" circle class="smallMargin"></el-button>
      <el-button type="primary" icon="el-icon-edit" circle class="smallMargin"></el-button>
      <el-button type="success" icon="el-icon-check" circle class="smallMargin"></el-button>
      <el-button type="info" icon="el-icon-message" circle class="smallMargin"></el-button>
      <el-button type="warning" icon="el-icon-star-off" circle class="smallMargin"></el-button>
      <el-button type="danger" icon="el-icon-delete" circle :loading="true" class="smallMargin"></el-button>
    </el-row>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data: function() {
    return { message: "Привет, Vue.js!" };
  },
  methods: {
    reverseMessage: function() {
      this.message = this.message
        .split("")
        .reverse()
        .join("");
    }
  },
 
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("//unpkg.com/element-ui@2.13.1/lib/theme-chalk/index.css");
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.smallMargin {
  margin: 1em;
}
</style>
