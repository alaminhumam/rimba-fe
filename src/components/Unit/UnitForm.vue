<template>
    <div class="unit-form">
        <form v-on:submit.prevent="submit">
            <div class="form-group mb-4">
                <label for="name">Name</label>
                <input type="text" v-model="unit.name" class="form-control" placeholder="Masukan Besaran unit">
            </div>
            <b-button type="submit" variant="outline-primary">Simpan</b-button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'unit-form',
    data() {
        return {
            unit: {
                name: ''
            }
        }
    },
    methods: {
        submit() {
            this.$emit('add-unit', this.unit)
            this.unit = {
                name: ''
            }
        }
    }
}
</script>