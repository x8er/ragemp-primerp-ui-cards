<template>
  <div id="app">
    <super-card />
  </div>
</template>

<script>
import SuperCard from "@/components/SuperCard.vue";
export default {
  name: "App",
  components: { SuperCard },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
}
</style>
