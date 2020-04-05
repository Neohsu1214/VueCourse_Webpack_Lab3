<template>
    <div class="component">
        <h3>You may edit the User here</h3>
        <p>Edit me!</p>
        <p> My age is {{ myAge }} </p>
        <button @click="updateAge">Update Age</button>
    </div>
</template>

<script>
    export default {
        props: {
            myAge: {
                type: Number
            }
        },
        methods: {
            updateAge: function() {
                this.myAge = 30;
                this.$emit('ageWasUpdated', this.myAge);
            }
        }
    }
</script>

<style scoped>
    div {
        background-color: lightgreen;
    }
</style>
