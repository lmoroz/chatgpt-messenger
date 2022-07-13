<template>
  <vue-final-modal v-slot="{ close, params }" v-bind="$attrs" classes="modal-container" content-class="modal-content" overlay-class="d-overlay" :esc-to-close="true">
    <form @submit.prevent="$emit('confirm', theme); close()" class="form">
      <input type="text" placeholder="Dialogue theme" v-model="theme">
      <button :disabled="!this.theme"><span class="fa fa-plus"></span></button>
    </form>
    <button class="close-button" @click="close">&#x2715;</button>
  </vue-final-modal>
</template>

<script>
export default {
  name: 'NewDialogueModal',
  inheritAttrs: false,
  emits: ['confirm'],
  data() {
    return {
      theme: ''
    }
  }
};
</script>

<style lang="stylus">
.modal-container
  display flex
  align-items center
  justify-content center

.modal-content
  width 100%
  max-width 640px
  background var(--header-footer-color)
  padding 12px
  position relative
  border-radius 12px
  transform-style: preserve-3d
  transition: transform 0.3s ease-in-out
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.3), 0 0 5px rgba(#fff, 0.5)

.close-button
  position absolute
  top 10px
  right 10px
  background: none
  border: none
  cursor: pointer
  font-size 24px
  width 34px
  height 34px
  display flex
  place-content center
  place-items center
  color rgba(#fff, 0.5)
  transition transform 300ms ease
  padding 5px
  border-radius 5px

  &:active
    transform scale(1.3)

  &:hover
    box-shadow inset 0 0 5px rgba(#000, 0.8)


.form
  display flex
  flex-direction column
  row-gap 12px
  justify-content space-between
  align-items center
  column-gap 12px
  padding-top 36px

  input, button
    font-size 20px
    border-radius: 20px

  input
    background-color: var(--message-input-color)
    color: var(--side-menu-color)
    padding 5px 12px
    width 100%

    &::placeholder
      color: rgba(#000, 0.3)

    &:focus::placeholder
      color: transparent

  button
    background: var(--sent-message-color)
    color: var(---sent-message-text)
    padding 5px 12px
    border none

    &[disabled]
      opacity 0.5

    &:not([disabled])
      cursor pointer

    &:not([disabled]):hover, &:not([disabled]):active
      background-color: darken(#f1c40f, 10%)

</style>
