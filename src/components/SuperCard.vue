<template>
  <div class="supercard">
    <header>
      <div class="logo">
        <img :src="require('@/assets/logo.svg')" />
        <span v-show="current === 'SuperCardMain'">Главное меню</span>
        <span v-show="current === 'SuperCardDaily'">Ежедневный приз</span>
        <span v-show="current === 'SuperCardShop'">Магазин</span>
        <span v-show="current === 'SuperCardInv'">Мои карты</span>
      </div>
      <nav>
        <div class="dust-counter">
          <img :src="require('@/assets/dust.svg')" />
          <span>Ваша пыль: 495</span>
        </div>
        <div class="amazing-btn" @click="current = 'SuperCardInv'">
          <div class="content">
            <span>Мои карты</span>
          </div>
        </div>
        <div class="amazing-btn" @click="current = 'SuperCardShop'">
          <div class="content">
            <span>Магазин</span>
          </div>
        </div>
      </nav>
    </header>
    <component
      :is="current"
      @opendaily="current = 'SuperCardDaily'"
    ></component>
  </div>
</template>

<script>
import SuperCardMain from "@/components/SuperCard/Main.vue";
import SuperCardDaily from "@/components/SuperCard/Daily.vue";
import SuperCardShop from "@/components/SuperCard/Shop.vue";
import SuperCardInv from "@/components/SuperCard/Inv.vue";

export default {
  name: "SuperCard",
  data() {
    return {
      current: "SuperCardMain",
    };
  },
  components: {
    SuperCardMain,
    SuperCardDaily,
    SuperCardShop,
    SuperCardInv,
  },
};
</script>

<style lang="scss" scoped>
@font-face {
  font-family: Gilroy;
  src: url("~@/assets/Gilroy-SemiBold.ttf");
}

.supercard {
  width: 72.03125vw;
  height: 38.2291666667vw;
  background-image: url("~@/assets/bg.png");
  background-size: cover;
  color: #ffffff;

  .amazing-btn {
    box-sizing: border-box;
    border: 0.1041666667vw solid rgba(80, 160, 255, 0.37);
    border-radius: 0.5208333333vw;

    .content {
      padding: 0 1.3541666667vw;
      border-radius: inherit;

      span {
        line-height: 1.71875vw;
      }
    }

    &:hover {
      border: 0;
      padding: 0.1041666667vw;
      background: linear-gradient(268.02deg, #256fff 0%, #50a0ff 100%);
      box-shadow: 0px 1.1979166667vw 2.5520833333vw -0.7291666667vw #5f65ff;

      .content {
        background: linear-gradient(268.02deg, #256fff 0%, #2548ff 100%);
      }
    }
  }

  header {
    box-sizing: border-box;
    padding: 0 2.8125vw 0 3.2291666667vw;
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 5.6770833333vw;
    font-family: Gilroy;
    font-size: 0.9375vw;

    .logo {
      display: flex;
      align-items: center;
      position: relative;
      z-index: 1;

      img {
        display: block;
        width: 1.6666666667vw;
        position: relative;
        z-index: 3;
      }

      &::before {
        content: "";
        width: 2.6041666667vw;
        height: 2.6041666667vw;
        position: absolute;
        left: -0.625vw;
        top: 0.9375vw;
        background: radial-gradient(
          circle,
          rgba(255, 95, 95, 0.3) 0%,
          rgba(255, 255, 255, 0) 70%
        );
        z-index: 2;
      }

      span {
        margin-left: 0.2604166667vw;
        font-size: 1.25vw;
      }
    }

    nav {
      display: flex;

      .dust-counter {
        display: flex;
        align-items: center;
        margin-right: 1.6666666667vw;

        img {
          display: block;
          width: 0.7291666667vw;
        }

        span {
          margin-left: 0.4166666667vw;
        }
      }

      .amazing-btn:last-child {
        margin-left: 0.8854166667vw;
      }
    }
  }
}
</style>