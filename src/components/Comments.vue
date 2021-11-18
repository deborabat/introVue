<template>
  <div class="container">
   <h1> Comentarios </h1>
     <hr>
       <formTodo v-on:add-todo="addComment"/>
        <div class="list-group">
          <p v-if="comments.lenght <= 0 ">Sem comentarios </p>
            <div v-else class="list-item-group" v-for="(commet, index) in allComments" v-bind:key="index">
              <span class="comment-autor"> Autor <strong>{{comment.name}}</strong></span>
                <p>{{comment.message}}</p>
                <div>
                  <a href="#" title="Exclir" v-on:click.prevent="removeComment(index)">Exclir</a> 
               </div>
            </div>
        </div>
     <hr />
  </div>
</template>

<script>
import FormTodo from './FormTodo.vue'

export default {
  components:{
    FormTodo
  },
  data() {
    return{
      comments: []
    }
  },
  methods: {
    addComment(comment) {
      this.comments.push(comment);
    },
    removeComment(index) {
      this.comments.splice(index, 1);
    }
  },
  computed: {
    allComments() {
      return this.comments.map(comment => ({
        ...comment,
        name: comment.name.trim() === "" ? 'Anônimo' : comment.name
      }))
    }
  },
  watch: {
    comments(val) {
      console.log('val', val)
    }
  }
}
</script>
