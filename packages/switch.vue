<template>
  <div class="xq-switch" :class="{'is-checked':value}" @click="handleClick">
    <input type="checkbox" class="xq-switch_input" :name="name" ref="input">
    <span class="xq-switch_core" ref="core">
      <span class="xq-switch_button"></span>
    </span>
  </div>
</template>
<script>
export default {
  name: 'XqSwitch',
  props: {
    value: {
      type: Boolean,
      default: false
    },
    activeColor: {
      type: String,
      default: ''
    },
    inactiveColor: {
      type: String,
      default: ''
    },
    name: {
      type: String,
      default: ''
    }
  },
  methods: {
    async handleClick() {
      this.$emit('input', !this.value)
      this.$refs.input.checked = !this.value
    }
  },
  mounted() {
    // 修改开关颜色
    if (this.value || this.inactiveColor) {
      const color = this.value ? this.activeColor : this.inactiveColor
      this.$refs.core.style.borderColor = color
      this.$refs.core.style.backgroundColor = color
    }
    this.$refs.input.checked = this.value
  },
  watch: {
    value(e) {
      if (this.activeColor || this.inactiveColor) {
        const color = e ? this.activeColor : this.inactiveColor
        this.$refs.core.style.borderColor = color
        this.$refs.core.style.backgroundColor = color
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.xq-switch {
  display: inline-block;
  align-items: center;
  position: relative;
  font-size: 14px;
  line-height: 20px;
  vertical-align: middle;
  .xq-switch_input {
    position: absolute;
    width: 0;
    height: 0;
    opacity: 0;
    margin: 0;
  }
  .xq-switch_core {
    margin: 0;
    display: inline-block;
    position: relative;
    width: 40px;
    height: 20px;
    border: 1px solid #dcdfe6;
    outline: nxq;
    border-radius: 10px;
    box-sizing: border-box;
    background: #dcdfe6;
    cursor: pointer;
    transition: border-color 0.3s, background-color 0.3s;
    vertical-align: middle;
    .xq-switch_button {
      position: absolute;
      top: 1px;
      left: 1px;
      border-radius: 100%;
      transition: all 0.3s;
      width: 16px;
      height: 16px;
      background-color: #fff;
    }
  }
}
.is-checked {
  .xq-switch_core {
    border-color: #409eff;
    background-color: #409eff;
    .xq-switch_button {
      transform: translateX(20px);
    }
  }
}
</style>
