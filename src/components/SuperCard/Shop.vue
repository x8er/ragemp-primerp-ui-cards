<template>
  <div class="shop">
    <div class="list">
      <div class="folder">
        <span class="title">Восхитительные карты</span>
        <span class="help">Наведитесь для взаимодействия.</span>
        <div class="card-list">
          <div
            class="card"
            :class="{
              selected:
                notWinCards.includes(index.toString()) &&
                animationFor === 'default',
            }"
            v-for="(item, index) of INCOMING_CARDS.default"
            :key="index"
          >
            <div class="content">
              <div class="front">
                <div class="container">
                  <img :src="item.image" />
                  <div class="info">
                    <span class="title">{{ item.title }}</span>
                    <span class="win">{{ item.win }}</span>
                  </div>
                </div>
              </div>
              <div class="back">
                <div class="container">
                  <img src="/supercardshop-logo.png" />
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="amazing-btn" @click="startTheGame('default')">
          <div class="content">
            <span
              >Купить карту этой редкости за
              <span class="highlight">15 пыли</span></span
            >
          </div>
        </div>
      </div>
      <div class="folder gold">
        <span class="title">Ультра карты</span>
        <span class="help">Наведитесь для взаимодействия.</span>
        <div class="card-list">
          <div
            class="card"
            :class="{
              selected:
                notWinCards.includes(index.toString()) &&
                animationFor === 'gold',
            }"
            v-for="(item, index) of INCOMING_CARDS.gold"
            :key="index"
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
                <div class="container">
                  <img src="/supercardshop-logo.png" />
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="amazing-btn" @click="startTheGame('gold')">
          <div class="content">
            <span
              >Купить карту этой редкости за
              <span class="highlight">50 пыли</span></span
            >
          </div>
        </div>
      </div>
      <div class="folder legend">
        <span class="title">Легендарные карты</span>
        <span class="help">Наведитесь для взаимодействия.</span>
        <div class="card-list">
          <div
            class="card"
            :class="{
              selected:
                notWinCards.includes(index.toString()) &&
                animationFor === 'legend',
            }"
            v-for="(item, index) of INCOMING_CARDS.legend"
            :key="index"
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
                <div class="container">
                  <img src="/supercardshop-logo.png" />
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="amazing-btn" @click="startTheGame('legend')">
          <div class="content">
            <span
              >Купить карту этой редкости за
              <span class="highlight">95 пыли</span></span
            >
          </div>
        </div>
      </div>
    </div>
    <div class="info">
      <span>
        <span class="plus">+</span>
        Тут может быть большое описание чего-нибудь связанного с карточками или
        чего-то ещё, чтобы игроку было ещё яснее.
      </span>
    </div>
    <div
      class="blackout"
      :class="{ 'show-win-card': showWinCard }"
      @click="showWinCard = false"
    >
      <div class="card" :class="[winCard.type]">
        <div class="content">
          <div class="front">
            <div class="container">
              <img :src="winCard.image" />
              <div class="info">
                <span class="title">{{ winCard.title }}</span>
                <span class="win">{{ winCard.win }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SuperCardShop",
  data() {
    return {
      INCOMING_CARDS: {
        default: [
          {
            title: "Автомобиль",
            win: "Lamborghini",
            image: "/test-car.png",
            type: "default",
            isWin: 0,
          },
          {
            title: "Деньги",
            win: "$ 100.000.000",
            image: "/test-car.png",
            type: "default",
            isWin: 0,
          },
          {
            title: "Статус",
            win: "VIP на 30 дней",
            image: "/test-car.png",
            type: "default",
            isWin: 0,
          },
          {
            title: "Деньги",
            win: "$ 100.000.000",
            image: "/test-car.png",
            type: "default",
            isWin: 0,
          },
          {
            title: "Статус",
            win: "VIP на 30 дней",
            image: "/test-car.png",
            type: "default",
            isWin: 1,
          },
          {
            title: "Деньги",
            win: "$ 100.000.000",
            image: "/test-car.png",
            type: "default",
            isWin: 0,
          },
        ],
        gold: [
          {
            title: "Автомобиль",
            win: "Lamborghini",
            image: "/test-car.png",
            type: "gold",
            isWin: 0,
          },
          {
            title: "Деньги",
            win: "$ 100.000.000",
            image: "/test-car.png",
            type: "gold",
            isWin: 0,
          },
          {
            title: "Статус",
            win: "VIP на 30 дней",
            image: "/test-car.png",
            type: "gold",
            isWin: 1,
          },
          {
            title: "Деньги",
            win: "$ 100.000.000",
            image: "/test-car.png",
            type: "gold",
            isWin: 0,
          },
          {
            title: "Статус",
            win: "VIP на 30 дней",
            image: "/test-car.png",
            type: "gold",
            isWin: 0,
          },
          {
            title: "Деньги",
            win: "$ 100.000.000",
            image: "/test-car.png",
            type: "gold",
            isWin: 0,
          },
        ],
        legend: [
          {
            title: "Автомобиль",
            win: "Lamborghini",
            image: "/test-car.png",
            type: "legend",
            isWin: 0,
          },
          {
            title: "Деньги",
            win: "$ 100.000.000",
            image: "/test-car.png",
            type: "legend",
            isWin: 0,
          },
          {
            title: "Статус",
            win: "VIP на 30 дней",
            image: "/test-car.png",
            type: "legend",
            isWin: 0,
          },
          {
            title: "Деньги",
            win: "$ 100.000.000",
            image: "/test-car.png",
            type: "legend",
            isWin: 1,
          },
          {
            title: "Статус",
            win: "VIP на 30 дней",
            image: "/test-car.png",
            type: "legend",
            isWin: 0,
          },
          {
            title: "Деньги",
            win: "$ 100.000.000",
            image: "/test-car.png",
            type: "legend",
            isWin: 0,
          },
        ],
      },
      animation: null,
      animationFor: null,
      winCard: {
        title: "",
        win: "",
        image: "",
        type: "default",
        isWin: 1,
      },
      showWinCard: false,
      notWinCards: [],
    };
  },
  methods: {
    mixedOrder(type) {
      const TEMP = [];
      let winIndex = null;
      for (const INDEX in this.INCOMING_CARDS[type]) {
        if (this.INCOMING_CARDS[type][INDEX].isWin) {
          winIndex = INDEX;
          continue;
        }
        if (Math.round(Math.random())) {
          TEMP.push(INDEX);
        } else {
          TEMP.unshift(INDEX);
        }
      }
      TEMP.unshift(winIndex);
      return TEMP;
    },
    startTheGame(type) {
      if (this.animation) return;
      const _ = this,
        temp = this.mixedOrder(type);
      let i = 0,
        delay = 1000;
      this.winCard = this.INCOMING_CARDS[type][temp[0]];
      this.animationFor = type;
      this.notWinCards = [...temp];
      this.animation = setTimeout(function tick() {
        if (i === temp.length - 1) {
          _.showWinCard = true;
          _.animationFor = null;
          _.notWinCards.pop();
          return (_.animation = clearTimeout(_.animation));
        }
        _.notWinCards.pop();
        i++;
        _.animation = setTimeout(tick, delay);
      }, 1000);
    },
  },
};
</script>

