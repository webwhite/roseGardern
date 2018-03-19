<template>
    <div class="star">
        <span></span>
    </div>
</template>

<script type="text/ecmascript-6">
const LENGTH = 5;
const CLS_ON = "on";
const CLS_OFF = "off";
const ClS_HALF = "half";
export default {
  props: {
    size: {
      type: Number
    },
    score: {
      type: Number
    }
  },
  computed: {
    starType() {
      return "star-" + this.size;
    },
    itemClasses() {
      let result = [];
      let hasDecimal = score % 1 !== 0;
      let integer = Math.floor(this.score);
      for (var i = 0; i < integer.length; i++) {
        result.push(CLS_ON);
      }
      if (hasDecimal) {
        result.push(ClS_HALF);
      }
      while (result.length < LENGTH) {
        result.push(CLS_OFF);
      }
      return result;
    }
  }
};
</script>