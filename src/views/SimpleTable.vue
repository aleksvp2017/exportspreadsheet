<template>
    <v-card outlined class="mx-auto mt-10 primary" max-width="700">
        <v-card-title class="white--text">Simple table</v-card-title>
        <v-card-actions>
            <v-divider/>
            <v-btn @click="exportSheet">Export</v-btn>
        </v-card-actions>
        <v-data-table
            show-select
            v-model="rowsSelected"
            class="elevation-1"
            :headers="tableColumns"
            :items="items"
            item-key="product"
            :footer-props="{
                itemsPerPageOptions: [5, 10, 15],
                showFirstLastPage: true,
                firstIcon: 'mdi-arrow-collapse-left',
                lastIcon: 'mdi-arrow-collapse-right',
                prevIcon: 'mdi-arrow-left',
                nextIcon: 'mdi-arrow-right'}"
            :search="searchKey">
        </v-data-table>
    </v-card>
</template>

<script>
import XLSX from 'xlsx'

export default {
    data() {
        return {
            searchKey: '',
            rowsSelected: [],
            tableColumns:[
                {
                    text: 'Product',
                    value: 'product'
                },
                {
                    text: 'Quantity',
                    value: 'quantity'
                 },
                 {
                     text: 'Origin',
                     value: 'origin'
                 } 
            ],
            items: [
                { product: 'Apples', quantity: 1000, origin: 'Ceilândia'}
            ],
        }
    },
    methods: {
        exportSheet(){
            let header = this.tableColumns.map(element => element.value)
            var dataRows = []
            this.rowsSelected.map( row => {
                var dataRow = []
                
                header.map(column => {
                    dataRow.push(row[column])
                })
                dataRows.push(dataRow)
            })
            console.log(dataRows)
            const ws = XLSX.utils.aoa_to_sheet([header,... dataRows])
			const wb = XLSX.utils.book_new()
			XLSX.utils.book_append_sheet(wb, ws, "SimpleTab")
			XLSX.writeFile(wb, "Example.xlsx")
        },
    },
}
</script>