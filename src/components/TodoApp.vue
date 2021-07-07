<template>
  <div class="container">
    <h2 class="text-center mt-5">My Vue Todo App</h2>
    <div class="d-flex">
      <input
        v-model="task"
        type="text"
        placeholder="Enter task"
        class="form-control"
      />
      <button class="btn btn-warning rounded-0" @click="submitTask">
        submit
      </button>
    </div>
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">task</th>
          <th scope="col">status</th>
          <th scope="col">##</th>
          <th scope="col">##</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td :class="{ line: task.status === 'done' }">{{ task.name }}</td>
          <td
            class="pointer"
            @click="updatedStatus(index)"
            style="width: 120px"
          >
            {{ firstChar(task.status) }}
          </td>
          <td class="pointer" @click="updatedTask(index)">編集</td>
          <td class="pointer" @click="deleteTask(index)">削除</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },

  data() {
    return {
      task: "",
      updated: null,
      statuses: ["to-do", "in-progress", "done"],
      tasks: [
        {
          name: "wrting blogs",
          status: "to-do",
        },
        {
          name: "wrting diary",
          status: "to-do",
        },
        {
          name: "listeining to some radio",
          status: "to-do",
        },
      ],
    };
  },
  methods: {
    submitTask() {
      if (this.task.length === 0) return;
      if (this.updated === null) {
        this.tasks.push({
          name: this.task,
          status: "to-do",
        });
      } else {
        this.tasks[this.updated].name = this.task;
        this.updated = null;
      }
      this.task = "";
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    updatedTask(index) {
      this.task = this.tasks[index].name;
      this.updated = index;
    },
    updatedStatus(index) {
      let statusNumber = this.statuses.indexOf(this.tasks[index].status);
      console.log(statusNumber);
      if (++statusNumber > 2) statusNumber = 0;
      this.tasks[index].status = this.statuses[statusNumber];
    },
    firstChar(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },
  },
};
</script>
<style scoped>
.pointer {
  cursor: pointer;
}
.line {
  text-decoration: line-through;
}
</style>
