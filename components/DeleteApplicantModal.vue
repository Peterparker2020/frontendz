<template>
    <div>
        <b-modal id="deleteApplicantModal" title="Delete Applicant" ok-title="Delete Applicant" @ok="onDelete" ok-variant="danger">
            Are you sure in deleting this applicant? <br><br>
            Name: {{applicant.name}} <br>
            Age: {{applicant.age}}
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        applicant: {}
    },
    methods: {
        async onDelete() {
            this.$axios.delete('/api/applicants/' + this.applicant.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Deleted successfully!')
                    this.$emit('onDeleted')
                }
            })
        }
    }
}
</script>