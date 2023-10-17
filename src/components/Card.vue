<script setup>
    import { ref } from 'vue';
    
    const advice = ref(null);

    const getAdvice = () => {
        fetch('https://api.adviceslip.com/advice')
            .then(response => response.json())
            .then(data => advice.value = data);
    }

    getAdvice();
</script>

<template>
    <div class="card">
        <div class="details" v-for="ad in advice" :key="ad.id">
            <p>Advice #{{ ad.id }}</p>
            <h1><q>{{ ad.advice }}</q></h1>
            <span><img src="../assets/pattern-divider-desktop.svg" alt="Divider" sizes="(max-width: 767px) 767w, 1440w" srcset="../assets/pattern-divider-mobile.svg 767w ,../assets/pattern-divider-desktop.svg 1440w"></span>
        </div>
        <div class="button" @click="getAdvice"><img src="../assets/icon-dice.svg" alt="Dice"></div>
    </div>
</template>

<style scoped>
    .card{
        position: relative;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        width: 530px;
        height: 330px;
        background: var(--dark-grayish-blue);
        border-radius: 10px;
        -webkit-box-shadow: 0px 10px 30px -10px rgba(0,0,0,.3);
        box-shadow: 0px 10px 30px -10px rgba(0,0,0,.3);
    }

    .details{
        padding: 10px 40px;
    }

    span img{
        width: 100%;
    }

    p{
        text-align: center;
        color: var(--neon-green);
        text-transform: uppercase;
        letter-spacing: 3.5px;
        font-size: 14px;
    }

    h1{
        margin: 30px 0;
        
        text-align: center;
        
        color: var(--light-cyan);
    }

    q{
        font-size: 28px;
        font-weight: 800;
    }

    .button{
        height: 65px;
        width: 65px;
        border-radius: 50%;
        background: var(--neon-green);
        padding: 20px;
        position: absolute;
        bottom: -35px;
    }

    .button:hover{
        filter: drop-shadow(0 0 10px var(--neon-green)) drop-shadow(0 0 30px var(--neon-green));
    }

    .button:active img{
        transform: scale(1.5) rotate(30deg);
    }

    .button img{
        width: 100%;
        object-fit: cover;
    }

    @media screen and (max-width: 767px){
        .card{
            width: 95%;
        }
    }
</style>