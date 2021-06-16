<template>
    <div>
        <div v-for="(item, index) in items" :key="index">
            <list-item
                :item="item"
                class="item"
                v-on:itemchanged="$emit('reloadlist')"
            />
        </div>
    </div>
</template>

<script>
import listItem from "./listItem";
export default {
    props: ["items"],
    components: {
        listItem
    }
};
</script>
<style scoped>
.item {
    padding: 5px;
    width: 100%;
}
</style>
