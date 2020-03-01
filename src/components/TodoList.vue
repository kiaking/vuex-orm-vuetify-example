<template>
  <v-card tile>
    <v-list-item>
      <v-list-item-title class="headline my-4">Todos</v-list-item-title>
    </v-list-item>

    <v-divider class="mx-4"></v-divider>

    <v-list>
      <template v-for="todo in todos">
        <v-row :key="todo.id">
          <v-col :cols="8">
            <v-list-item-group>
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
          </v-col>

          <v-col class="mt-3" :cols="4">
            <div class="pr-4">
              <v-select
                label="Assignee"
                :items="assignees"
                :value="todo.assignee.id"
                @change="v => { updateAssignee(todo, v) }"
              />
            </div>
          </v-col>
        </v-row>
      </template>
    </v-list>
  </v-card>
</template>

<script>
import User from '@/models/User'
import Todo from '@/models/Todo'

export default {
  computed: {
    todos () {
      return Todo.query().with('assignee').orderBy('id', 'desc').get()
    },

    assignees () {
      return User.query().orderBy('name', 'asc').get().map((user) => {
        return { text: user.name, value: user.id }
      })
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
    },

    updateAssignee (todo, id) {
      todo.$update({ user_id: id })
    }
  }
}
</script>
