<template>
    <div class="card">
        <router-link to="/"><img class="homeBtn" src="/images/home.png" alt="asd"></router-link>
        <h1>짝맞추기</h1>
        <div class="timer">
            <div>
                <img src="/images/timer.png" alt="asd">
                <p>{{time}}s</p>
            </div>
            <button @click="start">Start</button>
        </div>
        <!-- v-bind:style="(firstnum===k || secondnum===k)?{transform: 'rotateY(180deg)'}:{} " -->
        <div class="game_screen">
            <div class="game_card0" v-for="(cardData, k) in cardData" :key="k" @click="cardBack(k)" :class="{'reverse': cardData.reverse}">
                <div class="game_card">
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
            cardData: [{ idx: 1, src: "img1.png", num: 0, reverse: false }, { idx: 2, src: "img2.png", num: 1, reverse: false }, { idx: 3, src: "img3.png", num: 2, reverse: false }, { idx: 4, src: "img4.png", num: 3, reverse: false }, { idx: 5, src: "img5.png", num: 4, reverse: false }, { idx: 6, src: "img6.png", num: 5, reverse: false }, { idx: 7, src: "img7.png", num: 6, reverse: false }, { idx: 8, src: "img8.png", num: 7, reverse: false }, { idx: 1, src: "img1.png", num: 8, reverse: false }, { idx: 2, src: "img2.png", num: 9, reverse: false }, { idx: 3, src: "img3.png", num: 10, reverse: false }, { idx: 4, src: "img4.png", num: 11, reverse: false }, { idx: 5, src: "img5.png", num: 12, reverse: false }, { idx: 6, src: "img6.png", num: 13, reverse: false }, { idx: 7, src: "img7.png", num: 14, reverse: false }, { idx: 8, src: "img8.png", num: 15, reverse: false }],
            isClick: null,
            isStart: false,
            firstidx: 0,
            secondidx: 0,
            firstnum: 20,
            secondnum: 20,
            firstroom:20,
            secondroom:20,
            isNum: 0,
            score:0,
            time:2
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
            this.cardData.forEach(card => {
                card.reverse = true;
            });
            setTimeout(() => {
                this.cardData.forEach(card => {
                    card.reverse = false;
                });
                this.isStart = true;
                const a = setInterval(()=>{
                    --this.time;
                    if(this.time==0){
                        alert("게임끝!")
                        this.time=60;
                        clearInterval(a);
                        this.isStart=false;
                    }
                },1000)
            }, 2000);
        },
        cardBack(k) {
            if(this.isStart){
                if(this.cardData[k].reverse) return;
                
                if (this.isNum == 0) {
                    this.firstidx = this.cardData[k].idx;
                    this.firstnum = this.cardData[k].num;
                    this.firstroom = k;
                    this.cardData[k].reverse = true;
                    ++this.isNum
                    
                } else if (this.isNum == 1) {
                    this.secondidx = this.cardData[k].idx;
                    this.secondnum = this.cardData[k].num;
                    this.secondroom = k;
                    this.cardData[k].reverse = true;
                    
                        if (this.firstnum != 20 && this.secondnum != 20 && this.firstidx == this.secondidx) {
                            this.isNum = 0;
                            this.firstnum = 20;
                            this.secondnum = 20;
                            ++this.score;
                            if(this.score==8){
                                alert("끝");
                                this.score=0;
                                this.isStart=false;
                            }
                        } else if (this.firstnum != 20 && this.secondnum != 20 && this.firstidx !== this.secondidx) {
                            ++this.isNum;
                            
                            setTimeout(() => {
                                    this.cardData[this.firstroom].reverse = false;
                                    this.cardData[this.secondroom].reverse = false;
                                    this.firstnum = 20;
                                    this.secondnum = 20;
                                    this.isNum = 0;
                            }, 500);
                        }
                }

            }
            
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
            width: 80px;
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
            &.reverse {
                transform: rotateY(180deg);
            }

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
                top: 0;

                img {
                    border-radius: 20px;
                    width: 100px;
                    height: 100px;
                }
            }
        }
    }


}
</style>