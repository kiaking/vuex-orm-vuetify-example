<template>
  <v-card tile>
    <v-list-item>
      <v-list-item-title class="headline my-4">Todos</v-list-item-title>
    </v-list-item>

    <v-divider class="mx-4"></v-divider>

    <v-list>
      <template v-for="todo in todos">
        <v-list-item-group :key="todo.id">
          <v-list-item>
            <v-list-item-action>
              <v-checkbox :value="todo.done" @click.stop="toggle(todo)" />
            </v-list-item-action>

            <v-list-item-content>
              <v-text-field
                :value="todo.title"
                placeholder="Untitled Task"
                :messages="[`Assigned to ${todo.assignee.name}`]"
                @input="v => { update(todo, v) }"
              />
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
