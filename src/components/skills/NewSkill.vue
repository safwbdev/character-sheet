<template>
    <div id="new-skill">
        <h3>New Skill</h3>
        <div class="row">
            <form @submit.prevent="saveEmployee" class="col s12">
                <div class="row">
                    <div class="input-field col s12">
                        <input disabled type="text" v-model="skill_id" required hidden>
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input type="text" v-model="skill_name" required>
                        <label>Skill Name</label>
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input type="text" v-model="skill_type" required>
                        <label>Skill Type</label>
                    </div>
                </div>
                <button type="submit" class="btn">Submit</button>
                <router-link to="/dashboard" class="btn">Cancel</router-link>
            </form>
        </div>
    </div>
</template>

<script>
    import db from './../firebase/firebaseInit'
    export default {
        name: 'new-employee',
        data() {
            return {
                colectionID: [],

                skill_id: null,
                skill_name: null,
                skill_type: null,
            }
        },
        beforeRouteEnter (to,from,next) {
            db.collection('skills').orderBy('skill_id', 'desc').limit(1).get()
            .then(querySnapshot => {
                querySnapshot.forEach(doc => {
                    next(vm => {
                        vm.skill_id = (parseInt(doc.data().skill_id) + 1)
                    })
                })
            })
        },
        
        methods: {
            saveEmployee() {
                db.collection('skills').add({
                    skill_id: this.skill_id,
                    skill_name: this.skill_name,
                    skill_type: this.skill_type,
                })
                .then(docRef => this.$router.push('/dashboard'))
                .catch(error => console.log(err))
            }
        }
    }
</script>
