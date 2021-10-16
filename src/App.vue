<template>
    <div class="app">
        <header>
            <div class="title">
                <img src="./assets/heart.svg" alt="site logo" />
                <h1>Hyrule jobs</h1>
            </div>
            <div class="order">
                <button @click="handleClick('title')">Order by title</button>
                <button @click="handleClick('salary')">Order by salary</button>
                <button @click="handleClick('location')">Order by location</button>
            </div>
        </header>

        <JobList :jobs="jobs" :order="order" />
    </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import JobList from './components/JobList.vue'
import Job from './types/job'
import OrderTerm from './types/orderTerm'

export default defineComponent({
    name: 'App',
    components: { JobList },
    setup() {
        // const state = reactive({ name: 'Link', age: 25 as string | number})
        // return { ...toRefs(state) }
        // const name = ref('Link')
        // const age = ref<number | string>(25) //usando ref se tienen que usar genericos para especificar el tipo
        // return { name, age }

        const jobs = ref<Job[]>([
            { title: 'farm worker', location: 'lon lon ranch', salary: 30000, id: '1' },
            { title: 'quarryman', location: 'death mountain', salary: 40000, id: '2' },
            { title: 'flute player', location: 'the lost woods', salary: 35000, id: '3' },
            { title: 'fisherman', location: 'lake hylia', salary: 21000, id: '4' },
            { title: 'prison guard', location: 'gerudo valley', salary: 32000, id: '4' }
        ])
        const order = ref<OrderTerm>('title')

        const handleClick = (term: OrderTerm) => {
            order.value = term
        }

        return {
            jobs,
            handleClick,
            order
        }
    }
})
</script>

<style lang="scss">
header {
    text-align: center;
    .order {
        margin-top: 20px;
    }
    button {
        margin: 0 10px;
        color: #1195c9;
        border: 3px solid #1195c9;
        background: #d5f0ff;
        padding: 8px 16px;
        border-radius: 4px;
        cursor: pointer;
        font-weight: bold;
    }
    .title {
        display: flex;
        justify-content: center;
    }
    img {
        width: 60px;
        margin-right: 20px;
    }
    h1 {
        font-size: 3em;
    }
}
</style>
