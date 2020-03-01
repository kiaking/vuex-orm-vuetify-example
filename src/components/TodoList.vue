<template>
  <v-card tile>
    <v-list-item>
      <v-list-item-title class="headline my-4">Todos</v-list-item-title>
    </v-list-item>

    <v-divider class="mx-4"></v-divider>

    <template v-for="todo in todos">
      <v-list-item :key="todo.id">
        <v-list-item-content>
          <v-list-item-title>{{ todo.title }}</v-list-item-title>
        </v-list-item-content>
      </v-list-item>

      <v-divider class="mx-4" :key="todo.id"></v-divider>
    </template>
  </v-card>
</template>

<script>
import Todo from '@/models/Todo'

export default {
  computed: {
    todos () {
      return Todo.query().orderBy('id', 'desc').get()
    }
  },

  methods: {
    toggle (todo) {
      todo.$update({ done: !todo.done })
    },

    update (todo, title) {
      todo.$update({ title })
    },

    destroy (todo) {
      todo.$delete()
    }
  }
}
</script>
