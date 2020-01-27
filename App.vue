<template>
  <view class="container">
    <Statusbar />
    <Header title="Todo App" />
    <scroll-view :content-container-style="{contentContainer: {
        paddingVertical: 20
    }}">
      <view class="input-container">
        <text-input class="input" v-model="inputText"></text-input>
        <touchable-opacity class="btn" :on-press="addItem">
          <text class="btn__text">ADD</text>
        </touchable-opacity>
      </view>

      <view v-for="todo in todos"
            :key="todo.id"
            class="todo">
        <text class="todo__text" :class="{ 'todo__text--done': todo.done }">{{ todo.title }}</text>
        <touchable-opacity :on-press="() => doneItem(todo.id)">
          <text class="todo__btn todo__btn--done">Done</text>
        </touchable-opacity>
        <touchable-opacity :on-press="() => removeItem(todo.id)">
          <text class="todo__btn">Remove</text>
        </touchable-opacity>
      </view>
    </scroll-view>
  </view>
</template>

<script>
import Statusbar from './components/Statusbar'
import Header from './components/Header'

export default {
  name: 'App',
  components: {
    Statusbar,
    Header,
  },
  data:() => ({
    inputText: '',
    todos: [
      {
        id: 0,
        title: 'Go Shopping',
        done: false,
      },
      {
        id: 1,
        title: 'Buy products',
        done: false,
      },
    ],
  }),
  methods: {
    addItem() {
      const todoItem = {
        id: this.todos.length + 1,
        title: this.inputText,
        done: false,
      };

      this.todos.push(todoItem);
      this.inputText = '';
    },
    doneItem(id) {
      this.todos = this.todos.map(item => {
        if (item.id === id) item.done = true;
        return item;
      })
    },
    removeItem(id) {
      this.todos = this.todos.filter(item => item.id !== id);
    },
  }
}
</script>

<style>
.container {
  background-color: white;
  flex: 1;
}

.input-container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: stretch;
}

.input {
  flex: 1;
  height: 40px;
  background-color: #f8f8f8;
  font-size: 20px;
  padding-left: 10px;
  color: #000000;
}


.btn {
  width: 100px;
  height: 40px;
  justify-content: center;
  align-items: center;
  background-color: #FFCE00;
  flex-shrink: 0;
}

.btn__text {
  color: #000000;
  font-weight: 700;
}

.todo__text {
  flex: 1;
  font-size: 18px;
}

.todo__text--done {
  color: #cccccc;
}

.todo {
  flex-direction: row;
  align-items: center;
  padding: 10px;
}

.todo__btn {
  padding-left: 10px;
  color: red;
}

.todo__btn--done {
  color: green;
}

</style>
