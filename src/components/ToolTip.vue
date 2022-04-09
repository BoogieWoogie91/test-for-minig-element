<template>
  <div class="tooltip">
    <h5 class="">{{ msg }}</h5>
    <p>{{ count }} empolyees</p>
  </div>
</template>

<script>
export default {
  name: "ToolTip",
  props: {
    msg: {
      type: String,
      required: true,
    },

    count: {
      type: Number,
      required: true,
    },
  },
};
</script>
<style lang="scss">
.tooltip {
  position: absolute;
  z-index: -1;
  opacity: 0;
  transition: 300ms ease-in-out;
  width: 100px;
  padding: 5px;

  h5 {
    font-family: LabGrotesque-Bold, sans-serif;
    font-size: 14px;
    line-height: 22px;
  }

  p {
    font-family: LabGrotesque-Reg, sans-serif;
    font-size: 14px;
    line-height: 22px;
  }
}
</style>