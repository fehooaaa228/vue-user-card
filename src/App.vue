<template>
  <userCard v-bind:photoLink="photoLink" v-bind:nick="nick" v-bind:name="name" v-bind:surname="surname" v-bind:patronymic="patronymic" v-bind:address="address" v-bind:email="email" v-bind:phoneNum="phoneNum"></userCard>
  <button @click="getUserData">Обновить данные</button>
</template>

<script>
import userCard from './components/userCard.vue'

export default {
  name: 'App',
  components: {
    userCard
  },
  data(){
    return {
      photoLink: '../assets/70.jpg',
      nick: '',
      name: '',
      surname: '',
      patronymic: '',
      address: '',
      email: '',
      phoneNum: '',
    }
  },

  methods: {
    getUserData(){
      this.axios.get('https://randomuser.me/api/')
        .then((response) => {
          this.photoLink = response.data.results[0].picture.large;
          this.nick = response.data.results[0].login.username;
          this.name = response.data.results[0].name.title;
          this.surname = response.data.results[0].name.first;
          this.patronymic = response.data.results[0].name.last;
          this.address = response.data.results[0].location.city + ', ' + response.data.results[0].location.street.name + ' ' + response.data.results[0].location.street.number;
          this.email = response.data.results[0].email;
          this.phoneNum = response.data.results[0].phone;
        });
    }
  },

  mounted(){
    this.getUserData();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

button {
  display: flex;
  justify-content: flex-start;
  margin-left: 8px;
}
</style>
