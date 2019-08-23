<template>
    <div class="section">
        <div class="row">
            <div class="col s3">
                <img v-bind:src="img" alt="" style="width:100%;">
            </div>
            <div class="col s4 offset-s5">
                <h1>{{fName}} {{lName}}</h1>
                <div>{{tel}} - {{email}}</div>
                <div>{{dob}}</div>
                <div>{{address}}</div>
            </div>
        </div>
    </div>
</template>


<script>
import db from './firebase/firebaseInit'
export default {
    props:{
        title: String
    },
    data() {
        return {
            fName: null,
            lName: null,
            address: null,
            dob: null,
            email: null,
            fName: null,
            lName: null,
            tel: null,
            img: 'https://images.pexels.com/photos/220453/pexels-photo-220453.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940'
        }
    },
    created () {
        db.collection('personal').get().then(querysnapshot => {
            querysnapshot.forEach(doc => {
                 this.address = doc.data().address
                 this.dob = doc.data().dob
                 this.email = doc.data().email
                 this.fName = doc.data().fName
                 this.lName = doc.data().lName
                 this.tel = doc.data().tel
                 this.address = doc.data().address
            })
        })
    }
}
</script>