<template>

    <div>

        <div class="row">
            <div class="col">
                <input type="text" class="form-control" placeholder="Type your task" v-model="item.name" />
            </div>
            <div class="col-2">
                <button class="btn btn-primary" @click="addItem()" >
                    <font-awesome-icon icon="plus-square" />
                </button>
            </div>
        </div>

    </div>

</template>

<script>
    export default {
        data: function () {
            return {
                item: {
                    name: ""
                }
            }
        },
        methods: {
            addItem() {
                if (this.item.name == '') {

                    return;
                }
                axios.post('api/items/store', {
                        item: this.item
                    })
                    .then(response => {
                        if (response.status == 201) {
                            this.$emit('reloadList');
                            this.item.name = "";
                        }
                    })
                    .catch(error => {
                        console.log(error);
                    })
            }
        }
    }

</script>
