<style scoped>
    .Table {
        display: table;
        width: 80%;
    }
    .Row {
        display: table-row;
    }
    .Cell {
        display: table-cell;
        border: solid;
        border-width: 5px;
        padding-left: 5px;
        padding-right: 5px;
        width: 30%;
    }
</style>


<template>
    <div class="Table">
        <div class="Row" :style="styleObj">
            <div class="Cell">
                <p>{{itr.fname}}</p>
            </div>
            <div class="Cell">
                <p>{{itr.lname}}</p>
            </div>
            <div class="Cell">
                <p>{{itr.addr}}</p>
            </div>
            <div class="Cell">
                <p>
                    <button @click="$emit('removeelement')">X</button>
                </p>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import {Vue, Component, Prop} from 'vue-property-decorator';
import Customer from '@/models/Customer';

@Component({
    name: 'CustomerCmponent',
})
export default class CustomerComponent extends Vue {
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
