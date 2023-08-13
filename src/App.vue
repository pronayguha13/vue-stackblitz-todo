<script lang="ts">
import { defineComponent, ref, computed } from 'vue';

type Task = {
  task: string;
  createdAt: string;
  isCompleted: boolean;
};
export default defineComponent({
  name: 'App',
  setup() {
    const taskInput = ref<string>('');
    const tasks = ref<Task[]>([] as Task[]);

    const onClickAdd = () => {
      console.log('Inside the onClickAdd function--->', taskInput);
      if (!taskInput.value.length) return;

      const payload = {
        task: taskInput.value,
        createdAt: new Date().toISOString(),
        isCompleted: false,
      };

      const oldTaskList = tasks.value;
      oldTaskList.push(payload);

      tasks.value = oldTaskList;
      taskInput.value = '';
    };

    return {
      taskInput,
      tasks,
      onClickAdd,
    };
  },
});
</script>
<template>
  <div class="container">
    <header>
      <input type="text" v-model.trim="taskInput" />
      <button :disabled="taskInput.length === 0" @click="onClickAdd">
        Add
      </button>
    </header>
    <section class="tasklist">
      <ul>
        <li v-for="(entry, index) in tasks" :key="index">
          {{ entry.task }}
        </li>
      </ul>
    </section>
  </div>
</template>
<style>
:root {
  font-size: 100%;
}
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.container {
  height: 100%;
}

.container header {
  height: 20%;
  border-bottom: 0.125rem solid #eee;
  padding: 0.5rem;
  display: flex;
  flex-direction: column;
}

.container header input {
  height: 2rem;
  border: none;
  border-bottom: 1px solid #000;
  margin-bottom: 0.5rem;
}

.container header input:focus {
  outline: none;
}

.container header button {
  padding: 0.5rem;
  background-color: #2196f3;
  border-color: #2196f3;
  border-radius: 0.25rem;
  color: #fff;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
}

.container header button:disabled {
  cursor: not-allowed;
  opacity: 0.5;
}
</style>
