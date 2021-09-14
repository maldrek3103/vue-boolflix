<template>
  <section>
    <input type="text" :placeholder="placeholder" v-model.trim="inputText" />
    <button type="submit" @click="sendSearch" @keyup.enter="sendSearch">
      {{ submitText || "Search" }}
    </button>
  </section>
</template>

<script>
export default {
  name: "Search",
  props: ["placeholder", "submitText"],
  data() {
    return {
      inputText: "",
    };
  },
  methods: {
    sendSearch() {
      this.$emit("search", this.inputText);
    },
  },
};
</script>

<style>
</style>