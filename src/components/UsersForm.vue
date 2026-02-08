<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
    user: {
        type:Object,
        default: null
    }
});

const emit = defineEmits(['save','cancel']);

const name = ref('');
const username = ref('');
const email = ref('');
const phone = ref('');
const error =ref(null);

watch(  //inputs rellenados al editar
    ()=> props.user,
    (u) =>{
        if (u){
            name.value = u.name
            username.value = u.username
            email.value = u.email
            phone.value = u.phone
        }        
    },
    { immediate: true}
)

 //Aqui se valida el  email que se ingresa
const isValidEmail = (value)=>{  
    return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(value)
};

const saveUser = () =>{ //hay campos vacios?
    if(!name.value || !username.value || !email.value){
        error.value = 'Todos los campos obligatorios';
        return
    }

    if (!isValidEmail(email.value)){
        error.value = 'Email no válido';
        return
    }

    emit('save',{  //Almacenamiento de los valores nuevos
        ...props.user,
        name: name.value,
        username: username.value,
        email: email.value,
        phone: phone.value
    })

    //reset
    name.value = ''
    username.value = ''
    email.value = ''
    phone.value = ''
    error.value = null
};
</script>

<template>
    <div class="form-box">
        <h3>{{ user ? 'Edit User' : 'Add New User' }}</h3>
        <p v-if="error" style="color:red">{{ error }}</p>
        <label>Name: </label>
        <input v-model="name" />
        <label>Username:</label>
        <input v-model="username" />
        <label>Email:</label>
        <input v-model="email" />
        <label>Phone:</label>
        <input  v-model="phone" />

        <div class="actions">
            <button @click="saveUser">Save</button>
            <button @click="$emit('cancel')">Cancel</button>
        </div>
    </div>
</template>

<style scoped>

.form-box input{
    width: 100%;
    padding: 10px;
    margin-top: 10px;
    margin-bottom: 12px;
    border-radius: 6px;
    border: 1px solid #ddd;
    
}

.actions{
    display: flex;
    justify-content: flex-end;
    gap: 10px;
}
button{
    
    border-color:rgb(165, 163, 163);
    border-width: 3px;
    background-image: linear-gradient(rgb(235, 229, 229), rgb(145, 143, 143));
}
button:hover{
    background-image: linear-gradient(rgb(235, 229, 229), rgb(121, 119, 119));
}
</style>