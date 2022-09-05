<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Todolist</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 1</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-grid fixed size="sm">
        <ion-row>
          <ion-col size="2">ID</ion-col>
          <ion-col size="8">Name</ion-col>
          <ion-col size="2">Action</ion-col>
        </ion-row>
        <ion-row v-for="todo in state.todoList" :key="'todo-' + todo.id">
          <ion-col size="2">{{ todo.id }}</ion-col>
          <ion-col size="8">{{ todo.name }}</ion-col>
          <ion-col size="2" @click="deleteTodo(todo.id)">
            <ion-button color="danger">
              X
            </ion-button>
          </ion-col>
        </ion-row>
      </ion-grid>
      <ion-fab vertical="bottom" horizontal="center" slot="fixed">
        <ion-fab-button color="success" id="open-modal">
          +
        </ion-fab-button>
      </ion-fab>
      <ion-modal ref="modal" trigger="open-modal">
        <ion-header>
          <ion-toolbar>
            <ion-title>New todo</ion-title>
            <ion-buttons slot="end">
              <ion-button :strong="true" @click="addTodo">Confirm</ion-button>
            </ion-buttons>
          </ion-toolbar>
        </ion-header>
        <ion-content class="ion-padding">
          <ion-item>
            <ion-label position="stacked">Enter your name</ion-label>
            <ion-input v-model="state.newTodoName" type="text" placeholder="Your todo name"></ion-input>
          </ion-item>
        </ion-content>
      </ion-modal>
    </ion-content>
  </ion-page>
</template>

<script lang="ts" setup>
import {defineComponent, reactive, ref} from 'vue';
import {IonContent, IonHeader, IonInput, IonLabel, IonModal, IonPage, IonTitle, IonToolbar} from '@ionic/vue';

defineComponent({
  name: 'Tab1Page',
  components: {IonHeader, IonToolbar, IonTitle, IonContent, IonPage}
});


const state = reactive({
  id: 2,
  todoList: [
    {
      id: 1,
      name: 'Eat apple'
    }
  ],
  newTodoName: ''
})

// const toggleModal = () => modal.value = !modal.value;

const addTodo = () => {
  if (state.newTodoName.length > 0) {
    state.todoList.push({
      id: state.id,
      name: state.newTodoName
    });
  }
  state.id++;
  state.newTodoName = '';
}

const deleteTodo = (id: number) => {
  state.todoList = state.todoList.filter(todo => id !== todo.id);
}

</script>
