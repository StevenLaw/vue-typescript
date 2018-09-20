<style>
    .customerRow td {
        border:solid;
        border-width: 5px;
        padding-left: 5px;
        padding-right: 5px;
        width: 30%;
    }
</style>

<template>
    <tr class="customerRow" :style="styleObj">
        <td>{{itr.fname}}</td>
        <td>{{itr.lname}}</td>
        <td>{{itr.addr}}</td>
        <td>
            <button @click="$emit('removeelement')">X</button>
        </td>
    </tr>
</template>

<script lang="ts">
import {Vue, Component, Prop} from 'vue-property-decorator';
import Customer from '@/models/Customer';
import { compileFunction } from 'vm';

@Component
export default class CustomerRowComponent extends Vue {
    @Prop() public itr!: Customer;
    @Prop() public index!: number;

    public styleObj = {
        backgroundColor: this.getColor(),
        fontSize: 20,
    };

    public getColor(): string {
        if (this.index % 2) {
            return '#FFE633';
        } else {
            return '#D4CA87';
        }
    }
}
</script>
