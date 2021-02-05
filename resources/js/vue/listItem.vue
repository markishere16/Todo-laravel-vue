<template>
    <div class="item">
        <input type="checkbox" name="" id="" @change="updateCheck()" v-model="item.completed">
        <input type="text" :class="[item.completed ? 'completed' : '', 'itemText']" v-model="item.name"
            :disabled="edit == false ? true : false">

        <button @click="removeItem()" class="btn btn-danger ml-2">
            <font-awesome-icon icon="trash" /> </button>

        <button @click="editItem()" class="btn btn-primary ml-2 ">
            <font-awesome-icon :icon="edit == false ? 'pencil-alt' : 'save' " /> </button>
    </div>
</template>
<script>
    export default {
        props: ['item'],
        data: function () {
            return {
                edit: false
            }
        },

        methods: {
            updateCheck() {
                axios.put('api/items/' + this.item.id, {
                        item: this.item
                    })
                    .then(response => {
                        if (response.status == 200) {
                            this.$emit('itemChanged');
                        }
                    })
                    .catch(error => {
                        console.log(error);
                    })
            },
            removeItem() {
                axios.delete('api/items/' + this.item.id)
                    .then(response => {
                        if (response.status == 200) {
                            this.$emit('itemChanged');
                        }
                    })
                    .catch(error => {
                        console.log(error);
                    })
            },
            editItem() {

                this.edit = this.edit == true ? false : true;

                if (this.edit == false) {
                    console.log(this.item);

                    axios.put('api/items/' + this.item.id, {
                            item: this.item
                        })
                        .then(response => {
                            if (response.status == 200) {
                                this.$emit('itemChanged');
                            }
                        })
                        .catch(error => {
                            console.log(error);
                        })
                }

            }
        }
    }

</script>

<style scoped>
    .completed {
        text-decoration: line-through;
        color: #999;

    }

    .itemText {
        width: 100%;
        margin-left: 20px;
    }

    .item {
        border-bottom: 1px solid #999;
        padding-top: 10px;
        padding-bottom: 10px;
        display: flex;
        align-items: center;

    }

</style>
