<template>
  <v-app>
    <v-content>
      <v-app-bar app>
        <v-toolbar-title>Vuex ORM Vuetify Example</v-toolbar-title>
      </v-app-bar>

      <v-container class="pt-12 pb-12" id="home" tag="section">
        <v-row justify="center">
          <v-col cols="auto">
            <v-img
              class="mx-auto mb-10"
              src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-light.png"
              width="96"
            />
            <h1 class="headline">Vuex ORM Vuetify Todo App</h1>
          </v-col>
        </v-row>

        <v-row class="mt-8">
          <v-col :cols="4">
            <UserList />
          </v-col>

          <v-col :cols="8">
            <TodoList />
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import data from '@/data'
import User from '@/models/User'
import UserList from '@/components/UserList.vue'
import TodoList from '@/components/TodoList.vue'

export default {
  name: 'App',

  components: {
    UserList,
    TodoList
  },

  created () {
    // Here we are stubbing the initial data. In the real world, this
    // should be the response from the API Backend.
    const initialData = data

    User.insert({ data: initialData })
  }
}
</script>
