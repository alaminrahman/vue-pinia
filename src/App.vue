<template>
    <main>
        <header>
            <img src="./assets/pinia-logo.svg" alt="Pinia Logo">
            <h1>Pinia Task</h1>
        </header>

        <!--Filter-->
        <nav class="filter">
            <button @click="filter = 'all'">All tasks</button>
            <button @click="filter = 'favs'">Fav tasks</button>
        </nav>

        <div class="task-list" v-if="filter === 'all'">
            <p>You have {{ taskStore.totalCount }} tasks left to do</p>
            <div v-for="task in taskStore.tasks" :key="task.id">
                <TaskDetails :task="task"/>
            </div>
        </div>

        <div class="task-list" v-if="filter === 'favs'">
            <p>You have {{ taskStore.favCount }} favs tasks left to do</p>
            <div v-for="task in taskStore.favs" :key="task.id">
                <TaskDetails :task="task"/>
            </div>
        </div>

    </main>
</template>

<script>
import TaskDetails from './components/TaskDetails.vue'
import { useTaskStore } from './stores/TaskSotre';
import { ref } from 'vue'

    export default {
        components: { TaskDetails },
        setup () {
            const taskStore = useTaskStore()

            const filter = ref('all');

            return { taskStore, filter }
        }
    }
</script>