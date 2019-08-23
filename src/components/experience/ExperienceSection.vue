<template>
    <div class="section">
        <h5>Work Experience</h5>
        <div class="row">
            <div 
                v-for="work in experience" 
                v-bind:key="work.id"
                class="row col l6">
                <h6>{{work.work_name}}</h6>
                <div>{{work.work_start}} - {{work.work_end}}</div>
                <div>{{work.work_position}}</div>
                <div>{{work.work_desc}}</div>
            </div>
        </div>
    </div>
</template>


<script>
    import db from './../firebase/firebaseInit'
    export default {
        props:{
            title: String
        },
        data() {
            return {
                experience: [],
            }
        },
        created () {
            db.collection('experience').orderBy('work_id').get().then(querysnapshot => {
                querysnapshot.forEach(doc => {
                    // console.log(doc.id);
                    const data = {
                        'id': doc.id,
                        'work_id' : doc.data().work_id,
                        'work_name' : doc.data().work_name,
                        'work_position' : doc.data().work_position,
                        'work_start' : doc.data().work_start,
                        'work_end' : doc.data().work_end,
                        'work_desc' : doc.data().work_desc,
                    }
                    this.experience.push(data)
                })
            })
        }
    }
</script>