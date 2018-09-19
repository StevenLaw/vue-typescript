<style scoped>
    #databinding {
        padding: 20px 15px 15px 15px;
        margin: 0 0 25px 0;
        width: auto;
    }
    span, option, input {
        font-style: 20px;
    }
    .Table {
        display: table;
        width: 80%;
    }
    .Title {
        display: table-caption;;
        text-align: center;
        font-weight: bold;
        font-size: larger;
    }
    .Heading {
        display: table-row;
        font-weight: bold;
        text-align: center;
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
    <div id="databinding">
        <h1>Customer Details</h1>
        <span>First Name</span>
        <input type="text" placeholder="Enter First Name" v-model="fname"/>
        <span>Last Name</span>
        <input type="text" placeholder="Enter Last Name" v-model="lname"/>
        <span>Address</span>
        <input type="text" placeholder="Enter Address" v-model="addr"/>
        <button @click="showData" :style="styleObj">Add</button>
        <br>
        <br>
        <CustomerComponent
            v-for="(item, index) in custDet"
            :item="item"
            :index="index"
            :itr="item"
            :key="item.fname"
            @removeelement="custDet.splice(index, 1)">
        </CustomerComponent>
    </div>
</template>

<script lang="ts">
import {Vue, Component, Prop, Provide} from 'vue-property-decorator';
import Customer from '@/models/Customer';
import CustomerComponent from '@/components/CustomerComponent.vue';

@Component({
    name: 'CustomerDetails',
    components: {
        CustomerComponent,
    },
})
export default class CustomerDetails extends Vue {
    public fname: string = '';
    public lname: string = '';
    public addr: string = '';
    public custDet: Customer[] = [];
    public styleObj = {
        backgroundColor: '#2196F3!important',
        cursor: 'pointer',
        padding: '8px 16px',
        verticalAlign: 'middle',
    };

    /**
     * show the data
     */
    public showData(): void {
        this.custDet.push(new Customer(this.fname, this.lname, this.addr));
        this.fname = '';
        this.lname = '';
        this.addr = '';
    }
}
</script>

