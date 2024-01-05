<template>
    <div><h1>Galpões Cadastrados</h1>

        <v-text-field label="Buscar galpão" v-model="term" class="my-5"></v-text-field>
        <v-card>
            <v-card-text>
                <WarehouseTable :warehouses="filterWarehouse"/> 
            </v-card-text>
        </v-card>
        
    </div>
</template>

<script>
import Warehouse from '../components/Warehouse.vue'
import WarehouseTable from '../components/WarehouseTable.vue'
export default {
    name: 'WarehouseList',
    components:{
        Warehouse,
        WarehouseTable
    },
    data(){
        return{
            warehouses:[],
            term: ''
        }
    },
    async mounted(){
        this.getWarehouses();
    },
    methods: {
        async getWarehouses(){
            const response = await this.$http.get('http://127.0.0.1:3000/api/v1/warehouses');
            const result = await response.json();

            console.log(result);
            this.warehouses = result;
            return this.warehouses
        }
    },
    computed: {
        filterWarehouse(){
            return this.warehouses.filter(warehouse => {
                return warehouse.name.toLowerCase().includes(this.term.toLowerCase());
            })
        }
       }
}
</script>

<style>
    .form{
        margin-bottom: 20px;
    }
</style>