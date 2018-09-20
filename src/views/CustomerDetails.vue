<style scoped>
    #databinding {
        padding: 20px 15px 15px 15px;
        margin: 0 0 25px 0;
        width: auto;
    }
    /* span, option, input {
        font-style: 20px;
    } */
    #tableContainer {
        width: 100%;
    }
    #tableContainer table {
        margin: 0 auto;
    }
    #tableContainer td {
        font-style: 20px;
    }
    #tableContainer th {
        font-style: 20px;
        text-align: left;
    }
    #customerTable {
        border-collapse: collapse;
        width: 80%;
    }
</style>

<template>
    <div id="databinding">
        <h1>Customer Details</h1>
        <div id="tableContainer">
            <table>
                <tr>
                    <th>First Name</th>
                    <td>
                        <input type="text" placeholder="Enter First Name" v-model="fname"/>
                    </td>
                </tr>
                <tr>
                    <th>Last Name</th>
                    <td>
                        <input type="text" placeholder="Enter Last Name" v-model="lname"/>
                    </td>
                </tr>
                <tr>
                    <th>Address</th>
                    <td>
                        <input type="text" placeholder="Enter Address" v-model="addr"/>
                    </td>
                </tr>
            </table>
        </div>
        
        <!-- <div>
            <span>First Name</span>
            <input type="text" placeholder="Enter First Name" v-model="fname"/>
        </div>
        
        <div>
            <span>Last Name</span>
            <input type="text" placeholder="Enter Last Name" v-model="lname"/>
        </div>

        <div>
            <span>Address</span>
            <input type="text" placeholder="Enter Address" v-model="addr"/>
        </div> -->

        <button @click="showData" :style="styleObj">Add</button>
        <br>
        <br>

        <h1>Div based</h1>

        <CustomerComponent
            v-for="(item, index) in custDet"
            :item="item"
            :index="index"
            :itr="item"
            :key="index"
            @removeelement="custDet.splice(index, 1)">
        </CustomerComponent>

        <h1>Table based</h1>

        <div style="width:100%;" v-if="custDet.length > 0">
            <table id="customerTable">
                <CustomerRowComponent
                    v-for="(item, index) in custDet"
                    :item="item"
                    :index="index"
                    :itr="item"
                    :key="index"
                    @removeelement="custDet.splice(index, 1)">
                </CustomerRowComponent>
            </table>
        </div>
    </div>
</template>

<script lang="ts">
import {Vue, Component, Prop, Provide} from 'vue-property-decorator';
import Customer from '@/models/Customer';
import CustomerComponent from '@/components/CustomerComponent.vue';
import CustomerRowComponent from '@/components/CustomerRowComponent.vue';

@Component({
    name: 'CustomerDetails',
    components: {
        CustomerComponent,
        CustomerRowComponent,
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

