<template>
  <div id="app">
    <div>
      <input type="text" v-model="search" @change="searchQuotes" placeholder="Search quotes...">
    </div>
    <label>
      <input type="radio" v-model="selectedCategory" @click="filteredQuotes" value="All"> All
    </label>
    <label>
      <input type="radio" v-model="selectedCategory" @click="filteredQuotes" value="games"> Game
    </label>
    <label>
      <input type="radio" v-model="selectedCategory" @click="filteredQuotes" value="movies"> Movie
    </label>
    <Quotes v-bind:quotes="displayedQuotes"/>
  </div>
</template>

<script>
import axios from "axios";
import Quotes from "./components/Quotes";

export default {
  name: "app",
  components: {
    Quotes
  },
  data() {
    return {
      quotes: [],
      selectedCategory: "All",
      search: "",
      displayedQuotes: []
    };
  },
  created() {
    axios
      .get(
        "https://gist.githubusercontent.com/benchprep/dffc3bffa9704626aa8832a3b4de5b27/raw/quotes.json"
      )
      .then(res => {
        this.quotes = res.data;
        this.displayedQuotes = [...res.data];
      })
      .catch(err => console.log(err));
  },
  computed: {
    filteredQuotes: function() {
      var category = this.selectedCategory;
      if (category === "All") {
        return this.displayedQuotes;
      } else {
        return this.displayedQuotes.filter(function(quote) {
          return quote.theme === category;
        });
      }
    },

    searchQuotes: function() {
      return this.displayedQuotes.filter(quote =>
        quote.quote.match(this.search)
      );
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
