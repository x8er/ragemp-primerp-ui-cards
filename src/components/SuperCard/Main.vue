<template>
  <div class="main">
    <div class="left">
      <div class="description">
        <span class="title-small">Карточная игра</span>
        <span class="title">SuperCard</span>
        <span class="text"
          >Это карточная игра, в которойможно выйграть ценные игровые призы,
          копить обрывки и обменивать их на карты.</span
        >
      </div>
      <div class="amazing-big-btn" @click="$emit('opendaily')">
        <div class="content">
          <span>Начать игру</span>
          <img :src="require('@/assets/startgame.svg')" />
        </div>
      </div>
    </div>
    <div class="right">
      <img src="/supercardmain-cards.png" class="cards-image" />
      <div class="info">
        <div class="item">
          <span><span class="plus">+</span>Куча других призов продолжение</span>
        </div>
        <div class="item">
          <span
            ><span class="plus">+</span>Возможность выиграть другой
            автомобиль</span
          >
        </div>
        <div class="item">
          <span
            ><span class="plus">+</span>Ещё какое-нибудь плюс продолжение</span
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SuperCardMain",
};
</script>

<style lang="scss" scoped>
@font-face {
  font-family: Gilroy;
  src: url("~@/assets/Gilroy-SemiBold.ttf");
}

@font-face {
  font-family: Gilroy;
  src: url("~@/assets/Gilroy-Medium.ttf");
  font-weight: 300;
}

@font-face {
  font-family: Gilroy;
  src: url("~@/assets/Gilroy-Bold.ttf");
  font-weight: bold;
}

.main {
  box-sizing: border-box;
  padding: 1.5625vw 0.8854166667vw 0 3.2291666667vw;
  display: flex;
  justify-content: space-between;
  width: 100%;
  font-family: Gilroy;
  font-size: 0.9375vw;

  .amazing-big-btn {
    box-sizing: border-box;
    padding: 0.1041666667vw;
    display: inline-block;
    border-radius: 0.5208333333vw;
    background: linear-gradient(268.02deg, #256fff 0%, #50a0ff 100%);
    box-shadow: 0px 1.1979166667vw 2.5520833333vw -0.7291666667vw #5f65ff;
    margin-top: 2.0833333333vw;
    transition: transform 0.2s ease;

    .content {
      padding: 0 0.9375vw;
      display: flex;
      align-items: center;
      border-radius: inherit;
      background: linear-gradient(268.02deg, #256fff 0%, #2548ff 100%);

      span {
        font-size: 1.25vw;
        line-height: 4.0625vw;
        margin: 0 2.6041666667vw;
      }

      img {
        display: block;
        width: 2.65625vw;
      }
    }

    &:hover {
      transform: scale(1.1);
    }
  }

  .left {
    margin-top: 2.5520833333vw;

    .description {
      span {
        display: block;
      }

      .title {
        font-weight: bold;
        font-size: 3.3333333333vw;
        line-height: 1;
        position: relative;

        &-small {
          font-size: 1.875vw;
        }

        &::before {
          content: "SuperCard";
          font-size: 5vw;
          opacity: 0.04;
          position: absolute;
          top: 50%;
          transform: translateY(-50%);
        }
      }

      .text {
        font-weight: 300;
        font-size: 1.25vw;
        margin-top: 1.0416666667vw;
      }
    }
  }

  .right {
    .cards-image {
      display: block;
      width: 45.3125vw;
    }

    .info {
      display: flex;
      width: 36.25vw;
      height: 4.3229166667vw;
      background-color: rgba(255, 255, 255, 0.03);
      border-radius: 0.4166666667vw;
      margin: 0 auto;
      transform: translateY(-2.0833333333vw);
      position: relative;

      &::before {
        content: "i";
        width: 0.9895833333vw;
        line-height: 0.9895833333vw;
        text-align: center;
        font-weight: bold;
        border-radius: 50%;
        background-color: rgba(255, 255, 255, 0.09);
        position: absolute;
        left: -1.25vw;
        top: 0;
      }

      .item {
        box-sizing: border-box;
        padding: 0 0.5208333333vw;
        display: flex;
        align-items: center;
        text-align: center;
        color: rgba(255, 255, 255, 0.5);

        .plus {
          color: #ffee51;
          margin-right: 0.2604166667vw;
        }

        &:nth-child(2) {
          position: relative;

          &::before,
          &::after {
            content: "";
            width: 1px;
            height: 3.3854166667vw;
            background-color: rgba(255, 255, 255, 0.05);
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
          }

          &::before {
            left: 0;
          }

          &::after {
            right: 0;
          }
        }
      }
    }
  }
}
</style>