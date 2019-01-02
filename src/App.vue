<template>
  <div id="app">
    <form @submit="search">
      <h1 class="title is-2">
        CryptoSearcher
      </h1>
      <h2 class="subtitle">
        Search any crypto coin by it's symbol to retrieve up-to-date data.
      </h2>
      <div class="level-item has-text-centered">
        <div class="field has-addons">
          <div class="control">
            <input class="input is-primary is-medium" type="text" placeholder="Search" v-model="query">
          </div>
          <div class="control">
            <button class="button is-primary is-medium" :disabled="loading">
              Search
            </button>
          </div>
        </div>
      </div>
    </form>
    <div class="loader" style="height: 50px; width: 50px;" v-if="loading"></div>
    <div v-if="result == null && !loading">
      <span class="subtitle">
        Couldn't find anything similiar to your search.
      </span>
    </div>
    <app-currency v-bind:currency="result" v-if="!loading && result"></app-currency>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';
import CurrencyComponent from './components/CurrencyComponent.vue';
import { Currency } from './models/currency.model';

declare module 'vue/types/vue' {
  interface Vue {
    apiEndpoint: string;
    result?: Currency;
    loading: boolean;
    query: string;
    lastSearch: string;
    fetchData: Function;
  }
}

@Component({
  components: {
    "app-currency": CurrencyComponent
  },
  data() {
    return {
      apiEndpoint: "https://kns-crypto-search.herokuapp.com/coin?search=",
      result: null,
      loading: null,
      query: ""
    };
  },
  methods: {
    async fetchData(query: string) {
      if(!(this.result && this.result.status === "success" && query.toUpperCase() === this.result!.symbol.toUpperCase()) && query !== this.lastSearch) {
        this.lastSearch = query;
        this.loading = true;
        let res = await fetch(`${this.apiEndpoint}${query}`).then(re => re.json());
        if(res.status !== "error") {
          this.result = res;
        } else {
          this.result = undefined;
        }
        this.loading = false;
      }
    },
    search(e: Event) {
      e.preventDefault();
      this.fetchData(this.query);
    }
  },
  created() {
    this.fetchData("btc");
  }
})
export default class App extends Vue {}
</script>

<style lang="scss">
#app {
  width: 100vw;
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding: 35px;
  overflow-y: hidden;
  flex-direction: column;
  justify-content: center;
}
form {
  display: flex;
  justify-content: center;
  flex-direction: column;
  text-align: center;
}
.field {
  margin-bottom: 20px;
}
.field > .control > input {
  min-width: 40vw;
}
h2.subtitle {
  text-align: center;
}
p.heading {
  font-weight: bold;
}
</style>
