<template>
  <div class="daily">
    <div class="card-list">
      <div
        class="card"
        :class="{
          selected:
            selectedCards.includes(index) ||
            (remainingCards.includes(index) && showRemainingCards),
        }"
        v-for="(item, index) of INCOMING_CARDS"
        :key="index"
        @click="selectCard(index)"
      >
        <div class="content">
          <div class="front" :class="[item.type]">
            <div class="container">
              <img :src="item.image" />
              <div class="info">
                <span class="title">{{ item.title }}</span>
                <span class="win">{{ item.win }}</span>
              </div>
            </div>
          </div>
          <div class="back">
            <img src="/supercarddaily-card.svg" />
          </div>
        </div>
      </div>
    </div>
    <div class="controls">
      <div class="amazing-btn" style="visibility: hidden">
        <div class="content">
          <span>Пересдать</span>
        </div>
      </div>
      <div
        class="amazing-btn"
        @click="selectedCards.length === 3 ? (showRemainingCards = true) : null"
      >
        <div class="content">
          <span>Вскрыть карты</span>
        </div>
      </div>
      <div class="amazing-btn" style="visibility: hidden">
        <div class="content">
          <span>Подсмотреть</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SuperCardDaily",
  data() {
    return {
      INCOMING_CARDS: [
        {
          title: "Автомобиль",
          win: "Lamborghini",
          image: "/test-car.png",
          type: "legend",
        },
        {
          title: "Деньги",
          win: "$ 100.000.000",
          image: "/test-car.png",
          type: null,
        },
        {
          title: "Статус",
          win: "VIP на 30 дней",
          image: "/test-car.png",
          type: "gold",
        },
        {
          title: "Деньги",
          win: "$ 100.000.000",
          image: "/test-car.png",
          type: null,
        },
        {
          title: "Статус",
          win: "VIP на 30 дней",
          image: "/test-car.png",
          type: "gold",
        },
        {
          title: "Деньги",
          win: "$ 100.000.000",
          image: "/test-car.png",
          type: null,
        },
        {
          title: "Статус",
          win: "VIP на 30 дней",
          image: "/test-car.png",
          type: "gold",
        },
        {
          title: "Деньги",
          win: "$ 100.000.000",
          image: "/test-car.png",
          type: null,
        },
      ],
      selectedCards: [],
      showRemainingCards: false,
    };
  },
  computed: {
    remainingCards() {
      if (this.selectedCards.length < 3) {
        return [];
      }
      return this.INCOMING_CARDS.reduce((acc, el, index) => {
        if (!this.selectedCards.includes(index)) {
          acc.push(index);
        }
        return acc;
      }, []);
    },
  },
  methods: {
    selectCard(index) {
      if (this.selectedCards.length < 3 && !this.selectedCards.includes(index))
        this.selectedCards.push(index);
    },
  },
};
</script>

<style lang="scss" scoped>
@font-face {
  font-family: Gilroy;
  src: url("~@/assets/Gilroy-SemiBold.ttf");
}

.daily {
  box-sizing: border-box;
  padding: 0 11.3541666667vw;
  font-family: Gilroy;
  font-size: 0.9375vw;

  .amazing-btn {
    box-sizing: border-box;
    border: 0.1041666667vw solid rgba(80, 160, 255, 0.37);
    border-radius: 0.2083333333vw;
    margin: 0 0.5208333333vw;

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

  .card-list {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;

    .card {
      perspective: 41.6666666667vw;
      margin-bottom: 1.0416666667vw;

      &.selected .content {
        .front {
          transform: rotateY(0deg);
        }

        .back {
          transform: rotateY(-180deg);
        }
      }

      .content {
        position: relative;
        width: 11.5625vw;
        height: 13.6458333333vw;

        .front,
        .back {
          width: inherit;
          height: inherit;
          border-radius: 0.4166666667vw;
          position: absolute;
          top: 0;
          left: 0;
          backface-visibility: hidden;
          transform: rotateY(180deg);
          transition: transform 1s ease;
        }

        .front {
          box-sizing: border-box;
          padding: 0.1041666667vw;
          background: linear-gradient(
            211.88deg,
            rgba(57, 125, 255, 0.7) 0%,
            rgba(9, 28, 56, 0.71) 100%
          );
          box-shadow: 0px 1.1979166667vw 2.5520833333vw -0.7291666667vw rgba(95, 101, 255, 0.5);

          .container {
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
            align-items: center;
            width: 100%;
            height: 100%;
            border-radius: inherit;
            background: linear-gradient(
                180deg,
                #0a1422 0%,
                rgba(9, 28, 56, 0.71) 100%
              ),
              url("/supercarddaily-card.png");

            img {
              display: block;
              max-width: 100%;
            }

            .info {
              margin-top: 1.5625vw;
              margin-bottom: 0.625vw;

              span {
                display: block;

                &.win {
                  font-size: 1.25vw;
                  color: #51e0ff;
                }
              }
            }
          }

          &::after {
            content: "";
            height: 0.1041666667vw;
            width: 6.4583333333vw;
            background-color: #51e0ff;
            position: absolute;
            left: 50%;
            bottom: 0;
            transform: translateX(-50%);
            box-shadow: 0 -0.3645833333vw 4.0104166667vw 0.5208333333vw rgba(81, 224, 255, 0.75);
          }

          &.gold {
            background: linear-gradient(
              211.88deg,
              rgba(255, 238, 81, 0.7) 0%,
              rgba(89, 83, 27, 0.96) 100%
            );

            .container {
              background: linear-gradient(
                  180deg,
                  rgba(25, 26, 12, 0.96) 0%,
                  rgba(89, 83, 27, 0.96) 100%
                ),
                url("/supercarddaily-card.png");

              .info {
                .win {
                  color: #ffee51;
                }
              }
            }

            &::after {
              background-color: #ffee51;
              box-shadow: 0 -0.3645833333vw 4.0104166667vw 0.5208333333vw rgba(255, 238, 81, 0.75);
            }
          }

          &.legend {
            background: linear-gradient(
              211.88deg,
              rgba(255, 81, 81, 0.7) 0%,
              rgba(89, 27, 49, 0.96) 100%
            );

            .container {
              background: linear-gradient(
                  180deg,
                  rgba(34, 15, 27, 0.96) 0%,
                  rgba(89, 27, 49, 0.96) 100%
                ),
                url("/supercarddaily-card.png");

              .info {
                .win {
                  color: #ff5151;
                }
              }
            }

            &::after {
              background-color: #ff5151;
              box-shadow: 0 -0.3645833333vw 4.0104166667vw 0.5208333333vw rgba(255, 81, 81, 0.75);
            }
          }
        }

        .back {
          transform: rotateY(0deg);

          img {
            display: block;
            max-width: 100%;
          }

          &::after {
            content: "";
            height: 0.1041666667vw;
            width: 6.4583333333vw;
            background-color: #ffffff;
            position: absolute;
            left: 50%;
            bottom: 0;
            transform: translateX(-50%);
            box-shadow: 0 -0.3645833333vw 4.0104166667vw 0.5208333333vw rgba(255, 255, 255, 0.75);
          }
        }
      }
    }
  }
  .controls {
    display: flex;
    justify-content: center;
  }
}
</style>