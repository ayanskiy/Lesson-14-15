<template>
    <div class="card mb-4">
        <div class="card-body">
            <h5 class="card-title">Добавить новую задачу</h5>
            <form @submit.prevent="addTask">
                <div class="input-group mb-3">
                    <input v-model="title" placeholder="Название" class="form-control" required />
                </div>
                <div class="input-group">
                    <input v-model="description" placeholder="Описание" class="form-control" required />
                </div>
                <button type="submit" class="btn btn-primary mt-3">Добавить</button>
            </form>
        </div>
    </div>
</template>
  
<script>
export default {
    name: 'TaskForm',
    data() {
        return {
            title: '',
            description: '',
        };
    },
    methods: {
        addTask() {
            this.$emit('add-task', {
            id: Date.now(),
            title: this.title,
            description: this.description,
            completed: false,
            });
            this.title = '';
            this.description = '';
        },
    },
};
</script>