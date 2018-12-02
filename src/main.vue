<template>
  <div id="app">
    <h2>Current time is {{ getTime() }}</h2>
    <h3>
    Tasks:
    </h3>
    <div class='task' v-for="(task, index) in tasks" :key='task.id'>
      <p>
        <input type='checkbox' :checked='task.isSelected' @change='onSelectTask($event, index)' />
        <span class="key"> {{ task.name }} </span>
      </p>
      <form v-if='task.isSelected' @submit.prevent.stop='onSubmitTask($event, index)'>
        <p>
          <input type='text' :value="task.name" />
          <input style="display:none;" />
          <button type='submit'>Save</button>
        </p>
        <p><img :src="task.icon"></p>
        <p><span class="key">Name: </span> {{ task.name }}</p>
        <p><span class="key">Email: </span> {{ task.owner }}</p>
      </form>
    </div>
  </div>
</template>

<script>
let id = 0;
function getId() {
  id += 1;
  return id;
}

export default {
  name: 'main',
  data: () => ({
    tasks: [{
      id: getId(),
      name: 'My Task',
      icon: 'https://imgflip.com/s/meme/Jackie-Chan-WTF.jpg',
      owner: 'mzimmerman0205@gmail.com',
      isSelected: false,
    },
    {
      id: getId(),
      name: 'Another Task',
      icon: 'http://chittagongit.com//images/psyduck-icon/psyduck-icon-9.jpg',
      owner: 'mzimmerman0205@gmail.com',
      isSelected: false,
    }],
  }),
  methods: {
    getTime: () => new Date().toLocaleString(),
    onSelectTask: function onSelectTask(event, index) {
      this.tasks[index].isSelected = !this.tasks[index].isSelected;
    },
    onSubmitTask: function onSubmitTask(event, index) {
      this.tasks[index].name = event.target.querySelector('input').value;
      this.tasks[index].isSelected = !this.tasks[index].isSelected;
    },
  },
};
</script>

<style>
body {
  background: #20262E;
  padding: 20px;
  font-family: Helvetica;
}

#app {
  background: #fff;
  border-radius: 4px;
  padding: 20px;
  transition: all 0.2s;
}

li {
  margin: 8px 0;
}

h2 {
  margin-bottom: 10px;
}

h3 {
  font-weight: bold;
  margin-bottom: 15px;
}

del {
  color: rgba(0, 0, 0, 0.3);
}

.task {
  padding-bottom: 15px;
  margin-bottom: 15px;
  border-bottom: 2px solid black;
}

.key {
  font-weight: bold;
}
</style>
