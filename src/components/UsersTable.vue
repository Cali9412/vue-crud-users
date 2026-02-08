<script setup>
defineProps({
    users:Array
})

const emit = defineEmits(['edit', 'delete']);
</script>

<template>
   <div class="table-wrapper">
    
    <table class="users-table">
        <thead>
            <tr>
                <th>Name</th>
                <th>Username</th>
                <th>Email</th>
                <th>Phone</th>
                <th>Actions</th>
            </tr>
        </thead>
        
        <tbody>
            <tr v-for="user in users" :key="user.id">
                <td>{{ user.name }}</td>
                <td>{{ user.username }}</td>
                <td>{{ user.email }}</td>
                <td>{{ user.phone }}</td>
                <td>
                   <button @click="$emit('edit', user)" class="btn-edit">✏️ Edit</button> 
                    <button @click="$emit('delete',user.id)" class="btn-del">🗑️ Delete</button>
                </td>
            </tr>
        </tbody>
    </table>
   </div> 
</template>

<style scoped>
.table-wrapper{
    width: 100%;
    overflow-x:auto;
}
.users-table {
    min-width: 700px;
    width:100%;
    border-collapse: collapse;
    background: white;
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0 6px 20px rgba(0,0,0,0.05);
    margin-bottom: 2rem;
}
.users-table th {
    background: #464849;
    text-align: center;
    padding: 12px;
    font-size: 13px;
    text-transform: uppercase;
    color:#fdfeff;
}

.users-table td{
    padding:12px;
    border-top: 1px solid #2e2d2d;
    text-align: center;
}

.users-table tr:hover {
    background: #f4f6f8;
}

.users-table button {
    margin-right: 6px;
    margin-top:4px;
    margin-bottom: 4px;    
}
.btn-edit{
    background-color: rgb(241, 192, 101);
    border-color:rgb(241, 192, 101);
    border-width: 3px;
    background-image: linear-gradient(#fecc4c, #ffac33);
}
.btn-del{
    background-color: rgb(240, 89, 89);
    border-color:rgb(240, 89, 89);
    border-width: 3px;
    background-image: linear-gradient(#ff737a, #dd575d);
}

.btn-edit:hover{
    background-image: linear-gradient(#ffcc4c, #f89808);
}

.btn-del:hover {
    background-image: linear-gradient(#ff737a,#cc3139);
}
</style>