<template>
  <div class="container">
    <app-alert v-if="alert" :alert="alert" @close="alert = null"></app-alert>
    <form class="card" @submit.prevent="createPerson">
      <h2>Работа с базой данных</h2>
      <div class="form-control">
        <label for="name">Введите имя</label>
        <input type="text" id="name" v-model.trim="form.firstName">
      </div>
      <div class="form-control">
        <label for="lastname">Введите фамилию</label>
        <input type="text" id="lastname" v-model.trim="form.lastName">
      </div>
      <button class="btn primary" :disabled="form.lastName.length === 0">Создать человека</button>
    </form>
    <AppLoader v-if="load"/>
    <AppPeopleList v-else :people="people" @load="loadPeople" @remove="removePerson"/>
  </div>
</template>

<script>
import AppPeopleList from "./AppPeopleList";
import AppAlert from "./AppAlert";
import AppLoader from "./AppLoader"

import axios from 'axios'

export default {
  data() {
    return {
      form: {
        firstName: '',
        lastName: ''
      },
      people: [],
      alert: null,
      load: false
    }
  },
  mounted() {
    this.loadPeople()
  },
  methods: {
   async createPerson() {
      const person = await fetch('https://vue-with-http-e97b6-default-rtdb.firebaseio.com/people.json', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(this.form)
      })

      const firebaseData = await person.json()

     this.people.push({
       id: firebaseData.name,
       firstName: this.form.firstName,
       lastName: this.form.lastName
     })

     this.form.firstName = ''
     this.form.lastName = ''

     console.log(firebaseData)
    },
    async loadPeople() {
     try {
       this.load = true
       const {data} = await axios.get('https://vue-with-http-e97b6-default-rtdb.firebaseio.com/people.json')
       this.people = Object.keys(data).map(key => {
         return {
           id: key,
           ...data[key]
         }
       })
     } catch (e) {
       this.alert = {
         type: 'danger',
         title: 'Ошбика!',
         text: e.message
       }
     }
      this.load = false
    },
    async removePerson(id) {
     const person = this.people.find(person => person.id === id).firstName
     await axios.delete('https://vue-with-http-e97b6-default-rtdb.firebaseio.com/people/'+ id +'.json')
      this.people = this.people.filter(person => person.id !== id)
      this.alert = {
       type: 'primary',
        title: 'Успешно!',
        text: `Пользователь с именем "${person}" успешно удален!`
      }
    }
  },
  components: {AppPeopleList, AppAlert, AppLoader}
}
</script>

<style>

</style>
