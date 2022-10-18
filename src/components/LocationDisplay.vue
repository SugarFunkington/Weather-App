<template>
    <h1 class="location">{{location.locality}}, {{location.country}}</h1>
    <h3 class="date">{{date}}</h3>
</template>

<script>
    export default {
        name:'LocationDisplay',
        props: {
            location: Object
        },
        data () {
            return {
                date: ''
            }
        },
        created () {
            let d = new Date()
            let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"]
            let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]
            
            let day = days[d.getDay()]
            let date = d.getDate()
            let month = months[d.getMonth()]
            let year = d.getFullYear();

            this.date = `${day}, ${date} ${month} ${year}`
        }
    }
</script>

<style scoped>
h1.location {
    color:#fff;
    font-size:32px;
    font-weight:400;
    text-align:center;
    text-shadow:1px 3px rgba(0, 0, 0, 0.25);
    margin:0;

}

h3.date {
    color:#fff;
    font-size:20px;
    font-weight:200;
    text-align:center;
    margin:0;
}
</style>