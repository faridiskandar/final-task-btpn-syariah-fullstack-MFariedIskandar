<template>
    <div class="body">
        <h1>Profile</h1>
        <div class="profile-container">
            <img src="../assets/logo.svg" alt="img">
            <div class="profile">
                <h3>{{ profile.name }}</h3>
                <div class="set">
                    <div class="change">
                        <form @submit.prevent="ChangeProfile" method="post">
                            <input type="file" name="img">
                            <button type="submit">Change</button>
                        </form>
                    </div>
                    <button @click="DeleteProfile">Delete img</button>
                </div>
            </div>
        </div>

        <h3>users :</h3>
        <div class="card-container">
            <div class="card" v-for="profile in profiles" :key="profile.id">
                <img :src="'uploads/' + profile.profle_pictures" alt="img">
                <h3>{{ profile.name }}</h3>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {

    data() {
        return {
            profiles: [],
            profile: {}
        }
    },

    methods: {
        ChangeProfile() {
            axios.put('/profile_picture', this.profile.profile_picture)
                .then((response) => {
                    console.log(response.data)
                }).catch((error) => {
                    console.log(error.response)
                })
            console.log('change')
        },

        DeleteProfile() {
            axios.delete('/profile_picture')
                .then((response) => {
                    console.log(response.data)
                }).catch((error) => {
                    console.log(error.response)
                })
            console.log('delete')
        }
    },

    mounted() { 
        axios.get('/profile')
            .then((response) => {
                this.profile = response.data
                console.log(this.profile)
            }).catch((error) => {
                console.log(error.response)
            })

        axios.get('/profiles')
            .then((response) => {
                this.profiles = response.data
                console.log(response.data)
        }).catch((error) => {
            console.log(error.response)
            console.log("errorr cuyy")
        })
    }
}
</script>

<style>
.body{
    background-color: rgb(0, 0, 0);
    height: 100vh;
    width: 100%;
    padding: 20px;
    color:aliceblue;
}
.profile-container{
    display: grid;
    grid-template-columns: 1fr 1fr;
    background-color: rgb(27, 27, 27);
    padding: 1em;
    border-radius: 15px;
    margin-bottom: 3em;
}
.profile-container img{
    width: 100px;
    height: 100px;
    border-radius: 50%;
    object-fit: cover;
    box-shadow: 0px 5px 15px 0px rgba(124, 124, 124, 0.5);
}
.profile{
    padding: 10px;
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr 1fr;
}
.set{
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
}
.change input{
    max-width: 90px;
}
button{
    padding: 10px;
    border-radius: 10px;
    border: none;
    color: aliceblue;
    background-color: rgb(31, 30, 30);
    transition: 0.3s;
}
button:hover{
    cursor: pointer;
    background-color: rgb(44, 44, 44);
      box-shadow: 0px 5px 15px 0px rgba(124, 124, 124, 0.5);
}
.card-container{
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
}
.card{
    padding: 1rem;
    display: grid;
    grid-template-columns: 1fr 1fr;
    background-color: rgb(225, 235, 235);
    height: 80px;
    color: black;
    border-radius: 15px;
    max-width: 400px;
}
.card img{
    width:50px;
    height: 50px;
    border-radius: 50%;
    object-fit: cover;
    box-shadow: 0px 5px 15px 0px rgba(124, 124, 124, 0.5);
}
</style>