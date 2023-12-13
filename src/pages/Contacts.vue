<script>
import { store } from '../data/store';
import axios from 'axios';
import Loader from '../components/Loader.vue';
    export default {
        name:'Contacts',
        components:{
            Loader
        },
        data(){
            return{
                name:'',
                email:'',
                message:'',
                errors: {
                    name:[],
                    email:[],
                    message:[]
                },
                success: false,
                isLoaded: false
            }
        },
        methods:{
            sendForm(){
                this.isLoaded = true;
                const data = {
                    name: this.name,
                    email: this.email,
                    message: this.message
                }

            axios.post(store.apiUrl + 'send-email', data)
                .then(res =>{
                    this.isLoaded = false;
                    console.log(res.data.success)
                    this.success = res.data.success;
                    if(!this.success){
                        this.errors = res.data.errors;
                    }
                })
                .catch(error =>{
                    console.log(error);
                })
            }
        }
    }

</script>



<template>

    <h1 class="text-center mb-5">Contacts</h1>

    <Loader v-if="isLoaded" />

    <div v-else>
        <form v-if="!success" @submit.prevent="sendForm()">
            <div class="mb-3">
                <label for="name" class="form-label">Name</label>
                <input v-model="name" type="text" class="form-control" id="name">
                <p class="text-warning" v-for="error in errors.name" >{{ error }}</p>
            </div>
            <div class="mb-3">
                <label for="email" class="form-label">Email address</label>
                <input v-model="email" type="email" class="form-control" id="email">
                <p class="text-warning" v-for="error in errors.email" >{{ error }}</p>
            </div>
            <div class="form-floating mb-3">
                <textarea v-model="message" class="form-control" placeholder="Leave a comment here" id="message" style="height: 100px"></textarea>
                <label for="message">Message</label>
                <p class="text-warning" v-for="error in errors.message" >{{ error }}</p>
            </div>
            <button type="submit" class="btn btn-primary">Submit</button>
        </form>
    
        <div class="container" v-else>
    
            <h3>The message has been successfully sent!</h3>
    
        </div>
    </div>
  
</template>


<style>

</style>