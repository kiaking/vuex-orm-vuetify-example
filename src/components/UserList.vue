<template>
  <v-card tile>
    <v-list-item>
      <v-list-item-title class="headline my-4">Users</v-list-item-title>
    </v-list-item>

    <v-divider class="mx-4"></v-divider>

    <template v-for="user in users">
      <v-list-item :key="user.id">
        <v-list-item-content>
          <v-text-field
            :value="user.name"
            placeholder="Unkown user"
            :messages="[`Assigned to ${user.todos.length} tasks`]"
            @input="v => { update(user, v) }"
          />
        </v-list-item-content>
      </v-list-item>
    </template>
  </v-card>
</template>

<script>
import User from '@/models/User'

export default {
  computed: {
    users () {
      return User.query().with('todos').orderBy('id', 'asc').get()
    }
  },

  methods: {
    update (user, name) {
      user.$update({ name })
    },

    destroy (user) {
      user.$delete()
    }
  }
}
</script>
