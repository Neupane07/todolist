<template>
    <div class="item">
        <input type="checkbox" @change="updateCheck" v-model="item.completed" />
        <span :class="[item.completed ? 'completed' : '', 'itemText']">
            {{ item.name }}</span
        >
        <button @click="removeItem()" class="trashcan">
            <font-awesome-icon icon="trash" />
        </button>
    </div>
</template>

<script>
export default {
    props: ["item"],
    methods: {
        updateCheck() {
            axios
                .put("api/item/" + this.item.id, {
                    item: this.item
                })
                .then(response => {
                    if (response.status == 200) {
                        this.$emit("itemchanged");
                    }
                })
                .catch(error => {
                    console.log(error);
                });
        },
        removeItem() {
            axios
                .delete("api/item/" + this.item.id)
                .then(response => {
                    if (response.status == 200) {
                        this.$emit("itemchanged");
                    }
                })
                .catch(error => {
                    console.log(error);
                });
        }
    }
};
</script>

<style>
.completed {
    text-decoration: line-through;
    color: #999999;
}
.itemText {
    width: 100%;
    margin-left: 20px;
}
.item {
    margin-top: 5px;
    display: flex;
    background: #95d5b2;
    justify-content: center;
    align-items: center;
}

.item input[type="checkbox"] {
    appearance: initial;
    border: 1px solid black;
    padding: 1em;
}

.item input[type="checkbox"]:checked {
    background: #ccc;
}

.trashcan {
    background: #95d5b2;
    border: none;
    color: #ff0000;
    outline: none;
}
</style>
