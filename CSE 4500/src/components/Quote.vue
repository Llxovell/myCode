<template>
    <div class="quotebox">
        <div class="quote">{{ quote }}</div><br>
        <span class="name">{{ author }}</span>
    </div>
</template>

<script>
export default {
    data(){
        return{
            quote: 'Meaningful quote to help you complete your task',
            author: '- Author'
        }
    },

    beforeMount() {
        //calls the quote the first time when loading page
        this.quoteAPI()  
    },

    mounted(){
        //quote changes every 30 secs
        setInterval(this.quoteAPI, 30000)
    },

    methods: {
        quoteAPI() {
            fetch("https://quotes15.p.rapidapi.com/quotes/random/", {
                    "method": "GET",
                    "headers": {
                        "x-rapidapi-key": "d9f6d82617msh276e657dbd25914p1e7965jsn09591f308538",
                        "x-rapidapi-host": "quotes15.p.rapidapi.com"
                    }
                })
                .then(response => {
                    return response.json()
                })
                .then(response => {
                    this.quote = response.content
                    this.author = '- ' + response.originator.name
                })
                .catch(err => {
                    console.error(err);
                    //If user keeps spamming refresh like me :P
                    this.quote = 'Meaningful quote to help you complete your task'
                    this.author = '- Author'
                    setTimeout(this.quoteAPI, 1000)
                })
        }
    }
}
</script>

<style>
    .quotebox{
        margin-top: 60px;
        margin-bottom: 20px;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        text-align: center;
        width: 70vw;
    }
</style>