<template>
    <div id="new-education">
        <h3>New Education</h3>
        <div class="row">
            <form @submit.prevent="saveEmployee" class="col s12">
                <div class="row">
                    <div class="input-field col s12">
                        <input disabled type="text" v-model="edu_id" required hidden>
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input type="text" v-model="edu_name" required>
                        <label>University Name</label>
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input type="text" v-model="edu_field" required>
                        <label>Field</label>
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s6">
                        <input type="text" v-model="edu_start" required>
                        <label>Date Start</label>
                    </div>
                    <div class="input-field col s6">
                        <input type="text" v-model="edu_end" required>
                        <label>Date End</label>
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input type="text" v-model="edu_desc" required>
                        <label>Description</label>
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
        name: 'new-education',
        
        data() {
            return {
                edu_id: null,
                edu_name: null,
                edu_desc: null,
                edu_field: null,
                edu_start: null,
                edu_end: null,
            }
        },
        beforeRouteEnter (to,from,next) {
            db.collection('education').orderBy('edu_id', 'desc').limit(1).get()
            .then(querySnapshot => {
                querySnapshot.forEach(doc => {
                    next(vm => {
                        vm.edu_id = (parseInt(doc.data().edu_id) + 1)
                    })
                })
            })
        },
        methods: {
            saveEmployee() {
                db.collection('education').add({
                    edu_id: this.edu_id,
                    edu_name: this.edu_name,
                    edu_field: this.edu_field,
                    edu_start: this.edu_start,
                    edu_end: this.edu_end,
                    edu_desc: this.edu_desc,
                })
                .then(docRef => this.$router.push('/'))
                .catch(error => console.log(err))
            }
        }
    }
</script>
