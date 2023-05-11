<template>
    <AppLayout>
        <template #content>
            <div class="col-4 offset-4">
                <div class="row">
                    <div class="card-body">
                        <h4 class="card-title fw-bold">Add Student</h4>

                        <form @submit.prevent="studentStore" class="forms-sample">
                            <div class="form-group">
                                <label for="input1">Name</label>
                                <input type="text" class="form-control" name="name" v-model="studentform.name" id="input1"
                                    placeholder="Name">
                            </div>
                            <div class="form-group">
                                <label for="input2">Age</label>
                                <input type="text" class="form-control" name="age" v-model="studentform.age" id="input2"
                                    placeholder="Age">
                            </div>
                            <button type="submit" class="btn btn-primary text-dark me-2 mt-3">Submit</button>
                        </form>
                    </div>
                </div>
            </div>

            <div class="col-8 offset-2">
                <h1 class="fw-bold">Student List</h1>

                <div class="card-body">

                    <table class="table table-striped">
                        <thead>
                            <tr>
                                <th>#</th>
                                <th> Name </th>
                                <th> Age </th>
                                <th> Status </th>
                                <th> Action </th>
                            </tr>
                        </thead>
                        <tbody>
                            <!-- {{ student_list }} -->
                            <tr v-for="(student, key) in student_list">

                                <th scope="row">{{ ++key }}</th>
                                <td class="py-1">{{ student.name }}</td>
                                <td> {{ student.age }} </td>
                                <td>
                                    <label v-if="student.status == 'active'" class="badge bg-success">{{ student.status
                                    }}</label>
                                    <label v-if="student.status == 'inactive'" class="badge bg-warning">{{ student.status
                                    }}</label>
                                </td>
                                <td><button type="button" @click.prevent="deleteStudent(student.id)"
                                        class="btn btn-danger text-dark">Delete</button></td>
                                <td><button type="button" @click.prevent="editStudent(student.id)"
                                        class="btn btn-success text-dark">Edit</button>
                                </td>
                                <td><button type="button" @click.prevent="studentStatus(student.id)"
                                        class="btn btn-primary text-dark">Status</button> </td>
                            </tr>

                        </tbody>
                    </table>
                </div>
            </div>
        </template>
        <template #modals>
            <!-- Modal -->
            <div class="modal fade" id="studentEdit" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                <div class="modal-dialog">
                    <div class="modal-content">
                        <div class="modal-header">
                            <h5 class="modal-title" id="exampleModalLabel">Update Student</h5>
                            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                        </div>
                        <form @submit.prevent="studentUpdate" class="row g-3">

                            <div class="modal-body">

                                <div class="col-auto mt-3">
                                    <input type="text" class="form-control" name="name" v-model="student_update_form.name" 
                                        placeholder="Name">
                                </div>
                                <div class="col-auto mt-3">
                                    <input type="text" class="form-control" name="age" v-model="student_update_form.age"
                                        placeholder="Age">
                                </div>
                            </div>
                            <div class="modal-footer">
                                <button type="button" class="btn btn-secondary text-dark" data-bs-dismiss="modal">Close</button>
                                <button type="submit" class="btn btn-primary text-dark">Submit</button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </template>
    </AppLayout>
</template>

<script>
import AppLayout from '@/Layouts/App.vue'
import axios from 'axios';

export default {
    components: {
        AppLayout
    },
    data() {
        return {
            student_list: [],

            studentform: {},
            student_update_form: {
                name: '',
                age: ''
            },
        }
    },
    beforeMount() {
        this.getStudents();
    },
    methods: {
        async getStudents() {
            const student = (await axios.get(route('student.list'))).data
            this.student_list = student
        },
        async studentStore() {
            await axios.post(route('student.store'), this.studentform)
            this.getStudents();
            this.studentform = {
                name: '',
                age: ''
            }
        },
        async deleteStudent(id) {
            await axios.delete(route('student.delete', id))
            this.getStudents();
        },
        async studentStatus(id) {
            await axios.get(route('student.status', id))
            this.getStudents();
        },
        async editStudent(id) {
            const student = (await axios.get(route('student.get', id))).data
            this.student_update_form = student
            $('#studentEdit').modal('show');
        },
        async studentUpdate() {
            await axios.post(route('student.update', this.student_update_form.id), this.student_update_form)
            this.getStudents();
            this.student_update_form = {
                name: '',
                age: ''
            }
            $('#studentEdit').modal('hide');
        },

    }
}
</script>

<style lang="stylus" scoped>

</style>
