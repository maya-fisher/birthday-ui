<template>
    <div class="backdrop" @click.self="closeModel">
        <div class="model">
            <slot>default content</slot>
        </div>
    </div>
</template>

<script>
export default {
    methods: {
        closeModel() {
            // console.log('click pressed')
            this.$emit('close')
        }

        
    }
}

</script>

<style>
    .model {
        width: 400px;
        padding: 20px;
        margin: 100px auto;
        background: burlywood;
        border-radius: 10px;
    }
    .backdrop {
        top: 0;
        position: fixed;
        background: rgba(0, o, o, 0.5);
        width: 100%;
        height: 100%;
    }
    h1 {
        color: black;
        border: none;
        padding: 0;
    }
</style>


 