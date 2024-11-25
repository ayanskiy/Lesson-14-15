<template>
    <li :class="['list-group-item', { 'list-group-item-success': localTask.completed }]">
        <div class="d-flex justify-content-between align-items-center">
            <h5>{{ localTask.title }}</h5>
        </div>
        <div class="form-check form-switch">
            <input class="form-check-input" type="checkbox" :checked="localTask.completed" @change="toggleCompleted" role="switch" id="flexSwitchCheckDefault">
        </div>
        <button @click="deleteTask" class="btn btn-danger btn-sm m-2">Удалить</button>
        <button @click="showDetails" class="btn btn-info btn-sm mr-2" :data-bs-toggle="'collapse'" :data-bs-target="'#collapse' + localTask.id" :aria-expanded="showDetail" :aria-controls="'collapse' + localTask.id">Подробнее</button>
        <div :class="['collapse', { show: showDetail }]" :id="'collapse' + localTask.id">
            <div class="card card-body">
                {{ localTask.description }}
            </div>
        </div>
    </li>
</template>
  
<script>
export default {
    name: 'TaskItem',
    props: {
        task: {
            type: Object,
            required: true
        }
    },
    data() {
        return {
            localTask: { ...this.task },
            showDetail: false,
        };
    },
    watch: {
        task: {
            handler(newTask) {
                this.localTask = { ...newTask };
            },
            deep: true,
            immediate: true
        }
    },
    methods: {
        deleteTask() {
            this.$emit('delete-task', this.localTask.id);
        },
        toggleCompleted() {
            this.localTask.completed = !this.localTask.completed;
            this.$emit('update-task', this.localTask);
        },
        showDetails() {
            this.showDetail = !this.showDetail;
        },
    },
};
</script>
  
<style scoped>
.completed {
    color: green;
}
</style>