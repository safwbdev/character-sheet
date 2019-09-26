<template>
    <div id="new-experience">
        <h3>New Work Experience</h3>
        <div class="row">
            <form @submit.prevent="saveEmployee" class="col s12">
                <div class="row">
                    <div class="input-field col s12">
                        <input disabled type="text" v-model="work_id" required hidden>
                        <!-- <label>Work ID</label> -->
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input type="text" v-model="work_name" required>
                        <label>Company Name</label>
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input type="text" v-model="work_position" required>
                        <label>Position</label>
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s6">
                        <input type="text" v-model="work_start" required>
                        <label>Date Start</label>
                    </div>
                    <div class="input-field col s6">
                        <input type="text" v-model="work_end" required>
                        <label>Date End</label>
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input type="text" v-model="work_desc" required>
                        <label>Description</label>
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input type="text" v-model="work_location" required>
                        <label>Location</label>
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
        name: 'new-experience',
        data() {
            return {
                work_id: null,
                work_name: null,
                work_position: null,
                work_desc: null,
                work_start: null,
                work_end: null,
                work_location: null,

            }
        },
        beforeRouteEnter (to,from,next) {
            db.collection('experience').orderBy('work_id', 'desc').limit(1).get()
            .then(querySnapshot => {
                querySnapshot.forEach(doc => {
                    next(vm => {
                        vm.work_id = (parseInt(doc.data().work_id) + 1)
                    })
                })
            })
        },
        methods: {
            saveEmployee() {
                db.collection('experience').add({
                    work_id: this.work_id,
                    work_name: this.work_name,
                    work_position: this.work_position,
                    work_desc: this.work_desc,
                    work_start: this.work_start,
                    work_end: this.work_end,
                    work_location: this.work_location,
                })
                .then(docRef => this.$router.push('/'))
                .catch(error => console.log(err))
            }
            
        }
    }
</script>
