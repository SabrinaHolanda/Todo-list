<template>
 <q-page padding class="flex">
    <div class="row">
    <h3 class="col-12">Atividades | Tarefas</h3>
   
       <div class="col-12 right">
      <q-select v-model="usuario_selecionado" :options="user" option-value="id" option-label="name" label="Usuários" @input="listAtiv" />
    </div>
    <q-list class="col-12 row" bordered separator>
      <q-item class="col-12" clickable v-ripple v-for="(task, key) in tasks":key="task.id">
        <q-item-section>
          <q-item-label overline>{{key + 1}} - {{task.title}}</q-item-label>
          <q-item-label>{{task.completed ? 'Fechada' : 'A fazer'}}</q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
    </div>
  </q-page>

</template>

<script>
export default {

  name: 'PageIndex',
  data () {
    return {
      tasks: [],
      user: [],
      usuario_selecionado: {
        id: 1,
        name: ''
        
      }
    }
  },
  methods: {
    listAtiv () {
      const url = 'http://jsonplaceholder.typicode.com/todos?userId=' + this.usuario_selecionado.id
      this.$axios.get(url)
        .then(response => {
          this.tasks = (response.data)
        })
    },
    listUsuario () {
      const url = 'http://jsonplaceholder.typicode.com/users'
      this.$axios.get(url)
        .then(response => {
          this.user = (response.data)
        })
    }
  },
  beforeMount () {
    this.listAtiv()
    this.listUsuario()

  }
}
</script>
