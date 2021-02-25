<template>

    <v-data-table :headers="headers" :items="users" >
          <template v-slot:top>
            <v-toolbar flat>
              <v-toolbar-title>Usuarios</v-toolbar-title>
                <v-divider class="mx-4" vertical></v-divider>

                <v-spacer></v-spacer>
              <v-dialog v-model="dialog" max-width="500px">
                <template v-slot:activator="{on, attrs}">
                  <v-btn color="primary" dark  v-bind="attrs" v-on="on">New Item</v-btn>
                </template>
                <v-card>
                  <v-card-title>
                     <span class="headline">{{ formTitle }}</span>
                  </v-card-title>
                  <v-card-text>
                      <v-text-field v-model="username" label="User"></v-text-field>
                      <v-text-field v-model="correo" label="coreo" type="email"></v-text-field>
                      <v-text-field v-model="password" label="Password"></v-text-field>
                      <v-text-field v-model="first_name" label="First Name"></v-text-field>
                      <v-text-field v-model="last_name" label="Last Name"></v-text-field>
                  </v-card-text>
                </v-card>
              </v-dialog>
            </v-toolbar>
          </template>
    </v-data-table>


</template>

<script>

  export default {
  async asyncData ({$http}) {
 const data = await $http.$get('/api/users')

  return { users: data }
},
    data: () => ({
        efrain:'',
        headers: [
            { text: 'Name', value: 'name',  },
            { text: 'Apellido', value: 'apellido' },
        ],
        dialog: false,
        formTitle: ''
    }),

  head () {
  return {
  title: 'Users'
}
},
methods : {
    save: async function (user){
      try {
            let send= await  $http.$post('/api/users', user)
            console.log(send);
      } catch (error){
          console.log(error)
      }

  }
}


}
</script>

<style scoped>
  .container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
  .title
  {
    margin: 30px 0;
  }
  .users
  {
    list-style: none;
    margin: 0;
    padding: 0;
  }
  .user
  {
    margin: 10px 0;
  }
  .button
  {
    display: inline-block;
    margin-top: 50px;
  }
</style>
