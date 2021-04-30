<template>
  <div v-if="people.length !== 0">
    <div class="card inline" v-for="(person,i) in people" :key="person.id">
      <h3>{{i+1}}){{ person.firstName }} {{ person.lastName }}</h3>
      <button class="btn danger" @click="$emit('remove', person.id)">Удалить</button>
    </div>
  </div>
    <div class="card center" v-else>
      <p>Пока людей нет</p>
      <button class="btn" @click="$emit('load')">загрузить людей</button>
    </div>
</template>

<script>
export default {
  emits: ['load', 'remove'],
  props: ['people']
}
</script>

<style scoped>
.inline {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
