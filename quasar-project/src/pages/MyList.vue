<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input
        @keyup.enter="addNewTask"
        v-model="newTask"
        class="col"
        bg-color="white"
        placeholder="add new task"
        square
        filled
        dense>
        <template v-slot:append>
          <q-btn
            @click="addNewTask"
            round
            dense
            flat icon="add"/>
        </template>
      </q-input>
    </div>
    <q-list class="bg-white" separator bordered>
      <q-item v-for="(task, index) in tasks"
              :key="task.taskTitle"
              @click="task.done = !task.done"
              :class="{'done bg-blue-1' : task.done}"
              clickable
              v-ripple>
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            class="no-pointer-events"
            color="primary"/>
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.taskTitle }}</q-item-label>
        </q-item-section>
        <q-item-section
          v-if="task.done"
          side
        >
          <q-btn
            @click.stop="deleteTask(index)"
            flat
            round
            dense
            color="primary"
            icon="delete"
          />
          <q-icon name="task_alt" class="absolute-left"/>
        </q-item-section>
      </q-item>
    </q-list>
    <div v-if="!tasks.length"
      class="no-task absolute-center">
<div class="text-h5 text-primary text-center">
  <q-icon
    name="done_all"
    size="100px"
    color="primary"
  /><br>
  No tasks
</div>
    </div>
  </q-page>
</template>


<script>

export default {
  data() {
    return {
      newTask: '',
      tasks: [

      ],
    }
  },

  methods: {
    deleteTask(index) {
      this.$q.dialog({
        title: 'Confirm',
        message: 'Would you really wont to delete this task?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify({
          type: 'positive',
          message: 'This task been deleted successfully.'
        })
      })
    },

    addNewTask() {
      this.tasks.push({
        taskTitle: this.newTask,
        done: false
      })
      this.newTask = ''
    },
  }

}
</script>
<style lang="scss">
.done {
  .q-item__label {
    text-decoration: line-through;
    color: #bbb;
  }
}

.no-task{
  opacity: 0.5;
}

</style>
