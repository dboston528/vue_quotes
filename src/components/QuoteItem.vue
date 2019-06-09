<template>
  <div>
    <p>{{quote.quote}}</p>
  </div>
</template>



<script>
export default {
  name: "QuoteItem",
  props: ["quote"]
};
</script>

<style scoped>
</style>
