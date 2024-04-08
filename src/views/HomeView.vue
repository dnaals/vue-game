<template>
  <div class="home_list">
    <h1>Game</h1>
    <h2>게임을 선택해 주세용</h2>
    <div class="list_fl">
      <router-link :to="{ name: 'list', query: { game: 'rsp' } }">
        <div class="game_list">
          <img src="/images/game1.png" alt="asd">
          <p>가위바위보</p>
        </div>
      </router-link>
      <router-link :to="{ name: 'list', query: { game: 'card' } }">
        <div class="game_list">
          <img src="/images/img3.png" alt="asd">
          <p>짝맞추기게임</p>
        </div>
      </router-link>
    </div>

  </div>
</template>

<script>
export default {
  name: 'HomeView',
}

</script>

<style lang="scss" scoped>
.home_list {
  width: 1024px;
  height: 768px;
  margin: 0 auto;
  text-align: center;
  margin-top:100px;
  h1{
    font-size:100px;
    margin: 30px 0;
    font-weight: bold;
  }
  h2{
    font-size: 20px;
    margin:30px 0;
  }
  .list_fl {
    display: flex;
    justify-content: center;
    gap:80px;
    margin:100px 0;
    a {
      .game_list {
        width: 300px;
        height: 300px;
        background: #FFFFFF;
        box-shadow: 10px 10px 4px rgba(0, 0, 0, 0.25);
        border-radius: 20px 0px 20px 20px;
        display:flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        gap:20px;
        img{
          width:150px;
        }
        p{
          font-size: 20px;
          font-weight: bold;
        }
      }

    }
  }
}
</style>