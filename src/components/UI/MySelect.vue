<template>
    <select v-model="modelValue" @change="changeOption">
        <option disabled value="">Category</option>
        <option v-for="selectOption in selectOptions" :key="selectOption.value" :value="selectOption.value">
            {{ selectOption.name }}
        </option>
    </select>
</template>

<script>
export default {
    name: "my-select",
    props: {
        modelValue: {
            type: String
        },
        selectOptions: {
            type: Array,
            default: ()=> []
        },
        selectedSort: {
            type: String
        }
    },
    methods: {
        changeOption(e) {
            this.$emit('update:modelValue', e.target.value)
        }
    }
}
</script>