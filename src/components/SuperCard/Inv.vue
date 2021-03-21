<template>
  <div class="inv">
    <div class="card-list">
      <div
        class="card"
        :class="[
          item.type,
          {
            'to-dust': toDustAnimateIndex === index,
            'to-use': toUseAnimateIndex === index,
          },
        ]"
        v-for="(item, index) of devided[currentPage]"
        :key="index"
      >
        <div class="content" :class="{ 'info-open': openedInfo === index }">
          <img :src="item.image" />
          <div class="data">
            <span class="type" v-if="item.type === null">Восхитительный</span>
            <span class="type" v-if="item.type === 'ultra'">Ультра</span>
            <span class="type" v-if="item.type === 'legend'">Легендарный</span>
            <span>{{ item.title }}</span>
          </div>
          <div class="info">
            <span class="title" v-if="item.type === null">{{
              item.title
            }}</span>
            <span class="title" v-if="item.type === 'ultra'">{{
              item.title
            }}</span>
            <span class="title" v-if="item.type === 'legend'">{{
              item.title
            }}</span>
            <p class="text">{{ item.text }}</p>
          </div>
        </div>
        <div class="controls">
          <div
            class="btn to-dust"
            @click="
              toDustConfirmOpen = true;
              toDustConfirmIndex = index;
            "
          >
            В пыль
          </div>
          <div class="btn use" v-if="item.isCollected" @click="toUse(index)">
            Использовать
          </div>
          <div class="btn" v-else>
            {{ item.parts[0] }}/{{ item.parts[1] }} собрано
          </div>
        </div>
        <div class="rarity"></div>
        <img
          class="info-btn"
          :src="require('@/assets/info-btn.svg')"
          @click="openInfo(index)"
        />
      </div>
    </div>
    <div class="pages">
      <div class="box" @click="prevPage()">
        <img :src="require('@/assets/page-arrow.svg')" />
      </div>
      <div class="list">
        <div
          class="box"
          :class="{ current: currentPage === index }"
          v-for="(item, index) of devided"
          :key="index"
          @click="
            currentPage = index;
            openedInfo = null;
          "
        >
          <span style="text-align: center">{{ index + 1 }}</span>
        </div>
      </div>
      <div class="box" @click="nextPage()">
        <img :src="require('@/assets/page-arrow.svg')" />
      </div>
    </div>
    <div class="lightout" v-if="safeAnimation"></div>
    <div
      class="blackout"
      v-show="toDustConfirmOpen"
      @click.self="
        toDustConfirmOpen = false;
        toDustConfirmIndex = null;
      "
    >
      <div class="to-dust-confirm">
        <span class="title">Разрыв карты</span>
        <span class="text"
          >За эту карточку вы получите
          <span class="colored">95</span> обрывков.</span
        >
        <div class="amazing-btn" @click="toDust()">
          <div class="content">
            <span>Разорвать</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SuperCardInv",
  data() {
    return {
      INCOMING_CARDS: [
        {
          title: "VIP на 6 дней",
          text: "Некоторый текстик",
          type: "legend",
          image: "/test-car.png",
          isCollected: false,
          parts: [3, 6],
        },
        {
          title: "VIP на 6 дней",
          text: "Некоторый текстик",
          type: "ultra",
          image: "/test-car.png",
          isCollected: true,
          parts: null,
        },
        {
          title: "VIP на 6 дней",
          text: "Некоторый текстик",
          type: null,
          image: "/test-car.png",
          isCollected: false,
          parts: [1, 12],
        },
        {
          title: "VIP на 6 дней",
          text: "Некоторый текстик",
          type: "legend",
          image: "/test-car.png",
          isCollected: false,
          parts: [3, 6],
        },
        {
          title: "VIP на 6 дней",
          text: "Некоторый текстик",
          type: "ultra",
          image: "/test-car.png",
          isCollected: true,
          parts: null,
        },
        {
          title: "VIP на 6 дней",
          text: "Некоторый текстик",
          type: null,
          image: "/test-car.png",
          isCollected: false,
          parts: [1, 12],
        },
        {
          title: "VIP на 6 дней",
          text: "Некоторый текстик",
          type: "ultra",
          image: "/test-car.png",
          isCollected: true,
          parts: null,
        },
        {
          title: "VIP на 6 дней",
          text: "Некоторый текстик",
          type: null,
          image: "/test-car.png",
          isCollected: false,
          parts: [1, 12],
        },
        {
          title: "VIP на 6 дней",
          text: "Некоторый текстик",
          type: "legend",
          image: "/test-car.png",
          isCollected: false,
          parts: [3, 6],
        },
        {
          title: "VIP на 6 дней",
          text: "Некоторый текстик",
          type: "ultra",
          image: "/test-car.png",
          isCollected: true,
          parts: null,
        },
        {
          title: "VIP на 6 дней",
          text: "Некоторый текстик",
          type: "legend",
          image: "/test-car.png",
          isCollected: false,
          parts: [3, 6],
        },
        {
          title: "VIP на 6 дней",
          text: "Некоторый текстик",
          type: "ultra",
          image: "/test-car.png",
          isCollected: true,
          parts: null,
        },
      ],
      currentPage: 0,
      openedInfo: null,
      safeAnimation: false,
      toDustConfirmOpen: false,
      toDustConfirmIndex: null,
      toDustAnimateIndex: null,
      toUseAnimateIndex: null,
    };
  },
  computed: {
    devided() {
      const ARR = [];
      for (let i = 0; i < Math.ceil(this.INCOMING_CARDS.length / 10); i++) {
        ARR[i] = this.INCOMING_CARDS.slice(i * 10, (i + 1) * 10);
      }
      return ARR;
    },
  },
  methods: {
    openInfo(index) {
      if (this.openedInfo === index) {
        this.openedInfo = null;
      } else {
        this.openedInfo = index;
      }
    },
    prevPage() {
      if (!this.currentPage) return;
      this.currentPage--;
      this.openedInfo = null;
    },
    nextPage() {
      if (this.currentPage === this.devided.length - 1) return;
      this.currentPage++;
      this.openedInfo = null;
    },
    toDust() {
      this.toDustConfirmOpen = false;
      this.toDustAnimateIndex = this.toDustConfirmIndex;
      this.toDustConfirmIndex = null;
      this.safeAnimation = true;
      this.openedInfo = null;
      setTimeout(() => {
        this.INCOMING_CARDS.splice(
          this.currentPage * 10 + this.toDustAnimateIndex,
          1
        );

        this.toDustAnimateIndex = null;
        this.safeAnimation = false;
      }, 500);
    },
    toUse(index) {
      this.toUseAnimateIndex = index;
      this.safeAnimation = true;
      this.openedInfo = null;
      setTimeout(() => {
        this.INCOMING_CARDS.splice(
          this.currentPage * 10 + this.toUseAnimateIndex,
          1
        );

        this.toUseAnimateIndex = null;
        this.safeAnimation = false;
      }, 500);
    },
  },
};
</script>

