<template>
  <header>
    <h1>Quiz Questions</h1>
    <div id="nav"></div>
  </header>
</template>
<script>
export default {
  name: "Header",
};
</script>
<style scoped>
header {
  background-color: #a21212;
  color: #fff;
  padding: 15px;
  height: 60px;
  font-size: 15px;
  text-align: left;
}
h1 {
  position: relative;
  padding-bottom: 35px;
  text-decoration: none;
}
@media only screen and (max-width: 600px) {
  header {
    flex-direction: column;
    width: 100%;
    height: 80%;
  }
}
</style>