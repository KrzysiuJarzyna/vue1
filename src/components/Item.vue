<template>
    <div class="forms">
            <span>{{item.name}}</span> ilość: <span>{{item.quantity}}</span>
            <button v-on:click="deleteTask(index)"> usuń </button>
    </div>
</template>

<script>
    export default {
        name: 'Item',
        props: {
            item: Object
        },
        methods: {
            deleteTask: function (index) {
                this.$emit('delete-task', {index});
            }
        }
    }
</script>
