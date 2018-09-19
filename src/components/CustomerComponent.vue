<template>
    <div class="Table">
        <div class="Row">
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
