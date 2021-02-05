<template>
    <div class="todoListContainer">
        <br>
        <br>
        <h3 class="text-center">Todo List </h3>
        <div class="card">
            <div class="card-header">
                <add-item-form   v-on:reloadList="getList()"/>
            </div>

            <div class="card-body">
                <list-view :items="items" 
                v-on:reloadList="getList()"
                />

            </div>

        </div>


    </div>
</template>

<script>
    import addItemForm from "./addItemForm"
    import AddItemForm from './addItemForm.vue'

    import listView from './listView'
    export default {
        components: {
            addItemForm,
            listView


        },
        data: function () {
            return {
                items: [],
                edit: false
            }
            
        },
        methods: {
            getList() {
                axios.get('api/items')
                    .then(response => {
                        this.items = response.data
                    })
                    .catch(error => {
                        console.log(error);
                    })
            }
        },
        created() {
            this.getList();
        }

    }

</script>


<style scoped>
    .todoListContainer {
        width: 500px;
        margin: auto;
    }

    .card {
        position: relative;
        display: -webkit-box;
        display: -ms-flexbox;
        display: flex;
        -webkit-box-orient: vertical;
        -webkit-box-direction: normal;
        -ms-flex-direction: column;
        flex-direction: column;
        min-width: 0;
        word-wrap: break-word;
        background-color: #fff;
        background-clip: border-box;
        border: 1px solid rgba(0, 0, 0, .125);
        border-radius: .25rem;
    }

    .card-body {
        -webkit-box-flex: 1;
        -ms-flex: 1 1 auto;
        flex: 1 1 auto;
        padding: 1.25rem;
    }

    .card-header {
        padding: .75rem 1.25rem;
        margin-bottom: 0;
        background-color: rgba(0, 0, 0, .03);
        border-bottom: 1px solid rgba(0, 0, 0, .125);
    }

</style>
