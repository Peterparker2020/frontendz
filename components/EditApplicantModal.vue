<template>
    <div>
        <b-modal id="editApplicantModal" title="Edit Applicant" ok-title="Save Applicant" @ok="onSubmit">
            <form action="#">
                <b-form-group label="Name" label-for="name">
                <b-form-input id="name" v-model="applicant.name" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Age" label-for="age">
                <b-form-input id="age" v-model="applicant.age" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Expertise" label-for="expertise">
                <b-form-input id="expertise" v-model="applicant.expertise" trim></b-form-input>
                </b-form-group>


                <b-form-group label="Address" label-for="address">
                <b-form-input id="address" v-model="applicant.address" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Contact" label-for="contact">
                <b-form-select v-model="applicant.contact" :options="options"></b-form-select>
                </b-form-group>
            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        applicant: {}
    },
    data() {
        return {
            options: [
                {value: 'programmer', text: 'programmer'},
                {value: 'designer', text: 'designer'},
               
            ]
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.put('/api/applicants/' + this.applicant.id, this.applicant)
            .then((res)=>{
                if(res.status==202) {
                    alert('Edit successful!')
                }
            })
            .catch((err)=>{
                alert(err.message)
            })
        }
    }
}
</script>