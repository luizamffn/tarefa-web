<template>
  <v-container>
    <v-row class="">
      <v-col class="mb-4" cols="12">
        <h5 class="display-1 font-weight-bold">
          Tarefas
        </h5>

        <v-divider style="margin-bottom:20px"></v-divider>

        <v-text-field v-model="titulo" label="Título" outlined/>

        <div style="width:fit-content; float:right">
          <v-btn depressed color="orange darken-2" v-on:click="recuperarTarefas">
            <v-icon left>
              mdi-eraser
            </v-icon>
            Limpar
          </v-btn>  
          <v-btn v-on:click="pesquisar" color="primary" style="margin-left: 10px">
            <v-icon left>
              mdi-magnify
            </v-icon>
            Consultar
          </v-btn>
          <v-btn color="green darken-2" style="margin-left: 10px">
            <v-icon left>
              mdi-plus
            </v-icon>
            Nova Tarefa
          </v-btn>
        </div>  

        <v-card tile style="width: -webkit-fill-available; margin-top: 50px;">
            <v-simple-table>
              <template v-slot:default>
                <thead>
                  <tr>
                    <th class="text-left">
                      Titulo
                    </th>
                    <th class="text-left">
                      Descrição
                    </th>
                    <th class="text-left">
                      Data criação
                    </th>
                    <th class="text-left">
                      Ações
                    </th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="item in tarefas" :key="item.name" >
                    <td>{{ item.titulo }}</td>
                    <td>{{ item.descricao }}</td>
                    <td>{{ item.dataCriacao }}</td>
                    <td>
                      <v-icon color="yellow darken-2" style="font-size: 20px !important;">
                        mdi-square-edit-outline
                      </v-icon>

                      <v-dialog :key="item.id" v-model="showDialogDelet" persistent max-width="300">
                        <template v-slot:activator="{ on, attrs }">
                          <v-icon left v-bind="attrs" v-on="on" color="red darken-2" style="font-size: 20px !important;">
                              mdi-delete
                            </v-icon>
                        </template>
                        <v-card>
                          <v-card-title class="text-h5">
                            Você realmente deseja remover está tarefa?
                          </v-card-title>
                          <v-card-actions>
                            <v-spacer></v-spacer>
                            <v-btn style="background-color: red;" text @click="deletar(item)" >
                              Sim
                            </v-btn>
                            <v-btn style="background-color: green;" text @click="showDialogDelet = false" >
                              Não
                            </v-btn>
                          </v-card-actions>
                        </v-card>
                      </v-dialog>

                    </td>
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
            <v-text-field v-model="tarefa.titulo" label="Titulo" outlined></v-text-field>
          </v-col>

          <v-col cols="12" sm="6" style="padding-top:0px; padding-bottom:0px">
            <v-text-field v-model="tarefa.descricao" label="Descrição" outlined></v-text-field>
          </v-col>
        </v-row>

        <v-row>
          <v-col cols="12" sm="6" style="padding-top:0px; padding-bottom:0px">
            <v-select v-model="tarefa.statusTarefa" 
              :items="items" item-text="status"
              item-value="value" label="Status" outlined ></v-select>
          </v-col>
        </v-row>

        <v-btn>
            <v-icon left style="color:black">
              mdi-keyboard-return
            </v-icon>

            <div style="color:black">
            Voltar
            </div>
        </v-btn>
        <div style="width:fit-content; float:right">  
          <v-btn color="green darken-2" v-on:click="cadastrar">
            <v-icon left>
              mdi-content-save
            </v-icon>
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
    showDialogDelet: false,
    data: () => ({
      titulo: "",
      tarefa : {titulo: '', descricao: '', statusTarefa: ''},
      tarefas: [],
      items: [
          { status: 'Aberta', value: 'ABERTA' },
          { status: 'Em andamento', value: 'EM_ANDAMENTO' },
          { status: 'Concluída', value: 'CONCLUIDA' },
        ],

    }),
    mounted () {
      this.recuperarTarefas()
    },
    methods: {
      recuperarTarefas: function(){
        var that = this
        that.axios.get("http://localhost:8080/tarefas")
        .then(function (response) {
          that.tarefas = response.data.content
        })
        .catch(function (error) {
          console.log(error)
        })
      },
      cadastrar: function(){
        var that = this
        that.axios.post("http://localhost:8080/tarefas", that.tarefa)
        .then(function (response) {
          console.log(response)
          that.tarefas.push(response.data) 
        })
        .catch(function (error) {
          console.log(error)
        })
      },
      pesquisar: function(){
        var that = this
        that.axios.get("http://localhost:8080/tarefas?titulo=" + that.titulo)
        .then(function (response) {
          that.tarefas = response.data.content
        })
        .catch(function (error) {
          console.log(error)
        })
      },
      deletar: function(item){
        var that = this
        that.axios.delete("http://localhost:8080/tarefas/" + item.id)
        .then(function (response) {
          console.log(response)
          that.showDialogDelet = false
          that.recuperarTarefas()
        })
        .catch(function (error) {
          console.log(error)
        })
      }
    }
  }
</script>

<style>
  .v-btn__content {
    color: white !important;
  }
</style>
