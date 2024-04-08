<template>
    <div class="rsp">
        <router-link to="/"><img class="homeBtn" src="/images/home.png" alt="asd"></router-link>
        <h1>가위바위보</h1>
        <div class="score">
            <p><img src="/images/score.png" alt="asd">Score</p>
            <div>
                <p>Computer : {{ computer_score }}점</p>
                <p>Player : {{ player_score }}점</p>
            </div>
        </div>
        <div class="rsp_game">
            <div class="game_screen">
                <div class="result">
                    <div class="computer">
                        <!-- <img v-if="computer_result==1" src="/images/rsp.png" alt=""> -->
                        <img v-if="computer_picture == 0" src="/images/rock.png" alt="">
                        <img v-else-if="computer_picture == 1" src="/images/scissors.png" alt="">
                        <img v-else-if="computer_picture == 2" src="/images/paper.png" alt="">
                        <p>Computer</p>
                    </div>
                    <div class="player">
                        <img v-if="player_result == 1" src="/images/rsp.png" alt="">
                        <img v-else-if="player_result == 0" src="/images/rock.png" alt="">
                        <img v-else-if="player_result == 2" src="/images/scissors.png" alt="">
                        <img v-else-if="player_result == 5" src="/images/paper.png" alt="">
                        <p>Player</p>
                    </div>
                </div>
                <div class="result_text">
                    <p v-if="isVictory == 0">선택해주세요</p>
                    <p v-else-if="isVictory == 2">좀하시네요</p>
                    <p v-else-if="isVictory == 3">이걸지네 ㅋㅋ</p>
                    <p v-else-if="isVictory == 1">비겼습니다 다시!</p>
                </div>
                <button v-if="computer_result!==1" @click="reStart">다시하기</button>
            </div>
            <div class="game_play">
                <img @click="rockClick" src="/images/rock.png" alt="">
                <img @click="scissorsClick" src="/images/scissors.png" alt="">
                <img @click="paperClick" src="/images/paper.png" alt="">
            </div>
        </div>
    </div>
</template>

<script>
export default {

    data() {
        return {
            computer_score: 0,
            player_score: 0,
            rock_data: 0,
            scissors_data: 2,
            paper_data: 5,
            computer_result: 1,
            player_result: 1,
            computer_data: [0, 2, 5],
            isVictory: 0,   //0시작 , 1비김, 2이김, 3짐,
            computer_picture: 0
        }
    },
    mounted() {
        setInterval(this.incrementComputerPicture, 100);
    },
    methods: {
        reStart(){
            this.computer_result=1;
        },
        incrementComputerPicture() {
            if(this.computer_result==1){
                this.computer_picture++;
                    if (this.computer_picture === 3) {
                        this.computer_picture = 0;
                    }
        } else if(this.computer_result==0){
            this.computer_picture = 0;
        } else if(this.computer_result==2){
            this.computer_picture = 1;
        }else if(this.computer_result==5){
            this.computer_picture = 2;
        }
        }
        ,
        rockClick() {
            this.player_result = this.rock_data;
            this.computer_result = this.computer_data[Math.floor(Math.random() * this.computer_data.length)];
            if (this.computer_result == 0) {
                this.isVictory = 1;
            } else if (this.computer_result == 2) {
                this.isVictory = 2;
                ++this.player_score;
            } else if (this.computer_result == 5) {
                this.isVictory = 3;
                ++this.computer_score;
            }
        },
        scissorsClick() {
            this.player_result = this.scissors_data;
            this.computer_result = this.computer_data[Math.floor(Math.random() * this.computer_data.length)];
            if (this.computer_result == 0) {
                this.isVictory = 3;
                ++this.computer_score;
            } else if (this.computer_result == 2) {
                this.isVictory = 1;
            } else if (this.computer_result == 5) {
                this.isVictory = 2;
                ++this.player_score;
            }
        },
        paperClick() {
            this.player_result = this.paper_data;
            this.computer_result = this.computer_data[Math.floor(Math.random() * this.computer_data.length)];
            if (this.computer_result == 0) {
                this.isVictory = 2;
                ++this.player_score;
            } else if (this.computer_result == 2) {
                this.isVictory = 3;
                ++this.computer_score;
            } else if (this.computer_result == 5) {
                this.isVictory = 1;
            }
        }

    },
    computed: {

    }
}
</script>

<style lang="scss" scoped>
.rsp {
    position: relative;
    text-align: center;
    margin: 0 100px;

    h1 {
        font-size: 40px;
        padding: 80px 0;
    }

    .homeBtn {
        position: absolute;
        top: 20px;
        right: 0;
    }

    .score {
        display: flex;
        width: 600px;

        justify-content: space-between;
        align-items: center;

        >p {
            img {
                margin-right: 20px;
                height: 20px;
            }

            font-size: 24px;
        }

        >div {
            display: flex;
            gap: 30px;
        }
    }

    .rsp_game {
        display: flex;
        justify-content: space-between;

        .game_screen {
            width: 600px;
            height: 400px;
            background: #F1F1F1;
            border-radius: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 50px;
            button{
                width:200px;
                height:60px;
                border:none;
                border-radius: 10px;
                background-color: #FEDB21;
                color:white;
                position: absolute;
                bottom:10px;
                font-size: 20px;
            }
            .result {
                display: flex;
                align-items: center;
                justify-content: center;
                gap: 100px;
            }

            .result_text {
                width: 200px;
                height: 60px;
                background-color: #CC3333;
                color: white;
                border-radius: 10px;
                display: flex;
                align-items: center;
                justify-content: center;
                font-size: 20px;
            }
        }

        .game_play {
            display: flex;
            flex-direction: column;
            justify-content: space-evenly;

            img {
                display: block;
            }
        }
    }
}
</style>