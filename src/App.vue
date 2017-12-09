<template>
    <div>
        <b-navbar toggleable="md" type="dark" variant="bootstrap">
            <div class="container">
                <b-navbar-brand href="#"><i class="fab fa-vuejs"></i> Bootstrap Vue Example</b-navbar-brand>

                <b-navbar-nav class="ml-auto">
                    <b-button size="sm" type="button" variant="success"><i class="fas fa-plus"></i> New User</b-button>
                </b-navbar-nav>
            </div>
        </b-navbar>

        <div class="container">
            <br>
            <b-table bordered striped hover :fields="fields" :items="items">
                <template slot="active" scope="data">
                    <b-badge v-if="data.item.isActive == true" variant="success">Active</b-badge>
                    <b-badge v-if="data.item.isActive == false" variant="secondary">Inactive</b-badge>
                </template>
                <template slot="actions" scope="data">
                    <b-button size="sm" variant="danger"><i class="fas fa-times"></i> Delete</b-button>
                </template>
            </b-table>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                fields: [
                    { key: 'active', label: 'Active' },
                    { key: 'age', sortable: true },
                    { key: 'first_name', sortable: true },
                    'last_name',
                    // A virtual column made up from two fields
                    { key: 'actions', label: 'Actions' }
                ],
                items: [
                    { isActive: true, age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
                    { isActive: false, age: 21, first_name: 'Larsen', last_name: 'Shaw' },
                    { isActive: false, age: 89, first_name: 'Geneva', last_name: 'Wilson' },
                    { isActive: true, age: 38, first_name: 'Jami', last_name: 'Carney' }
                ]
            }
        }
    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }

    .bg-bootstrap {
        background-color: rgb(86, 61, 124);
    }
</style>
