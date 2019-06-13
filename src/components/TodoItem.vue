<template>
  <md-card v-bind:class="{'is-complete':todo.completed}" class="md-default">
    <md-card-header>
      {{ todo.title }}
    </md-card-header>
    <md-card-actions>
      <md-checkbox type="checkbox" v-on:change="commitComplete"></md-checkbox>
      <md-button  class="md-raised md-accent" @click="$emit('del-todo',todo.id)">
        <i class="material-icons">delete</i>
      </md-button>
    </md-card-actions>
  </md-card>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    commitComplete() {
      this.todo.completed = !this.todo.completed
    }
  }
}
</script>

<style scoped>
  .is-complete { text-decoration: line-through; }
  .del { background-color: red; color:white; border: none; }
</style>