<style lang="scss" scoped>
@font-face {
  font-family: Gilroy;
  src: url("~@/assets/Gilroy-SemiBold.ttf");
}

.shop {
  box-sizing: border-box;
  padding: 2.0833333333vw 2.8125vw 0;
  font-family: Gilroy;
  font-size: 0.9375vw;
  position: relative;

  .list {
    display: flex;
    justify-content: space-between;

    .amazing-btn {
      box-sizing: border-box;
      border: 0.1041666667vw solid rgba(80, 160, 255, 0.37);
      border-radius: 0.2083333333vw;

      .content {
        display: flex;
        justify-content: center;
        border-radius: inherit;

        span {
          font-size: 0.8333333333vw;
          line-height: 1.71875vw;
          color: rgba(255, 255, 255, 0.5);

          .highlight {
            color: #2cacff;
          }
        }
      }

      &:hover {
        border: 0;
        padding: 0.1041666667vw;
        background: linear-gradient(268.02deg, #256fff 0%, #50a0ff 100%);
        box-shadow: 0px 1.1979166667vw 2.5520833333vw -0.7291666667vw #5f65ff;

        .content {
          background: linear-gradient(268.02deg, #256fff 0%, #2548ff 100%);

          span {
            color: #ffffff;
          }
        }
      }
    }

    .folder {
      box-sizing: border-box;
      padding: 2.0833333333vw 1.5104166667vw 0;
      border-radius: 0.4166666667vw;
      background-color: rgba(255, 255, 255, 0.03);
      width: 21.6666666667vw;
      height: 23.6979166667vw;
      position: relative;

      > .title {
        padding: 0 0.9375vw;
        display: inline-block;
        line-height: 2.34375vw;
        border-radius: inherit;
        background: linear-gradient(268.02deg, #2bb2ff 0%, #5e25ff 100%);
        box-shadow: 0px 1.1979166667vw 2.5520833333vw -0.7291666667vw #5f65ff;
        position: absolute;
        left: 1.5625vw;
        top: 0;
        transform: translateY(-50%);
      }

      .help {
        position: relative;

        &::before {
          display: inline-block;
          content: "i";
          width: 0.9895833333vw;
          line-height: 0.9895833333vw;
          text-align: center;
          font-weight: bold;
          border-radius: 50%;
          background-color: rgba(255, 255, 255, 0.09);
          margin-right: 0.5208333333vw;
        }
      }

      &.gold {
        > .title {
          background: linear-gradient(268.02deg, #ffaa2b 0%, #ff5925 100%);
          box-shadow: 0px 1.1979166667vw 2.5520833333vw -0.7291666667vw #ffd25f;
        }

        .amazing-btn {
          .content .highlight {
            color: #ffd25f;
          }

          &:hover .content .highlight {
            color: #ffffff;
          }
        }

        .card-list .card .content {
          .front {
            .container {
              background: linear-gradient(
                  180deg,
                  rgba(25, 26, 12, 0.96) 0%,
                  rgba(89, 83, 27, 0.96) 100%
                ),
                url("/supercarddaily-card.png");
            }

            &::after {
              box-shadow: 0 -0.3645833333vw 4.0104166667vw 0.5208333333vw rgba(255, 238, 81, 0.75);
            }
          }
          .front,
          .back {
            box-shadow: 0px 1.1979166667vw 2.5520833333vw -0.7291666667vw rgba(255, 210, 95, 0.5);
            background: linear-gradient(
              211.88deg,
              rgba(255, 238, 81, 0.7) 0%,
              rgba(255, 238, 81, 0) 100%
            );

            .container {
              .info {
                .win {
                  color: #ffee51;
                }
              }
            }

            &::after {
              background-color: #ffee51;
            }
          }
        }
      }

      &.legend {
        > .title {
          background: linear-gradient(268.02deg, #ff2b77 0%, #9f25ff 100%);
          box-shadow: 0px 1.1979166667vw 2.5520833333vw -0.7291666667vw #ff5fd2;
        }

        .amazing-btn {
          .content .highlight {
            color: #ff5151;
          }

          &:hover .content .highlight {
            color: #ffffff;
          }
        }

        .card-list .card .content {
          .front {
            .container {
              background: linear-gradient(
                  180deg,
                  rgba(34, 15, 27, 0.96) 0%,
                  rgba(89, 27, 49, 0.96) 100%
                ),
                url("/supercarddaily-card.png");
            }

            &::after {
              box-shadow: 0 -0.3645833333vw 4.0104166667vw 0.5208333333vw rgba(255, 81, 81, 0.75);
            }
          }
          .front,
          .back {
            box-shadow: 0px 1.1979166667vw 2.5520833333vw -0.7291666667vw rgba(255, 95, 210, 0.5);
            background: linear-gradient(
              211.88deg,
              rgba(255, 81, 81, 0.7) 0%,
              rgba(255, 238, 81, 0) 100%
            );

            .container {
              .info {
                .win {
                  color: #ff5151;
                }
              }
            }

            &::after {
              background-color: #ff5151;
            }
          }
        }
      }

      .card-list {
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
        margin-bottom: 0.6770833333vw;

        .card {
          perspective: 41.6666666667vw;
          margin-top: 0.78125vw;

          &.selected .content {
            .front {
              transform: rotateY(0deg);
            }

            .back {
              transform: rotateY(-180deg);
            }
          }

          &.not-win .content {
            .front {
              transform: rotateY(180deg);
            }

            .back {
              transform: rotateY(0deg);
            }
          }

          .content {
            position: relative;
            width: 5.8333333333vw;
            height: 7.8125vw;

            .front,
            .back {
              box-sizing: border-box;
              padding: 0.1041666667vw;
              width: inherit;
              height: inherit;
              border-radius: 0.4166666667vw;
              background: linear-gradient(
                211.88deg,
                rgba(57, 125, 255, 0.7) 0%,
                rgba(255, 238, 81, 0) 100%
              );
              box-shadow: 0px 1.1979166667vw 2.5520833333vw -0.7291666667vw rgba(95, 101, 255, 0.5);
              position: absolute;
              top: 0;
              left: 0;
              backface-visibility: hidden;
              transform: rotateY(180deg);
              transition: transform 1s ease;

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
                  margin-top: 0.7291666667vw;
                  margin-bottom: 0.5208333333vw;

                  span {
                    display: block;
                    font-size: 0.6770833333vw;

                    &.win {
                      font-size: 1.25vw;
                      color: #51e0ff;
                      font-size: 0.7291666667vw;
                    }
                  }
                }
              }

              &::after {
                content: "";
                height: 0.1041666667vw;
                width: 4.0104166667vw;
                background-color: #51e0ff;
                position: absolute;
                left: 50%;
                bottom: 0;
                transform: translateX(-50%);
                box-shadow: 0 -0.3645833333vw 4.0104166667vw 0.5208333333vw rgba(81, 224, 255, 0.75);
              }
            }

            .back {
              transform: rotateY(0deg);

              .container {
                justify-content: center;
                background: linear-gradient(
                    180deg,
                    #0a1422 0%,
                    rgba(9, 28, 56, 0) 100%
                  ),
                  url("/supercarddaily-card.png");

                img {
                  width: 3.0208333333vw;
                }
              }

              &::after {
                box-shadow: none;
              }
            }
          }
        }
      }
    }
  }

  > .info {
    box-sizing: border-box;
    padding: 0 1.0416666667vw;
    display: flex;
    align-items: center;
    width: 36.25vw;
    height: 4.3229166667vw;
    background-color: rgba(255, 255, 255, 0.03);
    border-radius: 0.4166666667vw;
    margin: 1.0416666667vw auto 0;
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

    span {
      color: rgba(255, 255, 255, 0.5);

      .plus {
        color: #ffee51;
        margin-right: 0.2604166667vw;
      }
    }
  }

  .blackout {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    // background: radial-gradient(
    //   circle,
    //   rgba(0, 0, 0, 1) 20%,
    //   rgba(0, 0, 0, 0) 40%
    // );
    opacity: 0;
    visibility: hidden;
    transition: opacity 0.3s linear, visibility 0s linear 0.3s;
    position: absolute;
    left: 0;
    top: 0;

    &.show-win-card {
      opacity: 1;
      visibility: visible;
      transition: opacity 0.3s linear, visibility 0s linear;

      .card {
        opacity: 1;
        transform: scale(1);
      }
    }

    .card {
      width: 12vw;
      height: 16vw;
      transform: scale(0.5);
      opacity: 0;
      transition: transform 0.2s ease, opacity 0.2s ease;

      &.gold {
        .content {
          .front {
            box-shadow: 0px 1.1979166667vw 10vw -0.7291666667vw rgba(255, 210, 95, 0.8);
            background: linear-gradient(
              211.88deg,
              rgba(255, 238, 81, 0.7) 0%,
              rgba(255, 238, 81, 0) 100%
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
              box-shadow: 0 -0.3645833333vw 4.0104166667vw 0.5208333333vw rgba(255, 238, 81, 0.75);
              background-color: #ffee51;
            }
          }
        }
      }

      &.legend {
        .content {
          .front {
            box-shadow: 0px 1.1979166667vw 10vw -0.7291666667vw rgba(255, 95, 210, 0.8);
            background: linear-gradient(
              211.88deg,
              rgba(255, 81, 81, 0.7) 0%,
              rgba(255, 238, 81, 0) 100%
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
              box-shadow: 0 -0.3645833333vw 4.0104166667vw 0.5208333333vw rgba(255, 81, 81, 0.75);
              background-color: #ff5151;
            }
          }
        }
      }

      .content {
        position: relative;
        width: 100%;
        height: 100%;

        .front {
          box-sizing: border-box;
          padding: 0.1041666667vw;
          width: inherit;
          height: inherit;
          border-radius: 0.4166666667vw;
          background: linear-gradient(
            211.88deg,
            rgba(57, 125, 255, 0.7) 0%,
            rgba(255, 238, 81, 0) 100%
          );
          box-shadow: 0px 1.1979166667vw 10vw -0.7291666667vw rgba(95, 101, 255, 1);
          position: absolute;
          top: 0;
          left: 0;
          backface-visibility: hidden;

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
              margin-top: 2vw;
              margin-bottom: 1.7vw;

              span {
                display: block;

                &.win {
                  font-size: 1.5vw;
                  color: #51e0ff;
                }
              }
            }
          }

          &::after {
            content: "";
            height: 0.1041666667vw;
            width: 7vw;
            background-color: #51e0ff;
            position: absolute;
            left: 50%;
            bottom: 0;
            transform: translateX(-50%);
            box-shadow: 0 -0.3645833333vw 4.0104166667vw 0.5208333333vw rgba(81, 224, 255, 0.75);
          }
        }
      }
    }
  }
}
</style>