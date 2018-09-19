<style scoped>
    .currencySelect {
        width:300px;
        font-style:25px;
    }
</style>

<template>
    <div class="converter">
        <h1>Currency Converter</h1>
        <span>Enter Amount:</span>
        <input type="number" v-model.number="amount" placeholder="Enter Amount"/>>
        <br/>
        <br/>
        <span>Convert From:</span>
        <select v-model="convertFrom" class="currencySelect">
            <option v-for="(a) in currencyList" :key="a.name" :value="a.name">{{a.desc}}</option>
        </select>
        <br/>
        <span>Convert To:</span>
        <select v-model="convertTo" class="currencySelect">
            <option v-for="(a) in currencyList" :key="a.name" :value="a.name">{{a.desc}}</option>
        </select>
        <br/>
        <br/>
        <span>{{amount}} {{convertFrom}} equals {{finalAmount}} {{convertTo}}</span>
    </div>    
</template>

<script lang="ts">
import {Vue, Component, Prop} from 'vue-property-decorator';
import Currency from '@/models/Currency';
import {currencyList} from '@/data/CurrencyList';

@Component
export default class Converter extends Vue {
    public currencyList: Currency[] = currencyList;
    public convertFrom: string = 'INR';
    public convertTo: string = 'USD';
    public amount: number = 0;

    get finalAmount(): number {
        const to = this.convertTo;
        const from = this.convertFrom;
        let final = 0;
        switch (from) {
            case 'INR':
            switch (to) {
                case 'USD':
                final = this.amount * 0.016;
                break;
                case 'EUR':
                final = this.amount * 0.013;
                break;
                case 'INR':
                final = this.amount;
                break;
                case 'BHD':
                final = this.amount * 0.0059;
                break;
            }
            break;
            case 'USD':
            switch (to) {
                case 'USD':
                final = this.amount;
                break;
                case 'EUR':
                final = this.amount * 0.84;
                break;
                case 'INR':
                final = this.amount * 63.88;
                break;
                case 'BHD':
                final = this.amount * 0.38;
                break;
            }
            break;
            case 'EUR':
            switch (to) {
                case 'USD':
                final = this.amount * 1.19;
                break;
                case 'EUR':
                final = this.amount;
                break;
                case 'INR':
                final = this.amount * 76.22;
                break;
                case 'BHD':
                final = this.amount * 0.45;
                break;
            }
            break;
            case 'BHD':
            switch (to) {
                case 'USD':
                final = this.amount * 2.65;
                break;
                case 'EUR':
                final = this.amount * 2.22;
                break;
                case 'INR':
                final = this.amount * 169.44;
                break;
                case 'BHD':
                final = this.amount;
                break;
            }
            break;
        }
        return final;
    }
}
</script>

