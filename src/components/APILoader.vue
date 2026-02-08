<script setup>
import { ref } from 'vue';


const emit = defineEmits(['loaded','error']);

const apiUrl = ref('');
const loading = ref(false); //está cargando la API




const loadApi = async ()=>{
    
    loading.value = true;
    
        
    try{
        //delay (solo para mostrar loading)
        await new Promise(resolve => setTimeout(resolve,2000));

        const response = await fetch(apiUrl.value);
        if(!response.ok){
            throw new Error('Error al cargar la API');
        }
        const data = await response.json();
        
        emit('loaded',data);

        
    }catch (err) {
        emit('error', err.message);
    } finally {
        loading.value = false;
        
        
    }
};
</script>

<template>
    <div class="api-page">
        <div class="api-card">
            <h2>Connect API</h2>

            <!--FORM API LOADER-->
            <form v-if="!loading" @submit.prevent="loadApi">
                <input type="text" v-model="apiUrl" placeholder="Enter API">
                <button type="submit" class="btn-load">Load Users</button>
            </form>
            <!--LOADING-->
            <p v-else >Loading...</p>
        </div>        
    </div>    
</template>

<style scoped>
.api-page {
    height:100vh;
    padding-top: 5rem;
}
.api-card {
    margin: auto;
    background:white;
    padding:32px;
    width:380px;
    border-radius: 10px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.08);
    text-align: center;
}
.api-card input {
    width: 100%;
    padding: 10px;    
    margin-bottom: 20px;
    border-radius: 6px;
    border: 1px solid #ddd;
}
.btn-load {
    background-color:rgb(11, 141, 248);
    border-color:rgb(11, 141, 248);
    border-width:3px; 
    background-image: linear-gradient(rgb(85, 174, 247),rgb(25, 148, 248));
    color:white;
    width: 100%;
}
.btn-load:hover{
    background-image: linear-gradient(rgb(85, 174, 247),rgb(3, 121, 218));
}
</style>