<template>
    <div>
        <b-button v-b-modal.ApplicantEntryModal variant="primary">Add Applicant</b-button>

        <b-modal id="ApplicantEntryModal" title="Applicant Entry" ok-title="Save Applicant" @ok="onSubmit">
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
    data() {
        return {
            applicant: {},
            options: [
                {value: 'email', text: 'email'},
                {value: 'mobile number', text: 'mobile number'},
            ]
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.post('/api/applicants', this.applicant)
            .then((res)=>{
                if(res.status==202) {
                    alert('Successfully added an applicant')
                    this.$emit('onAdd')
                }
            })
        }
    }
}
</script>