<template>
    <div class="header"><h2>Вопросы тестирования к экзамену </h2></div>
    <div v-if="question">
        <div class="main-block" v-for="(item, i) in question">
            <p>{{ item.id }}. {{ item.question }}</p>
            <div class="variant" v-for="variant in item.variants" v-if="picked">
                <input type="radio" :name="item.id" :id="variant" :value="variant" v-model="picked[i].value">
                {{ variant }}
            </div>
            <p v-if="produce">{{result[i].checked ? 'правильно' : 'не правильно ' }}</p>
        </div>
        <button class="btn-1" @click="submit">submit</button>
    </div>
    <!-- <div>
        <div v-for="item in answer">
            <p>{{ item.answer }}</p>
        </div>
    </div> -->
</template>
<script>
export default {
    data: () => ({
        question: null,
        answer: null,
        picked: null,
        result: null,
        produce: false  
    }),
    methods: {
        async getquestion() {
            const response = await fetch(`http://localhost:3000/questions`)
            const data = await response.json()
            this.question = await data
            this.picked = await data.map(item => ({
                value: null
            }))
        },
        async getanswer() {
            const response = await fetch(`http://localhost:3000/answers`)
            this.answer = await response.json()
        },
        submit() {
            this.result = this.answer.map ((item,i) =>  ({
                ...item,
                checked:this.picked[i].value === item.answer
            }))
            this.produce = true;
        }       
    },
    mounted() {
        this.getquestion()
        this.getanswer()
    },
}
</script>

<style>
.header{
    font-size: large;
    font-weight: bold;
}
body{
    margin: 0;
    padding: 0;
    background-image: url(https://t3.ftcdn.net/jpg/02/64/30/32/360_F_264303251_zEuPW8uTjTTY2wogztkQHxekcLRUdvXT.jpg);
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
}
.main {
    display: flex;
    justify-content: center;
    color: rgb(10, 10, 10);
 }
.main-block{
    font-size: 20px;

}
.variant{
    font-size: 20px;
    padding: 3px;
}
.btn-1{
    margin: 20px;
    font-family: monospace;
    background: linear-gradient(to left,#c31432,#240b36);
    text-decoration: none;
    padding: 20px 70px;
    border-radius: 10px;
    background-size: 200%;
    transition: .5s;
    color: white;
    font-size: 20px;

}   
.btn-1:hover {
    background-position: right;
    
}
</style>
