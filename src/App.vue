<template>
  <v-app>
   

    <v-content>
      <Todo></Todo>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import Todo from "./components/Todo.vue"

export default {
  name: 'App',
  components: {
    HelloWorld, Todo
  },
  data: () => ({
    //
  }),
};
</script>
