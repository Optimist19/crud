<template>
	<div>
	  	<div class="modal">
		  	<div class="modal-con">
			  	<div class="p-input">
			  	<form @submit.prevent="submitFormUpdate">
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
				 	<button type="submit">Update</button>
				  </div>
			  	</form>
			  	</div> 
		  	</div>
		  	<div class="close-btn">
			  <router-link to="/"><button>Back</button></router-link>
		  	</div>
	  	</div>
	</div>
  </template>
  
<script>
	import {ref} from "vue"
	import {useRoute, useRouter} from "vue-router"
	import axios from "axios"

  	export default {
	name: "EditView",
  
	setup(){

		const form = ref({
			first_name: "",
			last_name: "",
			email: "",
		})

		const router = useRouter()
		const route = useRoute()
		const {id} = route.params
		
		async function submitFormUpdate(){
			console.log(id)
			// console.log(form.value)
			console.log("clicking is fine")
			let result = await axios.put("/users/"+id, form.value)
			console.log(result)
			router.push('/')
		}
		// 645a51dd6246ac03e853b340
  
		return{
		  submitFormUpdate,
		  form,
		}
	  }
  
}
</script>
  
<style>
  
</style>