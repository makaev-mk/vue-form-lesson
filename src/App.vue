<template>
  <div class="container">
    <form class="card" @submit.prevent="eventHendler">
      <h1>Анкета на Vue разработчика!</h1>
      <div class="form-control">
        <label for="name">Как тебя зовут?</label>
        <input type="text"
               id="name"
               placeholder="Введи имя"
               v-model.trim="name"
        >
      </div>

      <div class="form-control">
        <label for="age">Выбери возраст</label>
        <input type="number"
               id="age"
               max="70"
               v-model.number ="age"
        >
      </div>

      <div class="form-control">
        <label for="city">Твой город</label>
        <select id="city" v-model="city">
          <option value="spb">Санкт-Петербург</option>
          <option value="msk">Москва</option>
          <option value="kzn">Казань</option>
          <option value="nsk">Новосибирск</option>
        </select>
      </div>

      <div class="form-checkbox">
        <span class="label">Готов к переезду в Токио?</span>
        <div class="checkbox">
          <label><input type="radio" v-model="relocate" name="trip" value="yes"/> Да</label>
        </div>

        <div class="checkbox">
          <label><input type="radio" v-model="relocate" name="trip" value="no"/> Нет</label>
        </div>
      </div>

      <div class="form-checkbox">
        <span class="label">Что знаешь во Vue?</span>
        <div class="checkbox">
          <label><input type="checkbox" value="vuex" name="skills" v-model="skills"/> Vuex</label>
        </div>
        <div class="checkbox">
          <label><input type="checkbox" value="cli" name="skills" v-model="skills"/> Vue CLI</label>
        </div>
        <div class="checkbox">
          <label><input type="checkbox" value="router" name="skills" v-model="skills"/> Vue Router</label>
        </div>
      </div>
      <div class="form-checkbox">
        <span class="label">Правила компании</span>
        <div class="checkbox">
          <label><input type="checkbox" v-model="agree"/> С правилами согласен</label>
        </div>
      </div>

      <button type="submit" class="btn primary">Отправить</button>
    </form>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        name: '',
        age: 23,
        city: 'spb',
        relocate: null,
        skills: [],
        agree: false
      }
    },
    methods: {
      eventHendler() {
        console.group('form data')
          console.log('name:', this.name)
          console.log('age:', this.age)
          console.log('city:', this.city)
          console.log('to Tokyo:', this.relocate)
          console.log('Skills:', this.skills)
          console.log('Agree:', this.agree)
        console.groupEnd()
      }
    }
  }
</script>

<style>

</style>
