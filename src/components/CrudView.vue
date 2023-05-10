<template>
  <div>
    <div class="modal" v-if="openModal">
      <div class="modal-con">
        <div class="p-input">
          <form @submit.prevent="submitForm">
            <p>First name:</p>
            <input type="text" v-model="form.first_name" placeholder="John">
            
            <p>Last name:</p>
            <input type="text" v-model="form.last_name" placeholder="Doe">
            
            <p>Email:</p>
            <input type="email" v-model="form.email" placeholder="johndoe@example.com">
            
            <p>Image:</p>
            <!-- <input type="file"> -->
            <input type="type" v-model="form.avatar">

            <div class="form-btn">
              <button type="submit">Add</button>
            </div>
          </form>
        </div> 
      </div>
      <div class="close-btn">
        <button @click="closeModal">close</button>
      </div>
    </div>

    
    <div class="table-con">
      <table>
        <tr>
          <th>Id</th>
          <th>Avatar</th>
          <th>Name</th>
          <th>Email</th>
          <th colspan="3">Actions</th>
          
        </tr>
        <tbody>
          <tr v-for="user in profile" :key="user._id">
            <td>{{ user._id }}</td>
            <td><img :src="user.avatar" alt="profile picture"></td>
            <td>{{ user.first_name }} {{ user.last_name }}</td>
            <td>{{ user.email }}</td>
            <td><button @click="del(user._id)" class="del-btn">Delete</button></td>
            <router-link :to="{name: 'EditView', params:{id: user._id}}">
              <td>
                <button class="edit-btn">Edit</button>
              </td>
            </router-link>
          </tr>
        </tbody>
      </table>
      <!-- <div>
        <button @click="prev">Prev</button>
        <button @click="next">Next</button>
      </div> -->
    </div>
    <button @click="addUsers">Add Users</button>
  </div>
</template>

<script>
import { onMounted, reactive, ref, toRefs } from 'vue';
import axios from "../plugins/axios"

export default {
  name: 'CrudView',
  setup(){
    const openModal = ref(false)

    const state = reactive({
      profile:[],

      form:{
        first_name: '',
        last_name: '',
        email: '',
        avatar: ''
      }
    })

    onMounted(async()=>{
      const data = await axios.get(`/users`)
      console.log(data.data, "check")
      state.profile = data.data 
      // users.value = data
    })


    
    async function submitForm(){
      const profiles = await axios.post('/users', state.form)
      console.log(profiles.data)
      state.profile.push(profiles.data)
      openModal.value = false
      state.form = {
        first_name: '',
        last_name: '',
        email: '',
        avatar: ''
      }
    }


    function addUsers(){
      openModal.value = true
    }


    async function del(id){
      await axios.delete(`/users/${id}`)
      
      state.profile = state.profile.filter(user => user._id !== id)
    }

    function closeModal(){
      openModal.value = false
    }

    return{
      addUsers,
      del,
      openModal,
      closeModal,
      ...toRefs(state),
      submitForm,
    }
  }
}
</script>

<style scoped>
.table-con{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
table, th, td {
  border: 1px solid black;
}


td, th{
  padding: 1vh 2vw;
  text-align: center;
}

img{
  max-width: 6vw;
  border-radius: 50%;
}

.edit-btn, .del-btn{
  text-decoration: none;
  /* padding: 1vh 2vw; */
  text-align: center;
  cursor: pointer;
}

</style>

<!-- Add "scoped" attribute to limit CSS to this component only -->
