<template>
    <div class="hello">
        <h1>{{ msg }}</h1>

        <section v-if="errored">
            <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
        </section>

        <section v-else>
            <div v-if="loading">Loading...</div>

            <div
                    v-else
                    class="message"
            >
                <img v-bind:src="message">
            </div>
        </section>
        <div id="button">
            <button v-on:click="getNewDog">Woof</button>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';

    function getDog() {
        axios
            .get(' https://dog.ceo/api/breeds/image/random')
            .then(response => {
                this.message = response.data.message
            })
            .catch(error => {
                console.log(error)
                this.errored = true
            })
            .finally(() => this.loading = false)
    }

    export default {
        name: 'HelloWorld',
        props: {
            msg: String,
        },
        data() {
            return {
                message: null,
                loading: true,
                errored: false
            }
        },
        methods: {
            getNewDog: getDog
        },
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    button {
        color: white;
        background-color: #2c3e50;
        font-size: 20px;
        margin: 30px;
        border-radius: 20px;
        padding: 10px 30px 10px 30px;
    }

    img {
        border-radius: 20px;
        height: 500px;
    }
</style>
