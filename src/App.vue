<template>
  <div class="polls-box" :class="{ hovered: isHover }">
    <HelloWorld
      v-for="poll in polls"
      :key="poll.pollName"
      :pollName="poll.pollName"
      :noRisk="poll.noRisk"
      :mediumRisk="poll.mediumRisk"
      :highRisk="poll.highRisk"
      :notInterviewed="poll.notInterviewed"
      @hover="hover"
      @unhover="unhover"
    />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
  },

  data() {
    return {
      polls: [
        //эти данные я якобы получил в сторе с помощью асинхронного запроса, там же отпарсил в массив объектов через JSON.parse(), и притащил сюда из стэйта в computed через ...mapState([polls]), например
        {
          pollName: "Risk of Loss",
          noRisk: 20,
          mediumRisk: 47,
          highRisk: 69,
          notInterviewed: 102,
        },
        {
          pollName: "Satisfaction",
          noRisk: 5,
          mediumRisk: 7,
          highRisk: 8,
          notInterviewed: 150,
        },
        {
          pollName: "Impact of Loss",
          noRisk: 20,
          mediumRisk: 106,
          highRisk: 34,
          notInterviewed: 5,
        },
        {
          pollName: "Performance",
          noRisk: 69,
          mediumRisk: 15,
          highRisk: 87,
          notInterviewed: 9,
        },
      ],

      isHover: false,
    };
  },
  methods: {
    hover: function () {
      this.isHover = true;
    },
    unhover: function () {
      this.isHover = false;
    },
  },
};
</script>

<style lang="scss">
@font-face {
  font-family: "LabGrotesque-Reg";
  font-weight: 400;
  src: url("~@/assets/fonts/LabGrotesque-Regular.woff2") format("woff2"),
    url("~@/assets/fonts/LabGrotesque-Regular.woff") format("woff");
}

@font-face {
  font-family: "LabGrotesque-Bold";
  font-weight: 700;
  src: url("~@/assets/fonts/LabGrotesque-Bold.woff2") format("woff2"),
    url("~@/assets/fonts/LabGrotesque-Bold.woff") format("woff");
}
body {
  background: rgba(245, 245, 245, 1);
  padding: 0 15px;
  #app {
    .polls-box {
      width: 100%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: rgba(255, 255, 255, 1);
      border-radius: 30px;
      padding: 15px;
      flex-wrap: wrap;
      box-sizing: border-box;

      &.hovered {
        background: rgba(225, 225, 225, 0.08);

        .poll-wrap {
          .poll-name {
            opacity: 0.08;
            &.active {
              opacity: 1;
            }
          }
          .bar-wrap {
            .poll-bar {
              opacity: 0.08;
              &.active {
                opacity: 1;
              }

              &__gray {
                background: #999999;
              }
            }
          }
        }
      }
    }
  }
}
</style>
