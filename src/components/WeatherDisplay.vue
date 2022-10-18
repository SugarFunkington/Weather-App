<template>
    <div class="weather-box">
        <div class="temp">{{Math.round(weather.main.temp)}}°c</div>
        <div class="weather">{{weather.weather[0].main}}</div>
    </div>
</template>

<script>
    export default {
        name:'WeatherDisplay',
        props: {
            weather: Object
        }
    }
</script>

<style scoped>
.weather-box {
    text-align: center;
}

.weather-box .temp {
    display:inline-block;
    padding: 10px 25px;
    color:#fff;
    font-size:102px;
    font-weight:900;

    text-shadow: 3px 6px rgba(0,0,0,0.25);
    background-color:rgba(255,255,255,0.25);
    border-radius:16px;
    margin:30px 0px;

    box-shadow: 3px 6px rgba(0,0,0,0.25);
}

.weather-box .weather {
    color:#fff;
    font-size:48px;
    font-weight:200;
    text-shadow:1px 3px rgba(0,0,0,0.25);
}
</style>