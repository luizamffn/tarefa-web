<template>
  <v-container>
    <v-row class="">
      <v-col class="mb-4" cols="12">
        <h5 class="display-1 font-weight-bold">
          Tarefas
        </h5>

        <v-divider style="margin-bottom:20px"></v-divider>

        <v-text-field v-model="first" label="Título" outlined/>

        <div style="width:fit-content; float:right">  
          <v-btn depressed color="primary">
            Primary
          </v-btn>
          <v-btn depressed color="error">
            Error
          </v-btn>
        </div>  

        <v-card tile style="width: -webkit-fill-available; margin-top: 50px;">
            <v-simple-table>
              <template v-slot:default>
                <thead>
                  <tr>
                    <th class="text-left">
                      Name
                    </th>
                    <th class="text-left">
                      Calories
                    </th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="item in desserts" :key="item.name" >
                    <td>{{ item.name }}</td>
                    <td>{{ item.calories }}</td>
                    <td>{{ item.teste }}</td>
                  </tr>
                </tbody>
              </template>
            </v-simple-table>
        </v-card>
      </v-col>

      <v-col class="mb-4" cols="12">
        <h5 class="display-1 font-weight-bold">
          Nova Tarefa
        </h5>

        <v-divider style="margin-bottom:20px"></v-divider>

        <v-row>
          <v-col cols="12" sm="6" style="padding-top:0px; padding-bottom:0px">
            <v-text-field v-model="first" label="First Name" outlined></v-text-field>
          </v-col>

          <v-col cols="12" sm="6" style="padding-top:0px; padding-bottom:0px">
            <v-text-field v-model="first" label="First Name" outlined></v-text-field>
          </v-col>
        </v-row>

        <v-row>
          <v-col cols="12" sm="6" style="padding-top:0px; padding-bottom:0px">
            <v-text-field v-model="first" label="First Name" outlined></v-text-field>
          </v-col>
        </v-row>

        <v-btn depressed color="primary">
            Voltar
        </v-btn>
        <div style="width:fit-content; float:right">  
          <v-btn depressed color="primary">
            Salvar
          </v-btn>
        </div>  
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',
    data: () => ({
      desserts: [
          {
            name: 'Frozen Yogurt',
            calories: 159,
            teste: 'Teste',
          },
          {
            name: 'Ice cream sandwich',
            calories: 237,
            teste: 'Teste',
          },
          {
            name: 'Eclair',
            calories: 237,
            teste: 'Teste',
          },
        ],
    }),
  }
</script>
