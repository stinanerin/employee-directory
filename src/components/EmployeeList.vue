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
                employees: [], // to store the fetched employee data
                currentPage: 1, // current page of the pagination
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
                    const res = await axios.get(`htteps://reqres.in/api/users?page=${this.currentPage}`);
                    if(res.status !== 200) {
                        throw new Error()
                    }
                    const data = res.data
                    console.log(data);
                    this.employees = data.data;
                } catch (error) {
                    this.showModal = true; 
                    console.error("Error fetchEmployees", error);
                }
            },
            toggleModal() {
                this.showModal = !this.showModal
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
  
</style>