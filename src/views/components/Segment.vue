<template>
  <div 
    class="segment-container"
    :style="{
      width: computedWidth,
      height: computedHeight,
      backgroundColor: bgColor,
      flexDirection: flexDirection,
      gap: gap,
      borderRadius: borderRadius,
      ...computedPadding,
    }"
  >
    <button
      v-for="(item, index) in data"
      :key="index"
      @click="handleOnClick(index)"
      :class="[animate ? 'has-effect' : '', activeIndex ? 'active' : '']"
      :style="activeIndex === index
      ? {
        fontWeight: activeBtnFontWeight,
        fontColor: activeBtnFontColor,
        backgroundColor: activeBtnBgColor,
      }
      : {
        fontFamily: fontFamily,
        fontWeight: fontWeight,
        fontSize: fontSize,
        fontColor: fontColor,
        backgroundColor: btnBgColor,
        borderRadius: btnBorderRadius,
      }"
    >
    {{ typeof item === 'object' ? item.value : item }}
    </button>
  </div>
</template>
<script>
export default {
  name: 'Segment',
  components: {},
  computed: {
    computedWidth() {
      return typeof this.width === 'number' ? `${this.width}px` : this.width;
    },
    computedHeight() {
      return typeof this.height === 'number' ? `${this.height}px` : this.height;
    },
    computedPadding() {
      const top = typeof this.paddingTop === 'number' ? `${this.paddingTop}px` : this.paddingTop;
      const bottom = typeof this.paddingBottom === 'number' ? `${this.paddingBottom}px` : this.paddingBottom;
      const left = typeof this.paddingLeft === 'number' ? `${this.paddingLeft}px` : this.paddingLeft;
      const right = typeof this.paddingRight === 'number' ? `${this.paddingRight}px` : this.paddingRight;

      const obj = {};
      if(top) obj.paddingTop = top;
      if(bottom) obj.paddingBottom = bottom;
      if(left) obj.paddingLeft = left;
      if(right) obj.paddingRight = right;
      return obj;
    },
    computedGap() {
      return typeof this.gap === 'number' ? `${this.gap}px` : this.gap;
    },
    computedAnimationEffect() {
      return this.animate ? `transition: ease-in-out 0.3s;` : '';
    },
  },
  props: {
    data: {
      type: Array,
      required: true,
    },
    width: {
      type: [String, Number],
      default: '100%',
    },
    height: {
      type: [String, Number],
      default: 40,
    },
    bgColor: {
      type: String,
      default: 'white',
    },
    paddingTop: {
      type: [String, Number],
      default: 8,
    },
    paddingBottom: {
      type: [String, Number],
      default: 8,
    },
    paddingLeft: {
      type: [String, Number],
      default: 8,
    },
    paddingRight: {
      type: [String, Number],
      default: 8,
    },
    fontFamily: {
      type: String,
    },
    fontWeight: {
      type: Number,
    },
    fontColor: {
      type: String,
    },
    fontSize: {
      type: Number,
    },
    flexDirection: {
      type: String,
      default: 'row',
    },
    gap: {
      type: [String, Number],
      default: '4px',
    },
    borderRadius: {
      type: Number,
    },
    btnBgColor: {
      type: String,
      default: '#F1F2F3',
    },
    btnBorderRadius: {
      type: Number,
    },
    activeBtnFontWeight: {
      type: Number,
      default: 700,
    },
    activeBtnBgColor: {
      type: String,
      default: '#ACB2B9',
    },
    activeBtnFontColor: {
      type: String,
    },
    hoverCursor: {
      type: String,
      default: 'pointer',
    },
    animate: {
      type: Boolean,
      default: true,
    },

  },
  data() {
    return {
      activeIndex: null,
    };
  },
  async mounted() {
    this.setBtnBgColor();
    this.setCursor();
  },
  beforeDestroy() {
  },
  methods: {
    handleOnClick(index) {
      this.activeIndex = index;
      this.$emit('segment-click', index);
    },
    setBtnBgColor() {
      if(!this.activeBtnBgColor) return;
      document.documentElement.style.setProperty('--active-btn-bg-color', this.activeBtnBgColor);
    },
    setCursor() {
      if(!this.hoverCursor) return;
      document.documentElement.style.setProperty('--hover-cursor', this.hoverCursor);
    },
  },
};
</script>
<style lang="scss" scoped>
$Gray-5: #D1D6DB;
$Gray-10: #F1F2F3;
$Gray-20: #e8ebed;
$Gray-50: #ACB2B9;
$Gray-60: #8D939A;
$Gray-70: #6e747c;
$Gray-80: #4B5158;
$Gray-90: #2F3337;
$Gray-100 : #17191C;
$Yellow: #ffe414;
$SkyBlue : #E1F0FF;
$Blue : #278AEC;
$Red: #F55247;
$Orange: #FFA50A;
$Green: #22BF22;

* {
  box-sizing: border-box;
}

.segment-container {
  width: 100%;
  display: flex;
  gap: 4px;
  border-radius: 8px;
  padding: 4px;
  height: 40px;
  button {
    height: 100%;
    border-radius: 8px;
    flex: 1;
    cursor: var(--hover-cursor);
  }

  .has-effect {
    transition: ease-in-out 0.3s;
    &:hover {
      transition: ease-in-out 0.3s;
      background-color: rgba(0,0,0,0.05) !important;
    }
  
    &:active{
      transition: ease-in-out 0.3s;
      background-color: rgba(0,0,0,0.1) !important;
    }
  }

  .has-effect:hover,
  .has-effect:active {
    background-color: var(--active-btn-bg-color) !important;
  }
}
</style>

