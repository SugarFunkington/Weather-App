<template>
    <div class="container">
        <svg class="loader" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 340 340">
            <circle cx="170" cy="170" r="160" stroke="#FFFFFF"/>
            <circle cx="170" cy="170" r="135" stroke="#FFFFFF"/>
            <circle cx="170" cy="170" r="110" stroke="#FFFFFF"/>
            <circle cx="170" cy="170" r="85" stroke="#FFFFFF"/>
        </svg>
    </div>
    <p>Searching for location...</p>
</template>

<script>
export default {
name: 'LoadingSpinner'
}
</script>


<style lang="scss" scoped>

p {
    text-align:center;
    color:white;
}
.container {
	display: flex;
	align-items: center;
	justify-content: center;
	min-height: 50vh;
}

.loader {
	max-width: 10rem;
	width: 100%;
	height: auto;
	stroke-linecap: round;
}

circle {
	fill: none;
	stroke-width: 3.5;
	animation-name: preloader;
	animation-duration: 4s;
	animation-iteration-count: infinite;
	animation-timing-function: ease-in-out;
	transform-origin: 170px 170px;
	will-change: transform;

	&:nth-of-type(1) {
		stroke-dasharray: 550px;
	}

	&:nth-of-type(2) {
		stroke-dasharray: 500px;
	}

	&:nth-of-type(3) {
		stroke-dasharray: 450px;
	}

	&:nth-of-type(4) {
		stroke-dasharray: 300px;
	}

	@for $i from 1 through 4 {
		&:nth-of-type(#{$i}) {
			animation-delay: -#{$i * 0.15}s;
		}
	}
}

@keyframes preloader {
	50% {
		transform: rotate(360deg);
	}
}
</style>