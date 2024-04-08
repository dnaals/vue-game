<template>
  <div class="list">

    <CardGame v-if="isCard" />
    <RspGame v-if="isRsp" />
  </div>
</template>

<script>
import CardGame from "@/components/CardGame.vue";
import RspGame from "@/components/RspGame.vue";

export default {
  name: 'ListView',
  components: { CardGame, RspGame },
  data() {
    return {
      isCard: this.$route.query.game=="card",
      isRsp : this.$route.query.game=="rsp"
    }
  }
}
</script>

<style lang="scss" scoped>
.list {
  width: 1024px;
  height: 768px;
  background-color: white;
  margin: 50px auto;
  border-radius: 20px;
}
</style>