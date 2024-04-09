<template>
    <main>
        <header>
            <img src="./assets/pinia-logo.svg" alt="Pinia Logo">
            <h1>Pinia Task</h1>
        </header>
        
        <!--new task form-->
        <div class="new-task-form">
            <TaskForm />
        </div>

        <!--Filter-->
        <nav class="filter">
            <button @click="filter = 'all'">All tasks</button>
            <button @click="filter = 'favs'">Fav tasks</button>
        </nav>

        <!--Loading-->
        <div class="loading" v-if="loading">Loading...</div>

        <div class="task-list" v-if="filter === 'all'">
            <p>You have {{ totalCount }} tasks left to do</p>
            <div v-for="task in tasks" :key="task.id">
                <TaskDetails :task="task"/>
            </div>
        </div>

        <div class="task-list" v-if="filter === 'favs'">
            <p>You have {{ favCount }} favs tasks left to do</p>
            <div v-for="task in favs" :key="task.id">
                <TaskDetails :task="task"/>
            </div>
        </div>

    </main>
</template>

<script>
import { storeToRefs } from 'pinia';
import TaskDetails from './components/TaskDetails.vue'
import TaskForm from './components/TaskForm.vue'
import { useTaskStore } from './stores/TaskSotre';
import { ref } from 'vue'

    export default {
        components: { TaskDetails, TaskForm },
        setup () {
            const taskStore = useTaskStore()
            const { tasks, loading, favs, favCount, totalCount } = storeToRefs(taskStore)

            taskStore.getTasks()

            const filter = ref('all');

            return { filter, tasks, loading, favs, favCount, totalCount }
        }
    }
</script>