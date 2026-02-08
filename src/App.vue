<script setup>
import { ref } from 'vue';
import APILoader from './components/APILoader.vue';
import UsersTable from './components/UsersTable.vue';
import UsersForm from './components/UsersForm.vue';
import Modal from './components/Modal.vue';

const users = ref([]);
const error = ref(null);
const step = ref('form'); //controla la vista del formulario api
const showAddForm =ref(false); //controla la vista del formulario users
const editingUser = ref(null);

const startEdit = (user) => {
  showAddForm.value = false
  editingUser.value = {...user} //copia segura
};

//SAVE UPDATE
const saveEdit = (updatedUser) =>{
  const index = users.value.findIndex(u => u.id === updatedUser.id);
  if (index !== -1){
    users.value[index] = updatedUser;
  }
  editingUser.value = null
};

//ADD USER
const addUsers = (user) => {
  const maxId = users.value.length ? Math.max(...users.value.map(u=>u.id)) : 0;

  users.value.push({
    id: maxId + 1,
    ...user
  });
  showAddForm.value = false;
};

//DELETE USER
const deleteUser = (id)=>{
  const user = users.value.find(u => u.id === id);
  if(!user) return

  const confirmed = confirm(
    `You are going to delete the user "${user.name}" .\nAre you sure?`
  );

  if (confirmed){
    users.value = users.value.filter(u => u.id !== id)
  }
};

</script>

<template>
  <div class="app">
    <h1>User Management</h1>

    <!--FORM API-->
    <APILoader 
      v-if="step ==='form'"
      @loaded="users = $event; step='table'"
      @error="error = $event"
    />
    <!--Toolbar-->      
    <div v-if="step === 'table'">
      <div class="toolbar">
        <h2>Registered Users</h2>
        <div>
          <button @click="showAddForm = true" class="btn-new">+ New User</button>
          <button @click="step = 'form'; users=[]" class="btn-change">Change API</button>
        </div>
      </div>
      
      <!--FORMULARIO DE NUEVO USUARIO-->
      <Modal v-if="showAddForm" @close="showAddForm=false">
        <UsersForm                
          @save="addUsers"
          @cancel="showAddForm = false"        
        />
      </Modal>
      
      <!--FORMULARIO EDITAR USUARIO-->
      <Modal v-if="editingUser" @close="editingUser=false">
        <UsersForm           
          :user="editingUser"
          @save="saveEdit"
          @cancel="editingUser = null"
        />
      </Modal>
      
      <!--TABLA USUARIOS-->
      <UsersTable 
      v-if="users.length"
      :users="users"
      @edit="startEdit" 
      @delete="deleteUser"   
      />      
    </div>    
    <p v-if="error" style="color:red">{{ error }}</p>     
  </div>
</template>

<style scoped>
.app{
  max-width:70rem;
  margin: 0 auto;
  
}
h1{
  text-align: center;
  margin-bottom: 2.5rem;
  color:rgb(3, 23, 78);
}
.toolbar {
  display:flex;
  
  flex-wrap: wrap;
  justify-content:space-between; 
  align-items: center;
  margin-bottom: 20px;
}
.toolbar h2{
  width: 100%;
  color:rgb(3, 23, 78);
}

.btn-new{
  background-color: rgba(0, 128, 0, 0.445);
  border-color: rgb(89, 248, 89);
  background-image: linear-gradient(rgb(89, 248, 89),rgb(46, 245, 56));
  border-width:3px;
  color:black;
}
.btn-new:hover{
  background-image: linear-gradient(rgb(89, 248, 89),rgb(11, 202, 11));
}
.btn-change {
  margin-left:12px; 
  background-color:rgb(11, 141, 248);
  border-color:rgb(11, 141, 248);
  border-width:3px; 
  background-image: linear-gradient(rgb(85, 174, 247),rgb(25, 148, 248));
}

.btn-change:hover{
  background-image: linear-gradient(rgb(85, 174, 247),rgb(3, 121, 218));
}
@media (min-width: 768px) {
  .toolbar h2 {
    width: auto;
  }
}
</style>