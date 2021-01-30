<template>
  <div>
    <div class="header">중개 찾기</div>
    <Compare />
  </div>
</template>

<script>
import Compare from "./views/Compare";

export default {
  name: "App",
  components: {
    Compare,
  },
};
</script>

<style>
.header {
  font-size: 50px;
  text-align: center;
  margin-top: 1rem;
}
</style>