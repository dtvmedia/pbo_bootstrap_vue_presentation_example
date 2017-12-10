<template>
    <div>
        <!-- Navbar -->


        <!-- Jumbotron + Create Button -->


        <!-- Table -->


        <!-- Modal Form -->


    </div>
</template>

<script>
    export default {
        data: function () {
            return {
                /**
                 * Table Column Definitions
                 */
                fields: [

                ],
                /**
                 * Table Raw Data
                 */
                items: [
                    { id: 1, isActive: true, age: 40, first_name: 'Jan', last_name: 'Turner' },
                    { id: 2, isActive: false, age: 21, first_name: 'Katherine', last_name: 'Stewart' },
                    { id: 3, isActive: false, age: 89, first_name: 'John', last_name: 'Henderson' },
                    { id: 4, isActive: true, age: 38, first_name: 'Anne', last_name: 'Wilson' },
                    { id: 5, isActive: true, age: 18, first_name: 'Robert', last_name: 'Pullman' },
                    { id: 6, isActive: false, age: 24, first_name: 'Stephen', last_name: 'Clarkson' },
                    { id: 7, isActive: true, age: 28, first_name: 'Caroline', last_name: 'Duncan' },
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
             * @param delete_id
             */
            deleteRow: function ( delete_id ) {
                this.items = this.items.filter( function ( item ) {
                    return item.id !== delete_id;
                } );
            },

            /**
             * Add Table Row Function
             * @param row
             */
            addRow: function ( row ) {
                this.items.push( row );
            },

            /**
             * Returns the next auto increment id
             * @return int
             */
            getNextAutoId: function () {
                if ( this.items.length === 0 ) {
                    return 0;
                }

                return this.items[ this.items.length - 1 ].id + 1;
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
             */
            submitForm: function () {
                this.addRow( {
                    id: this.getNextAutoId(),
                    isActive: this.form.active,
                    age: this.form.age,
                    first_name: this.form.firstname,
                    last_name: this.form.lastname
                } );

                this.clearForm();
            }
        }
    }
</script>

<style>
    .bg-bootstrap {
        background-color: rgb(86, 61, 124);
    }
</style>
