<template>
    <div class="todo-header">
        <h3 aria-label="Todo form title">{{!isEdit ? "Add" : "Update"}} Todo</h3>
    </div>
</template>

<script>
    export default {
        props: {
            isEdit: {
                type: Boolean,
                default: false
            }
        }
        
    }
</script>

<style scoped>
.todo-header {
    width: fit-content;
    margin: 0 auto;
}
</style>