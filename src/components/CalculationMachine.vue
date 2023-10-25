<template>

        <div class="container mt-5">
            <div class="row justify-content-center">
                <div class="col-md-4">
                    <div class="card">
                        <div class="card-header bg-primary text-white">
                            <h1 class="text-center bg-dark" >  Interview Task </h1>
                            <h3 class="text-center">Calculator</h3>
                        </div>
                        <div class="card-body">
                            <div id="calculator-form">
                                <div class="form-group">
                                    <label for="operand1">Operand 1</label>
                                    <input v-model="operand1"  class="form-control" id="operand1" required>
                                </div>
                                <div class="form-group">
                                        <label for="operator">Operator (drop down)</label>
                                        <select  v-model="operator" class="form-control" id="operator" required>
                                            <option value="add">Add</option>
                                            <option value="subtract">Subtract</option>
                                            <option value="multiply">Multiply</option>
                                            <option value="divide">Divide</option>
                                        </select>
                                </div>
                                <div class="form-group">
                                    <label for="operand2">Operand 2</label>
                                    <input v-model="operand2"  class="form-control" id="operand2" required>
                                </div>
                                <button @click="calculate" class="btn btn-primary btn-block">Calculate</button>
                            </div>
                        </div>
                        <div class="card-footer">
                            <div id="result" class="text-center">{{ result }}</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
</template>

<script>
import axios from 'axios'; // Import Axios
import { IP_API_HOST } from '@/host_config';
export default {
    data() {
        return {
            operand1: null,
            operator: '',
            operand2: null,
            result: null,
        };
    },
    methods: {
        calculate() {
            // const apiUrl = `https://127.0.0.1:8002/${this.operator}/${this.operand1}/${this.operand2}`; or configure host_config.js file; 
            const apiUrl = `${IP_API_HOST}/${this.operator}/${this.operand1}/${this.operand2}`;
            // Make an Axios GET request

            axios.get(apiUrl)
                .then(response => {
                    if (response.data.result !== undefined) {
                        this.result = response.data.result;
                        console.log(this.result); // Log the result here
                    } else {
                        console.error('Response data result is undefined.');
                    }
                })
                .catch(error => {
                    console.error('Axios request error:', error);
                });

            // Make a GET request using fetch
            fetch(apiUrl, {
                method: "GET",
                headers: {
                    "Content-Type": "application/json",
                },
            })
                .then(response => {
                    if (response) {
                        return response.json();
                    } else {
                        console.error('Network response was not ok');
                        throw new Error('Network response was not ok');
                    }
                })
                .then(data => {
                    if (data.result !== undefined) {
                        this.result = data.result;
                        console.log(this.result); // Log the result here
                    } else {
                        console.error('Fetch response data result is undefined.');
                    }
                })
                .catch(error => {
                    console.error("Fetch request error:", error);
                });

        }

    }
}

</script>