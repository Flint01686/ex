<template>
    <div v-for="(item, index) in listData" :key="index">
        <span>{{ item.id }}</span>
        <br>
        <span>{{ item.text }}</span>
        <button v-on:click="del(index)">del</button>
        <br>
        <br>
    </div>
    <span>theme</span>
    <input type="text" v-model="theme"/>
    <br>
    <span>text</span>
    <input type="text" v-model="text"/>
    <br>
    <button v-on:click="save">Save</button>
</template>

<script lang="ts">
import { ref } from "vue"

export default {
    setup() {
        const text = ref("")
        const theme = ref("")
        const listData = ref(JSON.parse(localStorage.getItem("list") ?? "[]"));
        const save = function () {
            listData.value.push({
                id: theme.value,
                text: text.value
            })
            localStorage.setItem("list", JSON.stringify(listData.value))
        }
        const del = function (index: number) {
            listData.value.splice(index, 1)
            localStorage.setItem("list", JSON.stringify(listData.value))
        }
        return {
            listData,
            save,
            del,
            text,
            theme
        }
    }
}
</script>
    
<style>

</style>