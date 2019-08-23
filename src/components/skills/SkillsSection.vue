<template>
    <div class="section">
        <div class="row">
            <h5>Skills</h5>
            <div class="col s6">
                <span v-for="skill in skills" v-bind:key="skill.id" class="chip">
                    {{skill.skill_name}}
                </span>
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
                skills: [],
            }
        },
        created () {
            db.collection('skills').orderBy('skill_id').get().then(querysnapshot => {
                querysnapshot.forEach(doc => {
                    // console.log(doc.id);
                    const data = {
                        'id': doc.id,
                        'skill_id' : doc.data().skill_id,
                        'skill_name' : doc.data().skill_name,
                        'skill_type' : doc.data().skill_type,
                    }
                    this.skills.push(data)
                })
            }) 
        }
    }
</script>