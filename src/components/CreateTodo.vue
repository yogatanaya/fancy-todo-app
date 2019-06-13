<template>
  <div class="md-layout md-alignment-center">
    <form @submit="createTodo">
      <md-field>
        <label>Task</label>
        <md-input v-model="title"></md-input>
      </md-field>
      <div>
        <md-button class="md-raised md-primary"
        type="submit"
        value="Save"
        >
          Save
        </md-button>
      </div>
    </form>
  </div>
</template>

<script>
import uuid from 'uuid';

export default {
  name: "CreateTodo",
  data() {
    return {
      title: ''
    }
  },
  methods:{
    createTodo(e) {
      e.preventDefault();
      const newTodo = {
        title: this.title,
        completed: false,
      }
      // send to parent
      this.$emit('createTodo', newTodo);
      this.title = ''
    }
  }
}

</script>

<style scoped>
  form { display: flex; justify-content: center; } 
  .md-layout {
    display: flex;
    justify-content: flex-start;
    margin-right: 40%;
  }

  @media only screen and (max-width: 800px) {
    .md-layout {
      display: flex;
      margin-right: 0;
    }
  }
</style>
