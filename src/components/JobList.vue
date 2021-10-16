<template>
    <div class="job-list">
        <p>Order by {{ order }}</p>
        <transition-group name="list" tag="ul">
            <li v-for="job in orderedJobs" :key="job.id">
                <h2>{{ job.title }} in {{ job.location }}</h2>
                <div class="salary">
                    <img src="@/assets/rupee.svg" alt="ruppe" />
                    <p>{{ job.salary }} rupees</p>
                </div>
                <div class="description">
                    <p>
                        Lorem ipsum, dolor sit amet consectetur adipisicing elit. Facere deserunt obcaecati consectetur
                        mollitia assumenda reprehenderit et amet odio debitis ab? Facere enim quam omnis, amet incidunt
                        repellendus quo delectus dolores?
                    </p>
                </div>
            </li>
        </transition-group>
    </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from 'vue'
import Job from '@/types/job'
import OrderTerm from '@/types/orderTerm'

export default defineComponent({
    props: {
        jobs: {
            type: Array as PropType<Job[]>,
            required: true
        },
        order: {
            type: String as PropType<OrderTerm>,
            required: true
        }
    },
    setup(props) {
        const orderedJobs = computed(() => {
            return [...props.jobs].sort((a: Job, b: Job) => {
                return a[props.order] > b[props.order] ? 1 : -1
            })
        })

        return {
            orderedJobs
        }
    }
})
</script>

<style lang="scss" scoped>
.job-list {
    max-width: 960px;
    margin: 40px auto;
    & ul {
        padding: 0;
    }
    & li {
        list-style-type: none;
        background: white;
        padding: 16px;
        margin: 16px 0;
        border-radius: 4px;
    }
    & h2 {
        margin: 0 0 10px;
        text-transform: capitalize;
    }
}
.salary {
    display: flex;
    img {
        width: 30px;
    }
    p {
        color: #17bf66;
        font-weight: bold;
        margin: 10px 4px;
    }
}

.list-move{
    transition: all 1s;
}
</style>
