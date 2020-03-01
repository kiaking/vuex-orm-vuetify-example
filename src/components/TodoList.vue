<template>
  <v-card tile>
    <v-list-item>
      <v-list-item-title class="headline my-4">Todos</v-list-item-title>
    </v-list-item>

    <v-divider class="mx-4"></v-divider>

    <v-list>
      <template v-for="todo in todos">
        <v-list-item-group :key="todo.id" multiple>
          <v-list-item>
            <v-list-item-action>
              <v-checkbox />
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title>{{ todo.title }}</v-list-item-title>
              <v-list-item-subtitle>Assigned to {{ todo.assignee.name }}</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </template>
    </v-list>
  </v-card>
</template>

<script>
import Todo from '@/models/Todo'

export default {
  computed: {
    todos () {
      return Todo.query().with('assignee').orderBy('id', 'desc').get()
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
