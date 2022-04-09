<template>
  <div class="poll-wrap">
    <p class="poll-name" :class="textClass">{{ pollName }}</p>
    <div class="bar-wrap">
      <div
        class="poll-bar poll-bar__green"
        :style="{ width: `${greenWidth}%` }"
        @mouseenter="hover"
        @mouseleave="unhover"
      >
        <ToolTip :count="noRisk" msg="Low Risk" />
      </div>
      <div
        class="poll-bar poll-bar__yellow"
        :style="{ width: `${yellowWidth}%` }"
        @mouseenter="hover"
        @mouseleave="unhover"
      >
        <ToolTip :count="mediumRisk" msg="Medium Risk" />
      </div>
      <div
        class="poll-bar poll-bar__red"
        :style="{ width: `${redWidth}%` }"
        @mouseenter="hover"
        @mouseleave="unhover"
      >
        <ToolTip :count="highRisk" msg="High Risk" />
      </div>
      <div
        class="poll-bar poll-bar__gray"
        :style="{ width: `${grayWidth}%` }"
        @mouseenter="hover"
        @mouseleave="unhover"
      >
        <ToolTip :count="notInterviewed" msg="Not Rated" />
      </div>
    </div>
  </div>
</template>

<script>
import ToolTip from "./ToolTip.vue";

export default {
  name: "HelloWorld",
  components: {
    ToolTip,
  },
  props: {
    pollName: {
      type: String,
      required: true,
    },
    noRisk: {
      type: Number,
      required: true,
    },
    mediumRisk: {
      type: Number,
      required: true,
    },
    highRisk: {
      type: Number,
      required: true,
    },
    notInterviewed: {
      type: Number,
      required: true,
    },
  },

  data() {
    return {
      hovered: false,
    };
  },

  methods: {
    hover: function (event) {
      this.hovered = true;
      event.target.classList.toggle("active");
      this.$emit("hover");
    },

    unhover: function (event) {
      this.hovered = false;
      event.target.classList.toggle("active");
      this.$emit("unhover");
    },
  },

  computed: {
    textClass() {
      return { active: this.hovered };
    },

    allCount: function () {
      return (
        this.noRisk + this.mediumRisk + this.highRisk + this.notInterviewed
      );
    },

    greenWidth: function () {
      return (this.noRisk * 100) / this.allCount;
    },

    yellowWidth: function () {
      return (this.mediumRisk * 100) / this.allCount;
    },

    redWidth: function () {
      return (this.highRisk * 100) / this.allCount;
    },

    grayWidth: function () {
      return (this.notInterviewed * 100) / this.allCount;
    },
  },
};
</script>

<style lang="scss">
.poll-wrap {
  width: 45%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 50px;

  &:nth-last-child(-n + 2) {
    margin-bottom: 0;
  }

  .poll-name {
    font-family: LabGrotesque-Reg, sans-serif;
    font-size: 16px;
    line-height: 24px;
    color: #1a1a1a;
  }

  .bar-wrap {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 6px;
    width: 80%;

    .poll-bar {
      border-left: 0.5px solid #fff;
      border-right: 0.5px solid #fff;
      height: 100%;
      position: relative;
      cursor: pointer;
      display: flex;
      align-items: center;
      transition: 300ms ease-in-out;

      &__green {
        background: #45e596;

        & h5 {
          color: #45e596;
        }
      }
      &__yellow {
        background: #ffc44c;

        & h5 {
          color: #ffc44c;
        }
      }
      &__red {
        background: #ff4c4c;

        & h5 {
          color: #ff4c4c;
        }
      }
      &__gray {
        background: #f2f2f2;

        & .tooltip {
          right: 0;
        }

        & h5 {
          color: #999999;
        }
      }

      &:first-of-type {
        border-left: none;
        border-radius: 6px 0 0 6px;
      }

      &:last-of-type {
        border-right: none;
        border-radius: 0 6px 6px 0;
      }

      &:hover {
        .tooltip {
          opacity: 1;
          z-index: 1;
        }
      }
    }
  }
}
</style>
