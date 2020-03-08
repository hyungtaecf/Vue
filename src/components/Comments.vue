<template>
  <div class="container">
    <h1>Comentários</h1>
    <hr />
    <FormTodo v-on:add-todo="addComment"></FormTodo>
    <div class="list-group">
      <p v-if="comments.length <= 0">Sem comentários...</p>
      <div
        v-else
        class="list-group-item"
        v-for="(comment, index) in allComments"
        :key="index"
      >
        <span class="comment__author">
          Autor:
          <strong>{{ comment.name }}</strong>
        </span>
        <p>{{comment.message}}</p>
        <div>
          <a v-on:click.prevent="removeComment(index)" href="#" title="Excluir">Excluir</a>
        </div>
      </div>
    </div>
    <hr />
  </div>
</template>

<script>
import FormTodo from "./FormTodo";
export default {
  components: {
    FormTodo
  },
  //O compilador do Vue.js dá um New Vue() automaticamente
  data() {
    //data: function(){
    return {
      comments: [],
      name: "",
      message: ""
    };
  },
  methods: {
    addComment(comment) {
      this.comments.push(comment);
    },
    removeComment(index) {
      this.comments.splice(index, 1); //remove 1 item desde a posição index
    }
  },
  computed: {
    //para evitar de fazer lógicas de como aparece para o usuário no template, se usa computed
    allComments() {
      return this.comments.map(comment => ({
        ...comment, //separa os atributos name e message para variáveis
        name: comment.name.trim() === "" ? "Anônimo" : comment.name
      }));
    }
  },
  watch: {
    //acionado toda a vez que altera uma propriedade
    //as funções têm que ter o mesmo nome das propriedades do data
    comments(val) {
      console.log("val", val);
    }
  }
};
</script>
