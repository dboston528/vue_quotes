<template>
  <div id="app">
    <div>
      <input class="search" type="text" v-model="search" placeholder="Search quotes...">
    </div>
    <label>
      <input type="radio" v-model="selectedCategory" value="All"> All
    </label>
    <label>
      <input type="radio" v-model="selectedCategory" value="games"> Game
    </label>
    <label>
      <input type="radio" v-model="selectedCategory" value="movies"> Movie
    </label>
    <Quotes v-bind:quotes="displayedQuotes" v-if="selectedCategory=`All`"/>
    <!-- <p>{{ filteredQuotes }}</p> -->
    <!-- <p>{{ searchQuotes }}</p> -->
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
        return (this.displayedQuotes = this.quotes);
      } else {
        return (this.displayedQuotes = this.quotes.filter(function(quote) {
          return quote.theme === category;
        }));
      }
    },

    searchQuotes: function() {
      this.$set(
        (displayedQuotes = this.quotes.filter(quote =>
          quote.quote.match(this.search)
        ))
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
  margin-left: 15px;
  margin-right: 15px;
}

.search {
  margin-bottom: 15px;
}
</style>
