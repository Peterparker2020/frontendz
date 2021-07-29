<template>
    <div>
        <NavBar />
        <EditApplicantModal :applicant="selectedApplicant" />
        <DeleteApplicantModal :applicant="selectedApplicant" @onDeleted="getAll" />

        <div class="container">
            <h1>
                List of Applicants
            </h1>
            
            <ApplicantEntryModal class="float-right mb-1" @onAdd="getAll" />

            <table class="table table-bordered table-striped table-primary">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Name</th>
                        <th>Age</th>
                        <th>Expertise</th>
                        <th>Address</th>
                        <th>Contact</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="applicant in applicants" :key="applicant.id">
                        <td>{{applicant.name}}</td>
                        <td>{{applicant.age}}</td>
                        <td>{{applicant.expertise}}</td>
                        <td>{{applicant.address}}</td>
                        <td>{{applicant.contact}}</td>
                        <td class="buttons">
                            <b-button @click="onEdit(applicant)" variant="primary" size="sm">
                                Edit
                            </b-button>
                            <b-button @click="onDelete(applicant)" variant="danger" size="sm">
                                Delete
                            </b-button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
           applicants: [],
            selectedApplicant: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('/api/applicants')
            .then((res)=>{
                if (res.status==200) {
                    this.applicants = res.data
                };
            })
        },
        onEdit(selectedApplicant) {
            this.selectedApplicant = selectedApplicant
            this.$bvModal.show('editApplicantModal')
        },
        onDelete(selectedApplicant) {
            this.selectedApplicant = selectedApplicant
            this.$bvModal.show('deleteApplicantModal')
        }
    },
    created() {
        this.getAll()
    }
}
</script>

<style>
h1 {
    text-align: center;
    margin-top: 50px;
}
.buttons {
    text-align: center;
}
</style>