<template>
    <div>
        <h2>Список задач</h2>
        <TaskForm @add-task="addTask" />
        <ul class="list-group">
            <TaskItem v-for="task in tasks" :key="task.id" :task="task" @delete-task="deleteTask" @update-task="updateTask" />
        </ul>
        <div class="mt-3">
            <p>Итого задач: {{ totalTasks }}</p>
            <p>Выполнено: {{ completedTasks }}</p>
        </div>
    </div>
</template>
  
<script>
import TaskItem from './TaskItem.vue';
import TaskForm from './TaskForm.vue';
  
export default {
    name: 'TaskList',
    components: {
        TaskItem,
        TaskForm
    },
    data() {
        return {
            tasks: [
                { id: 1, title: 'Задача № 1', description: 'Тестовое описание 1', completed: false },
                { id: 2, title: 'Задача № 2', description: 'Тестовое описание 2', completed: false },
                { id: 3, title: 'Задача № 3', description: 'Тестовое описание 3', completed: false },
            ],
        };
    },
    computed: {
        totalTasks() {
            return this.tasks.length;
        },
        completedTasks() {
            return this.tasks.filter(task => task.completed).length;
        },
    },
    methods: {
        addTask(task) {
            this.tasks.push(task);
        },
        deleteTask(id) {
            this.tasks = this.tasks.filter(task => task.id !== id);
        },
        updateTask(updatedTask) {
            const index = this.tasks.findIndex(task => task.id === updatedTask.id);
            if (index !== -1) {
                this.tasks.splice(index, 1, updatedTask);
            }
        },
    },
};
</script>
  
<style scoped>
.completed {
    color: green;
}
</style>