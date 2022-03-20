<template>
    <div class="text-center">
        <h2 class="text-3xl font-bold">{{text}}</h2>
        <div class="text-2xl mb-10 mt-4">
           {{timeStamp}}
        </div>
    </div>
</template>

<script>
import moment from "moment";
export default {
    name:"DataTitle",
    props : ["text"],
    computed :{
        timeStamp : function(){
            return moment(new Date()).format("Do MMMM YYYY, hh:mm:ss")
        }
    }
}
</script>