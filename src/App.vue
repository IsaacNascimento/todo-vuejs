<template>
  <div id="app">
    <div class="container grid-xs py-2">
      <img
        class="img-responsive img-logo"
        src="https://via.placeholder.com/150"
        alt="LogoMarca"
      />
      <form ref="addTarefa" @submit.prevent="addTodo">
        <div class="input-group">
          <input
            type="text"
            v-model="tarefa.description"
            class="form-input"
            placeholder="Nova tarefa"
          />
          <button class="btn btn-primary input-group-btn">Adicionar</button>
        </div>
      </form>
      <div class="todo-list">
        <tileTarefa v-for="item in tarefas" :key="item.id" :tarefa="item" @toggle="toggleTarefa" @remove="removerTarefa"/>
      </div>
    </div>
  </div>
</template>

<script>
import TileTarefa from './components/TileTarefa.vue';

export default {
  name: "App",
  components: { TileTarefa },
  data() {
    return {
      tarefas: [],
      tarefa: {
        checked: false,
      },
    };
  },
  methods: {
    addTodo() {
      const id = Date.now();
      const { checked, description } = this.tarefa;
      this.tarefas.push({ checked, id, description });
      console.log(this.tarefas);
      this.tarefa.description = "";
    },

    toggleTarefa(tarefa) {
      const index = this.tarefas.findIndex(item => item.id === tarefa.id);
      if (index >= 0) {
        const checked = !this.tarefas[index].checked;
        this.tarefas[index].checked = checked;
      }
    },
    removerTarefa(tarefa) {
      const index = this.tarefas.findIndex(item => item.id === tarefa.id);
      if (index >= 0) {
        this.tarefas.splice(index, 1);
      }
    }
  },
};
</script>

<style scoped>
.img-logo {
  max-width: 200px;
  margin: 0 auto;
  margin-bottom: 10px;
}

.todo-list {
  padding-top: 2rem;
}
</style>
