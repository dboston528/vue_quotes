<template>
  <div>
    <div v-for="quote in paginatedData">
      <QuoteItem v-bind:quote="quote"/>
    </div>
    <button :disabled="pageNumber === 0" @click="prevPage">Prev</button>
    <button :disabled="pageNumber >= pageCount -1" @click="nextPage">Next</button>
  </div>
</template>

<script>
import QuoteItem from "./QuoteItem.vue";
export default {
  name: "Quotes",
  components: {
    QuoteItem
  },
  props: {
    quotes: {
      type: Array,
      required: true
    },
    size: {
      type: Number,
      required: false,
      default: 10
    }
  },

  data() {
    return {
      pageNumber: 0
    };
  },
  methods: {
    nextPage() {
      this.pageNumber++;
    },
    prevPage() {
      this.pageNumber--;
    }
  },
  computed: {
    pageCount() {
      let l = this.quotes.length,
        s = this.size;
      return Math.ceil(l / s);
    },
    paginatedData() {
      const start = this.pageNumber * this.size,
        end = start + this.size;
      return this.quotes.slice(start, end);
    }
  }
};
</script>

<style scoped></style>

