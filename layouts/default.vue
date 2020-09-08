<template>
  <v-app app dark>
    <v-navigation-drawer app v-model="drawer">
      <v-list subheader>
        <v-subheader>List of People in room</v-subheader>
        <v-list-item
          v-for="user in users"
          :key="user.id"
          @click.prevent
        >

          <v-list-item-content>
            <v-list-item-title >{{user.name}}</v-list-item-title>
          </v-list-item-content>

          <v-list-item-icon>
            <v-icon :color="user.id === 2 ? 'primary' : 'grey'">chat_bubble</v-icon>
          </v-list-item-icon>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar app prominent extended>
      <v-toolbar-side-icon @click="drawer = !drawer">

      </v-toolbar-side-icon>
      <v-btn icon @click="exit">
        <v-icon>arrow_back</v-icon>
      </v-btn>
      <v-toolbar-title>Chat of room {{ user.room }}</v-toolbar-title>
    </v-toolbar>
    <div>
      <nuxt/>
    </div>
  </v-app>
</template>

<script>
import {mapState, mapMutations} from 'vuex'

export default {
  computed: mapState(['user']),
  data: () => ({
    drawer: true,
    users: [
      {id: 1, name:'User1'},
      {id: 2, name:'User2'}
    ]
  }),
  methods: {
    ...mapMutations(['clearData']),
    exit() {
      this.$router.push('/?message=leftChat')
      this.clearData()
    }
  }
};
</script>
