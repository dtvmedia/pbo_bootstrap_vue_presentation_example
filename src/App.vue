<template>
    <div>
        <!-- Navbar -->
        <b-navbar toggleable="md" type="dark" variant="bootstrap">
            <b-container>
                <b-navbar-brand href="#"><i class="fab fa-vuejs"></i> Bootstrap Vue Example</b-navbar-brand>
            </b-container>
        </b-navbar>

        <!-- Jumbotron + Main Buttons -->
        <b-jumbotron>
            <template slot="header">
                <b-container>
                    User Management
                    <div class="float-right">
                        <b-button size="lg" type="button" variant="success" v-b-modal.form_modal><i class="fas fa-plus"></i> New User</b-button>
                    </div>
                </b-container>
            </template>
        </b-jumbotron>

        <!-- Table -->
        <b-container>
            <b-table bordered striped hover class="user-table" :fields="fields" :items="items">
                <template slot="active" scope="row">
                    <b-badge v-if="row.item.isActive === true" variant="success">Active</b-badge>
                    <b-badge v-if="row.item.isActive === false" variant="secondary">Inactive</b-badge>
                </template>
                <template slot="actions" scope="row">
                    <b-button size="sm" variant="danger" v-on:click="deleteRow(row.index)"><i class="fas fa-times"></i> Delete</b-button>
                </template>
            </b-table>
        </b-container>

        <!-- Modal Form -->
        <b-modal id="form_modal" ref="form_modal_ref" title="Create new User" header-bg-variant="dark" header-text-variant="light" ok-variant="success" v-on:ok="handleOk">
            <template slot="modal-ok">
                <i class="fas fa-plus"></i> Create User
            </template>

            <b-form @submit="formSubmit">
                <b-form-group label="Your Firstname:">
                    <b-form-input type="text" v-model="form.firstname" placeholder="Firstname"></b-form-input>
                </b-form-group>
                <b-form-group label="Your Lastname:">
                    <b-form-input type="text" v-model="form.lastname" placeholder="Lastname"></b-form-input>
                </b-form-group>
                <b-form-group label="Your Age:">
                    <b-form-input type="number" v-model="form.age" placeholder="Age"></b-form-input>
                </b-form-group>
                <b-form-group>
                    <b-form-checkbox v-model="form.active">Active</b-form-checkbox>
                </b-form-group>
            </b-form>
        </b-modal>
    </div>
</template>

<script>
    export default {
        data: function() {
            return {
                /**
                 * Table Column Definitions
                 */
                fields: [
                    { key: 'active', label: 'Active' },
                    { key: 'first_name', sortable: true },
                    { key: 'last_name', sortable: true },
                    { key: 'age', sortable: true },
                    { key: 'actions', label: 'Actions' }
                ],
                /**
                 * Table Raw Data
                 */
                items: [
                    { isActive: true, age: 40, first_name: 'Jan', last_name: 'Turner' },
                    { isActive: false, age: 21, first_name: 'Katherine', last_name: 'Stewart' },
                    { isActive: false, age: 89, first_name: 'John', last_name: 'Henderson' },
                    { isActive: true, age: 38, first_name: 'Anne', last_name: 'Wilson' },
                    { isActive: true, age: 18, first_name: 'Robert', last_name: 'Pullman' },
                    { isActive: false, age: 24, first_name: 'Stephen', last_name: 'Clarkson' },
                    { isActive: true, age: 28, first_name: 'Caroline', last_name: 'Duncan' },
                ],
                /**
                 * Form Data Vars
                 */
                form: {
                    firstname: '',
                    lastname: '',
                    age: 0,
                    active: false
                },
            }
        },
        methods: {
            /**
             * Delete Table Row Function
             * @param index
             */
            deleteRow: function ( index ) {
                this.items.splice( index, 1 );
            },

            /**
             * Add Table Row Function
             * @param row
             */
            addRow: function ( row ) {
                this.items.push( row );
            },

            /**
             * Clear Form Function
             */
            clearForm: function () {
                this.form.firstname = '';
                this.form.lastname = '';
                this.form.age = 0;
                this.form.active = false;
            },

            /**
             * Form Submit Event Handler
             * @param event
             */
            formSubmit: function ( event ) {
                // Prevent browser from sending a http request
                event.preventDefault();

                this.addRow( {
                    isActive: this.form.active,
                    age: this.form.age,
                    first_name: this.form.firstname,
                    last_name: this.form.lastname
                } );

                this.clearForm();

                this.$refs.form_modal_ref.hide();
            },

            /**
             * Modal Ok Button Handler
             * @param event
             */
            handleOk: function ( event ) {
                // Prevent modal from closing
                event.preventDefault();

                if ( !this.form.firstname || !this.form.lastname ) {
                    alert( 'Please enter your name' )
                } else {
                    this.formSubmit( event )
                }
            },
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

    .user-table {
        margin-top: 30px;
    }
</style>
