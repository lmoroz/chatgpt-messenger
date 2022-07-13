<template>
  <div class="settings">
    <div class="settings__logo"></div>
    <div class="settings__title">ChatGPT</div>
    <form action="#">
      <div class="settings__field">
        <span class="fa fa-key"></span>
        <input type="text" required placeholder="" :value="openapi.OPENAI_API_KEY" @input="sendSettings('OPENAI_API_KEY', $event)">
        <label>OPENAI_API_KEY</label>
      </div>
      <div class="settings__field">
        <span class="fa fa-user"></span>
        <input type="text" required placeholder="" :value="openapi.engine" @input="sendSettings('engine', $event)">
        <label>Engine</label>
      </div>
      <div class="settings__field">
        <span class="fa fa-magic"></span>
        <input type="number" required min="0" max="1" step="0.1" placeholder="" :value="openapi.temperature" @input="sendSettings('temperature', $event)">
        <label>Creativity</label>
      </div>
      <div class="settings__field">
        <span class="fa fa-check"></span>
        <input type="number" required min="0" max="1" step="0.1" placeholder="" :value="openapi.top_p" @input="sendSettings('top_p', $event)">
        <label>Predictability</label>
      </div>
      <transition name="fade">
        <div v-show="savingInProgress" class="settings__save">
          <svg width="48" height="48" viewBox="0 0 50 50">
            <circle cx="25" cy="25" r="20" fill="none" stroke="#ffffff77" stroke-width="5" stroke-dasharray="125.66" stroke-dashoffset="125.66">
              <animate attributeName="stroke-dashoffset" values="125.66;0" dur="1s" repeatCount="indefinite"></animate>
            </circle>
          </svg>
        </div>
      </transition>
      <transition v-show="settingsSaved" name="fade">
        <div class="settings__saved">
          <span class="fa fa-check"></span>Saved!
        </div>
      </transition>
    </form>
  </div>
</template>

<script>
import debounce from 'https://cdn.skypack.dev/lodash.debounce@4.0.8';

export default {
  name: 'settings',
  props: {
    openapi: {
      type: Object,
      default: () => {},
    },
    settingsSaved: {
      type: Boolean,
      default: false,
    },
  },
  watch: {
    settingsSaved(newValue) {
      if (newValue) this.savingInProgress = false;
    },
  },
  data() {
    return {
      savingInProgress: false,
    };
  },
  mounted() {

  },
  methods: {
    sendSettings(prop, value) {
      console.log('saveSettings', );
      this.savingInProgress = true;
      this.saveSettings({[prop]: value});
    },
    saveSettings: debounce((openapi) => {
      this.$emit(`update:modelValue`, Object.assign({}, this.openapi, openapi));
    }, 3000),

  },
};
</script>

<style lang="stylus" scoped>
:root
  --header-footer-color: linear-gradient(to bottom right, #4d566c, #2c3e50, #2c3e50, #1e2e3c)
  --shadows: -3px -3px 7px #ffffff73, 2px 2px 5px rgba(94, 104, 121, 0.288)

.slide-out-enter-active, .slide-out-leave-active
  transition: all .2s ease;

.slide-out-enter-from, .slide-out-leave-to
  opacity: 0

.settings
  max-width 300px
  background var(--header-footer-color)
  border-radius 20px
  padding 40px 30px
  box-shadow var(--shadows)

  &__logo
    position absolute
    display block
    left 50%
    width 120px
    height 120px
    border-radius 50%
    background linear-gradient(to bottom, transparent 50%, #4d566c 50%, #2c3e50 65%, #2c3e50 80%, #1e2e3c 100%)
    transform translateY(calc(-50% - 40px)) translateX(-50%)
    box-shadow var(--shadows)
    &:before
      display block
      content ''
      position absolute
      top 0
      left 0
      bottom 0
      right 0
      background linear-gradient(to bottom, transparent 50%, #ffffff44 50%)
      width 120px
      height 120px
      border-radius 50%
      background-size cover
      transform scale(0.95)

    &:after
      display block
      content ''
      position absolute
      top 0
      left 0
      bottom 0
      right 0
      background #ffffffdd url("https://seeklogo.com/images/C/chatgpt-logo-02AFA704B5-seeklogo.com.png")
      width 120px
      height 120px
      border-radius 50%
      background-size cover
      transform scale(0.8)
      box-shadow 0 0 0 7px #ffffffdd

  &__title
    font-size 42px
    font-weight 900
    margin 12px auto 48px
    color #ffffffdd
    text-shadow 0 2px 1px #333, -2px -1px #000000

  form
    display flex
    flex-direction column
    row-gap 36px

  &__field
    height 50px
    width 100%
    display flex
    position relative

    input
      height 100%
      width 100%
      padding-left 45px
      padding-right 12px
      font-size 18px
      outline none
      border none
      color #595959
      background #dde1e7
      border-radius 25px
      box-shadow inset 2px 2px 5px #00000055, inset -5px -5px 10px #00000055
      box-sizing border-box
      transition all 0.2s ease-in-out
      appearance none
      -webkit-appearance None

    .fa
      position absolute
      width 50px
      line-height 50px
      color #595959

    label
      position absolute
      top 50%
      left 45px
      pointer-events none
      color #666666
      transform translateY(-50%)
      transition all 0.3s ease

  &__field input:focus ~ label,
  &__field input:valid ~ label
    transform translateY(calc(-300% + 14px))
    font-size 14px
    color #ffffff66
    text-shadow 0 2px 3px #333, -2px -1px #00000099
    text-transform uppercase

  &__field input:focus ~ label:after,
  &__field input:valid ~ label:after
    content ':'

  &__saved
    color #ffffff99
    height 48px
    display flex
    align-items center
    justify-content center

    .fa
      margin-right 12px
</style>
