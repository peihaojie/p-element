<!--
 * @Author: HaoJie
 * @Date: 2023-01-28 16:02:25
 * @LastEditTime: 2023-01-29 16:19:54
 * @LastEditors: HaoJie
 * @FilePath: \p-element\src\components\pSelect.vue
-->
<template>
  <div ref="selectWrap" class="select--wrap">
    <div
      ref="selectTitle"
      class="select--title"
      :class="{ checked }"
      @click="!disabled && handleClick()"
      @mouseover="clearable && changeClearable(true)"
      @mouseout="clearable && changeClearable(false)"
    >
      <input
        ref="input"
        type="text"
        readonly
        :placeholder="placeholder"
        class="select--input"
        :disabled="disabled"
      />
      <div
        v-if="showClearableBool"
        class="btn iconfont icon-shanchu"
        @click.stop="clear"
      ></div>
      <div v-else class="btn iconfont icon-xiala"></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    optionList: {
      type: Array,
      default: () => [],
    },
    placeholder: {
      type: String,
      default: "请选择",
    },
    emptyText: {
      type: String,
      default: "暂无数据",
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    value: {
      default: "",
    },
  },
  data() {
    return {
      checked: false,
      clearable: true,
      showClearableBool: false,
    };
  },
  mounted() {
    window.addEventListener("click", this.isHandleClickIn, false);
    this.initValue();
  },
  methods: {
    isHandleClickIn(e) {
      const event = e || window.event;
      const target = event.target || event.srcElement;
      if (this.$refs.selectWrap.contains(target)) {
        target.tagName === "LI" && this.handleSelect(target);
        return;
      } else {
        this.checked && this.handleClick();
      }
    },
    initValue() {
      if (this.value) {
        try {
          const temp = this.optionList.find((a) => a.value === this.value);
          this.$refs.input.value = temp.label;
        } catch (e) {
          console.log("该 value 在 optionList 中不存在");
        }
      }
    },
    handleClick() {
      this.checked = !this.checked;
      this.$refs.selectTitle.classList.toggle("select--focus");
      if (this.checked) {
        this.initOption();
      } else {
        this.hiddenOption();
      }
    },
    handleSelect(target) {
      const label = target.innerText;
      const val = this.optionList.find((a) => a.label === label).value;
      this.emit(val);
      this.$refs.input.value = label;
      this.handleClick();
    },
    initOption() {
      const wrap = document.createElement("div");
      wrap.classList.add("select--body");
      if (this.optionList && this.optionList.length) {
        const ul = document.createElement("ul");
        this.optionList.forEach((i) => {
          const item = document.createElement("li");
          item.innerText = i.label;
          ul.appendChild(item);
        });
        wrap.appendChild(ul);
      } else {
        const empty = document.createElement("div");
        empty.innerText = this.emptyText;
        empty.classList.add("select--empty");
        wrap.appendChild(empty);
      }
      this.$refs.selectWrap.appendChild(wrap);
    },
    hiddenOption() {
      const wrap =
        this.$refs.selectWrap.getElementsByClassName("select--body")[0];
      this.$refs.selectWrap.removeChild(wrap);
    },
    emit(data) {
      this.$emit("input", data);
    },
    changeClearable(bool) {
      if (bool && this.$refs.input.value) {
        this.showClearableBool = true;
      } else {
        this.showClearableBool = false;
      }
    },
    clear() {
      this.$refs.input.value = "";
      this.emit(null);
      this.emit("clear", true);
    },
  },
  beforeDestroy() {
    window.removeEventListener(this.isHandleClickIn);
  },
};
</script>

<style lang="stylus" scoped>
bc = #9e9e9e
option-BC = #fff
.select--wrap
  position relative
  cursor pointer
  font-size 14px
  background option-BC
  .select--title
    display flex
    outline 1px solid bc
    border none
    border-radius 5px
    transition 0.3s outline
    &:hover, &:focus
      outline 1px solid #2196f3
    .select--input
      cursor pointer
      flex 1
      outline none
      border none
      padding 10px 10px
    .btn
      width 40px
      display flex
      justify-content center
      align-items center
      color @bc
      transition 0.3s all
  .checked
    outline 1px solid #2196f3
    .btn
      transform rotate(180deg)
</style>

<style>
:root {
  --option-BC: #fff;
  --option-hover: #f5f7fa;
}

.select--body {
  cursor: pointer;
  position: absolute;
  top: 45px;
  left: 0;
  width: 100%;
  background: var(--option-BC);
  border-radius: 3px;
  padding: 10px 0;
  box-shadow: 0 2px 12px 0 rgb(0 0 0 / 10%);
}

.select--body:after {
  content: "";
  position: absolute;
  top: -12px;
  left: 10px;
  border: 6px;
  border-style: solid;
  border-color: transparent;
  border-bottom-color: #fff;
}

.select--body ul {
  list-style: none;
  margin: 0;
  padding: 0;
  overflow: auto;
  max-height: 274px;
}

.select--body ul li {
  padding: 5px 10px;
  text-align: left;
}

.select--body ul li:hover {
  background: var(--option-hover);
}

.select--body .select--empty {
  text-align: center;
  color: #9e9e9e;
  font-size: 12px;
}
</style>
