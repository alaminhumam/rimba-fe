<template>
    <div>
        <table class="table">
            <thead class="thead-light">
                <tr>
                    <th scope="col">Name</th>
                    <th scope="col">Action</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="unit in units" :key="unit.id">
                    <template v-if="unitId == unit.id">
                        <td>
                            <label for="name" class="font-weigh-bold">Name:</label>
                            <div>
                                <input type="text" v-model="unit.name" class="form-control">
                            </div>
                        </td>
                        <td>
                            <b-button variant="primary" class="mr-md-3" @click="saveEdit(unit)">Save Edit</b-button>
                            <b-button variant="danger" class="ml-md-3" @click="cancelEdit(unit)">Cancel Edit</b-button>
                        </td>
                    </template>
                    <template v-else>
                        <td>{{ unit.name }}</td>
                        <td>
                            <b-button variant="success" @click="editUnit(unit)">Edit Unit</b-button>
                            <b-button variant="danger" @click="deleteUnit(unit.id)">Delete</b-button>
                        </td>
                    </template>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: 'unit-table',
    props: {
        units: Array
    },
    data() {
        return {
        unitId: null,
        }
    },
    methods: {
        editUnit(unit) {
            this.data = Object.assign({}, unit)
            this.unitId = unit.id
        },
        saveEdit(unit) {
            let id = this.data.id
            this.$emit('edit-unit', id, unit)
            this.unitId = null
        },
        cancelEdit(unit) {
            Object.assign(unit, this.data)
            this.unitId = null
        },
        deleteUnit(id) {
            this.$emit('delete-unit', id)
        },
    }
}
</script>

<style scoped>
</style>