<style lang="scss" scoped>
@font-face {
  font-family: Gilroy;
  src: url("~@/assets/Gilroy-SemiBold.ttf");
}

@font-face {
  font-family: Gilroy;
  src: url("~@/assets/Gilroy-Bold.ttf");
  font-weight: bold;
}

.inv {
  box-sizing: border-box;
  padding: 0 2.7604166667vw;
  height: 32.5520833333vw;
  font-family: Gilroy;
  font-size: 0.9375vw;
  position: relative;

  .card-list {
    display: flex;
    flex-wrap: wrap;

    .card {
      box-sizing: border-box;
      padding: 0.3645833333vw;
      margin-right: 2.1354166667vw;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      border-radius: 0.4166666667vw;
      width: 11.5625vw;
      height: 13.6458333333vw;
      background-color: rgba(255, 255, 255, 0.03);
      position: relative;
      transition: transform 0.5s ease, opacity 0.5s ease;

      &:nth-child(5n) {
        margin-right: 0;
      }

      &:nth-child(n + 6) {
        margin-top: 2.1354166667vw;
      }

      &.to-use {
        // transform: translateY(-1.5625vw);
        transform: scale(1.2);
        opacity: 0;
      }

      &.to-dust {
        transform: scale(0.8);
        opacity: 0;
      }

      &.ultra {
        .content {
          .data {
            .type {
              background: linear-gradient(268.02deg, #ffaa2b 0%, #ff5925 100%);
              background-clip: text;
            }
          }

          .info .title {
            background: linear-gradient(268.02deg, #ffaa2b 0%, #ff5925 100%);
            background-clip: text;
          }
        }
        .rarity {
          background: linear-gradient(268.02deg, #ffaa2b 0%, #ff5925 100%);
        }
      }

      &.legend {
        .content {
          .data .type {
            background: linear-gradient(268.02deg, #ff2b77 0%, #9f25ff 100%);
            background-clip: text;
          }

          .info .title {
            background: linear-gradient(268.02deg, #ff2b77 0%, #9f25ff 100%);
            background-clip: text;
          }
        }

        .rarity {
          background: linear-gradient(268.02deg, #ff2b77 0%, #9f25ff 100%);
        }
      }

      .content {
        display: flex;
        flex-direction: column;
        justify-content: flex-end;
        align-items: center;
        height: 10.4166666667vw;
        border-radius: inherit;
        background-color: rgba(0, 0, 0, 0.06);
        position: relative;

        &.info-open {
          img {
            opacity: 0;
          }

          .data {
            opacity: 0;
          }

          .info {
            opacity: 1;
          }
        }

        img {
          display: block;
          max-width: 100%;
          transition: opacity 0.2s ease;
        }

        .data {
          box-sizing: border-box;
          padding-left: 0.5208333333vw;
          width: 100%;
          margin: 0.9375vw 0 0.5208333333vw 0;
          transition: opacity 0.2s ease;

          span {
            display: block;
            font-weight: bold;
          }

          .type {
            background: linear-gradient(268.02deg, #2bb2ff 0%, #5e25ff 100%);
            background-clip: text;
            -webkit-text-fill-color: transparent;
          }
        }

        .info {
          box-sizing: border-box;
          padding: 2.7083333333vw 0 0 1.0416666667vw;
          display: flex;
          flex-direction: column;
          width: 100%;
          height: 100%;
          opacity: 0;
          transition: opacity 0.2s ease;
          position: absolute;

          .title {
            font-weight: bold;
            background: linear-gradient(268.02deg, #2bb2ff 0%, #5e25ff 100%);
            background-clip: text;
            -webkit-text-fill-color: transparent;
          }

          .text {
            font-size: 0.7291666667vw;
            color: rgba(255, 255, 255, 0.51);
          }
        }
      }

      .controls {
        display: flex;

        .btn {
          display: flex;
          justify-content: center;
          align-items: center;
          font-size: 0.7291666667vw;
          width: 50%;
          height: 1.8229166667vw;
          border-radius: 0.1041666667vw;
          background-color: rgba(255, 255, 255, 0.06);

          &.to-dust {
            background-color: rgba(0, 0, 0, 0.16);

            &:hover {
              background-color: #e43c3a;
              box-shadow: 0px 1.1979166667vw 2.5520833333vw -0.7291666667vw #ff5151;
            }
          }

          &.use:hover {
            background: linear-gradient(268.02deg, #256fff 0%, #2548ff 100%);
            box-shadow: 0px 1.1979166667vw 2.5520833333vw -0.7291666667vw #5f65ff;
          }
        }
      }

      .rarity {
        background: linear-gradient(268.02deg, #256fff 0%, #2548ff 100%);
        border-radius: 0.15625vw;
        width: 0.46875vw;
        height: 0.46875vw;
        position: absolute;
        top: 0.6770833333vw;
        left: 0.6770833333vw;
      }

      .info-btn {
        display: block;
        width: 0.78125vw;
        height: 0.78125vw;
        position: absolute;
        top: 0.6770833333vw;
        right: 0.6770833333vw;
      }
    }
  }

  .pages {
    display: flex;
    position: absolute;
    left: 50%;
    bottom: 1.1979166667vw;
    transform: translateX(-50%);

    .box {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 0.78125vw;
      height: 0.8333333333vw;
      background-color: rgba(255, 255, 255, 0.04);
      border-radius: 0.15625vw;
      font-size: 0.7291666667vw;
      color: rgba(255, 255, 255, 0.11);
      margin: 0 0.4166666667vw;

      img {
        display: block;
        width: 0.2083333333vw;
      }

      &.current,
      &:hover {
        background-color: #ffffff;
        box-shadow: 0px 0.2083333333vw 0.8333333333vw 0.0520833333vw
          rgba(255, 255, 255, 0.25);
        color: #363636;
      }
    }

    > .box:last-child {
      img {
        transform: rotate(180deg);
      }
    }

    .list {
      display: flex;

      .box {
        margin: 0 0.15625vw;
      }
    }
  }

  .blackout {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    background: linear-gradient(
      0deg,
      rgba(0, 0, 0, 1) 0%,
      rgba(0, 0, 0, 0) 100%
    );
    border-bottom-left-radius: 0.5208333333vw;
    border-bottom-right-radius: 0.5208333333vw;
    position: absolute;
    left: 0;
    top: 0;
  }

  .lightout {
    width: 100%;
    height: 100%;
    position: absolute;
    left: 0;
    top: 0;
  }

  .to-dust-confirm {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 19.1666666667vw;
    height: 13.2291666667vw;
    border-radius: 0.5208333333vw;
    background: linear-gradient(
      68.5deg,
      rgba(22, 40, 103, 1) 0%,
      #040d2d 85.15%
    );

    .title {
      font-size: 1.875vw;
    }

    .text {
      display: inline-block;
      margin-top: 1.5625vw;
      margin-bottom: 1.875vw;
      font-size: 0.7291666667vw;

      .colored {
        color: #ffee51;
      }
    }

    .amazing-btn {
      box-sizing: border-box;
      border: 0.1041666667vw solid rgba(80, 160, 255, 0.37);
      border-radius: 0.5208333333vw;

      .content {
        padding: 0 1.3541666667vw;
        border-radius: inherit;

        span {
          line-height: 2.3958333333vw;
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
  }
}
</style>