 

<template>
    <div class="overlay" >
        <div class="modal">
            <slot /> <!--AQUI VA EL FORMULARIO CREAR/EDITAR -->
        </div>
    </div>
</template>

<script setup>
defineEmits(['close'])
</script>

<style scoped>
.overlay{
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
}

.modal{
    background: white;
    padding:24px;
    border-radius: 12px;
    width: 90%;
    /*min-width:460px;*/
    max-width:420px;
    box-shadow: 0 20px 40px rgba(0,0,0,0.2);
}
</style>