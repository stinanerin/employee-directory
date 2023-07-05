<template>

    <ul class="employee-list">

        <li v-for="employee in employees" :key="employee.id">
            <img :src="employee.avatar" :alt="'Picture of ' + employee.first_name" />
            <h2>
                {{ employee.first_name }} {{ employee.last_name }}
            </h2>
            <a :href="'mailto:' + employee.email + '?&body=Hi%20' + employee.first_name + ','">Contact me!</a>
        </li>

    </ul>

    <div>

        <button class="nav-btn" :class="{ 'active-link' : pageNum === currentPage}" v-for="pageNum in totalPages" :key="pageNum" @click="switchPage(pageNum)">
            {{ pageNum }}
        </button>

    </div>

    <div v-if="showModal" >
        <ModalWindow @close="toggleModal"/>
    </div>

</template>

<script>
    import axios from 'axios';
    import ModalWindow from "./ModalWindow.vue"

    export default {
        data() {
            return {
                // Fetched employee data
                employees: [], 
                // Current api page
                currentPage: 1,
                // Tot. api pages
                totalPages: 0,
                showModal: false,
            };
        },
        components: { ModalWindow },
        mounted() {
            this.fetchEmployees();
        },
        methods: {
            async fetchEmployees() {
                try {
                    const res = await axios.get(`https://reqres.in/api/users?page=${this.currentPage}`);
                    if(res.status !== 200) {
                        throw new Error()
                    }
                    const data = res.data
                    console.log(data);
                    console.log(data.data);
                    this.employees = data.data;
                    this.totalPages = data.total_pages;
                } catch (error) {
                    this.showModal = true; 
                    console.error("Error fetchEmployees", error);
                }
            },
            toggleModal() {
                this.showModal = !this.showModal
            },
            switchPage(pageNumber) {
                this.currentPage = pageNumber
                this.fetchEmployees()
            }
        },
    };

</script>


<style>

    .employee-list {
        display:flex;
        justify-content: center;
        flex-wrap: wrap;
        gap: 3rem;
        padding-left: 0;
    }
    .employee-list li {
        list-style-type: none;
        padding: 2rem;
        background-color: var(--sec-bg-clr);
        border-radius: 1rem;
        text-align: center;
        width: 200px;
    }
    .employee-list li img{
        border-radius: 50%;

    }
    .employee-list li a {
        color: var(--text-clr)
    }
    .employee-list li a:hover {
        cursor: pointer;
    }
    .nav-btn {
        background-color: transparent;
        border: none;
        padding: 0.5rem;
        margin: 0 0.5rem;
        color: var(--text-clr);
    }
    .nav-btn:hover {
        font-weight: bold;
        cursor: pointer;

    }
    .nav-btn.active-link {
        border-bottom: 2px solid var(--text-clr);
        font-weight: bold;
    }
  
</style>