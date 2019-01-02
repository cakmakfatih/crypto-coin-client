<template>
  <div class="container">
    <div class="level">
        <div class="level-item has-text-centered" v-if="currency.rank">
            <div>
                <p class="heading">Rank</p>
                <p class="title">{{currency.rank}}</p>
            </div>
        </div>
        <div class="level-item has-text-centered" v-if="currency.name">
            <div>
                <p class="heading">Name</p>
                <p class="title">{{currency.name}}</p>
            </div>
        </div>
        <div class="level-item has-text-centered" v-if="currency.symbol">
            <div>
                <p class="heading">Symbol</p>
                <p class="title">{{currency.symbol}}</p>
            </div>
        </div>
        <div class="level-item has-text-centered" v-if="currency.price_usd">
            <div>
                <p class="heading">Price (USD)</p>
                <p class="title">{{currency.price_usd}}</p>
            </div>
    </div>
    </div>
    <div class="level">
        <div class="level-item has-text-centered" v-if="currency.price_btc">
            <div>
                <p class="heading">Price (BTC)</p>
                <p class="title">{{currency.price_btc}}</p>
            </div>
        </div>
        <div class="level-item has-text-centered" v-if="currency['24h_volume_usd']">
            <div>
                <p class="heading">24h Volume (USD)</p>
                <p class="title">{{currency["24h_volume_usd"]}}</p>
            </div>
        </div>
        <div class="level-item has-text-centered" v-if="currency.market_cap_usd">
            <div>
                <p class="heading">Market Cap (USD)</p>
                <p class="title">{{currency.market_cap_usd}}</p>
            </div>
        </div>
        <div class="level-item has-text-centered" v-if="currency.total_supply">
            <div>
                <p class="heading">Total Supply</p>
                <p class="title">{{currency.total_supply}}</p>
            </div>
        </div>
    </div>
    <div class="level">
        <div class="level-item has-text-centered" v-if="currency.max_supply">
            <div>
                <p class="heading">Max Supply</p>
                <p class="title">{{currency.max_supply}}</p>
            </div>
        </div>
        <div class="level-item has-text-centered" v-if="currency.percent_change_1h">
            <div>
            <p class="heading">Percent Change (1h)</p>
            <p class="title">-{{currency.percent_change_1h}}</p>
            </div>
        </div>
        <div class="level-item has-text-centered" v-if="currency.percent_change_24h">
            <div>
            <p class="heading">Percent Change (24h)</p>
            <p class="title">{{currency.percent_change_24h}}</p>
            </div>
        </div>
        <div class="level-item has-text-centered" v-if="currency.percent_change_7d">
            <div>
            <p class="heading">Percent Change (7d)</p>
            <p class="title">{{currency.percent_change_7d}}</p>
            </div>
        </div>
    </div>
</div>
</template>

<script lang="ts">
import { Currency } from './../models/currency.model';
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class CurrencyComponent extends Vue {
  @Prop() private currency!: Currency;
}
</script>
<style lang="scss" scoped>
p.heading {
    color: #616161;
}
</style>