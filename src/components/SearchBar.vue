<template>
    <div :class="{'highlightForm' : formHighlighted === true}">
        <input type="text" class="search-bar" id="search-bar" placeholder="Search for a city..." v-model="query" @focus="toggleFormHighlight()" @blur="toggleFormHighlight()"
        @keypress="search"/>
        <button @click="search">
            <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
        </button>
    </div>
</template>

<script>
    export default {
        name:'SearchBar',
        methods: {
            toggleFormHighlight() {
                this.formHighlighted = !this.formHighlighted
            },
            search(e) {
                if (e.type === 'keypress' && e.key !== 'Enter') {
                    return
                } else {
                    this.$emit('search', this.query)
                    this.query = ''
                    document.getElementById("search-bar").blur()
                }
            }
        },
        emits: ['search'],
        data () {
            return {
                query:'',
                formHighlighted:false
            }
        }
    }
</script>

<style scoped>

div {
    width:100%;
    max-width:500px;
    margin:30px auto;
    display:block;
    box-shadow:0px 2px 4px rgba(0, 0, 0, 0.25);
    background-color:rgba(255,255,255,0.65);
    border-radius: 0px 16px 0px 16px;
    transition:0.4s;
}

button {
    background:none;
    color:#555454;
    width:36px;
    height:36px;
    border-radius:100%;
    border:1px;
    transition:0.2s;
}

button:hover {
    color:rgb(39, 39, 39);
    background:rgba(255,255,255,0.2);
}

button:active {
    color:black;
    background:rgba(255,255,255,0.4);
}

.highlightForm {
    background-color:rgba(255, 255, 255, 0.9);
    box-shadow:0px 4px 16px rgba(0, 0, 0, 0.5);
}
.search-bar {
    padding:15px;
    color:#202020;
    font-size: 20px;
    width: 90%;

    appearance:none;
    border:none;
    outline:none;
    background:none;
}



</style>