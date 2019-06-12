<template>
  <div>
    <h3>{{quote.quote}}</h3>
    <p>{{quote.source}}</p>
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
