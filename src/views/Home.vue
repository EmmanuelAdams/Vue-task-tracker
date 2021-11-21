<template>
  <div>
    <AddTask
      v-show="showAddTask"
      @add-task="addTask"
    />
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<script>
import Tasks from '../components/Tasks';
import AddTask from '../components/AddTask';
export default {
  name: 'Home',
  props: {
    showAddTask: Boolean,
  },
  components: {
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
    };
  },

  methods: {
    addTask(task) {
      this.tasks = [...this.tasks, task];
    },
    deleteTask(id) {
      if (confirm('Are you sure?')) {
        this.tasks = this.tasks.filter(
          (task) => task.id !== id
        );
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id
          ? { ...task, reminder: !task.reminder }
          : task
      );
    },
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Doctors Appointment',
        day: 'September 1st at 2:30pm',
        reminder: true,
      },
      {
        id: 2,
        text: 'Meeting with George',
        day: 'November 17th at 8:30am',
        reminder: true,
      },
      {
        id: 3,
        text: 'Date',
        day: 'October 1st at 5:00pm',
        reminder: false,
      },
    ];
  },
};
</script>
