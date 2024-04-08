<template>
    <div class="card">
        <router-link to="/"><img class="homeBtn" src="/images/home.png" alt="asd"></router-link>
        <h1>짝맞추기</h1>
        <div class="timer">
            <div>
                <img src="/images/timer.png" alt="asd">
                <p>60s</p>
            </div>
            <button @click="start">Start</button>
        </div>
        <div class="game_screen">
            <div class="game_card0" v-for="(cardData, k) in cardData" :key="k" @click="cardBack(k)" v-bind:style="isClick===k?{transform: 'rotateY(180deg)'}:{} ">
                <div class="game_card" >
                    <img src="/images/card.png" alt="aa">
                </div>
                <div class="game_card2">
                    <img :src="'/images/' + cardData.src" :alt="'Card ' + cardData.idx">
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            cardData: [{ idx: 1, src: "img1.png" }, { idx: 2, src: "img2.png" }, { idx: 3, src: "img3.png" }, { idx: 4, src: "img4.png" }, { idx: 5, src: "img5.png" }, { idx: 6, src: "img6.png" }, { idx: 7, src: "img7.png" }, { idx: 8, src: "img8.png" }, { idx: 1, src: "img1.png" }, { idx: 2, src: "img2.png" }, { idx: 3, src: "img3.png" }, { idx: 4, src: "img4.png" }, { idx: 5, src: "img5.png" }, { idx: 6, src: "img6.png" }, { idx: 7, src: "img7.png" }, { idx: 8, src: "img8.png" }],
            isClick:null,
            isStart : false
        }
    },
    methods: {
        start() {
            let cardArr = [...this.cardData];
            for (let i = 0; i < cardArr.length; i++) {
                const num = Math.floor(Math.random() * (i + 1));
                [cardArr[i], cardArr[num]] = [cardArr[num], cardArr[i]];
            }
            this.cardData = cardArr;
        },
        cardBack(k){
            this.isClick = k;
            // if(this.isClick===k){
            
            //     this.isClick = null;
            // } else{
            
            //     this.isClick = k;
            // }
            
        }
    },

}
</script>

<style lang="scss" scoped>
.card {
    position: relative;
    text-align: center;
    margin: 0 200px;

    h1 {
        font-size: 40px;
        padding: 60px 0;
    }

    .homeBtn {
        position: absolute;
        top: 20px;
        right: -160px;
    }

    .timer {
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 10px;
        margin: 0 70px 20px 70px;

        >div {
            display: flex;
            align-items: center;
            gap: 10px;

            img {
                width: 25px;
            }

            p {
                font-size: 20px;
            }
        }

        button {
            border: none;
            width: 60px;
            height: 30px;
            background-color: #FFA722;
            color: white;
            font-weight: bolder;
            font-size: 18px;
        }

    }

    .game_screen {
        width: 500px;
        height: 500px;
        margin: 0 auto;

        display: flex;
        gap: 33px;
        flex-wrap: wrap;
        align-items: center;
        justify-content: center;
        
        .game_card0 {
            transition: transform 0.3s;
            transform-style: preserve-3d;
            
            
            >div {
                backface-visibility: hidden;               
            }

            .game_card {
                img {
                    border-radius: 20px;
                    width: 100px;
                    height: 100px;
                }
            }

            .game_card2 {
                transform: rotateY(180deg);
                position: absolute;
                top:0;
                img {
                    border-radius: 20px;
                    width: 100px;
                    height: 100px;
                }
            }
        }
    }

    
}</style>