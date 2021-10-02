<template>
    <div class="app">
        <div class="container">
            <h1 class="mb-4">Daftar Unit</h1>
            <hr>
            <p>
                <b-button variant="primary" v-b-toggle.tambah-unit>Tambah Unit</b-button>
            </p>

            <b-collapse id="tambah-unit" class="mt-2">
                <b-card>
                    <h2>Input Data Unit</h2>
                    <hr>

                    <unit-form @add-unit="addUnit"/>
                </b-card>
            </b-collapse>


            <unit-table v-bind:units="units" @edit-unit="editUnit" @delete-unit="deleteUnit"/>

        </div>
    </div>
</template>

<script>
import axios from 'axios'

import UnitTable from './UnitTable.vue'
import UnitForm from './UnitForm.vue'

export default {
    name: 'App',
    components: {
        UnitTable,
        UnitForm
    },
    data() {
        return {
        units: []
        }
    },
    created() {
        axios.get('http://test-rimba.test/api/v1/units')
        .then(response => {
            this.units = response.data.data
        })
    },
    methods: {
        addUnit(unit) {
            axios.post('http://test-rimba.test/api/v1/units', unit)
            .then(response => {
                this.units = [...this.units, response.data.data]
            })
        },
        editUnit(id, data) {
            axios.put(`http://test-rimba.test/api/v1/units/${id}`, data)
            .then(() => {
                this.units = this.units.map(unit => (unit.id === id ? data : unit))
            })
        },
        deleteUnit(id) {
            axios.delete(`http://test-rimba.test/api/v1/units/${id}`)
            .then(() => {
                const unitId = this.units.indexOf(id)
                this.units.splice(unitId, 1)
            })
        }
    }
}
</script>