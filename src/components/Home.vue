<template>
  <div >
    <h1>Soccer</h1>
  </div>
</template>

<script>

export default {
  name: 'Home',
  data() {
    return {
      msg: 'Emoji Soccer',
    };
  },
  mounted() {
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
html {
}

canvas {
  position: absolute;
  top:0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
  border: 3px solid #F2F2F2;
}
</style>
