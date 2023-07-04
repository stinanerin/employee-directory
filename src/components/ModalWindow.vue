
<template>
    <div class="backdrop" @click="closeModal">
        <div class="modal" @click.stop >
            <h1>Opps! Something went wrong... </h1>
            <p>Please try again later</p>
        </div>
    </div>
</template>


<script>
    export default {
        methods: {
            closeModal() {
                this.$emit("close")
            }
        } 
    }
</script>

<style>
    .modal{
        width: 350px;
        padding: 2rem;
        margin: 100px auto;
        background-color: white;
        border-radius: 1rem;
    }
    .modal h1 {
        color: rgb(27, 145, 178);
    }
    .backdrop {
        top:0;
        position: fixed;
        background-color: rgba(0, 0, 0, 0.5);
        width: 100%;
        height: 100%;
    }
</style>