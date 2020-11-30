<template>
  <div>
    <input type="text" v-model="message" />
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  name: "TodoApplication",
  data() {
    return {
      message: "Todo Application Sample"
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
