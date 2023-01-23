<template>
  <li class="typing" :class="{_on: isTyping}">
    <span class="typing__bullet"></span>
    <span class="typing__bullet"></span>
    <span class="typing__bullet"></span>
  </li>
</template>

<script>
export default {
  name: 'typing',
  props: {
    isTyping: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style lang="stylus" scoped>
:root
  --typing-bullet-size 7px
  --typing-bullet-color alpha(#000, 70%)
  --typing-bullet-bg #e6e6e6dd
  --typing-speed 1s
  --typing-bullet-delay 0.2s
  --typing-bounce-animation: bounce var(--typing-speed) linear infinite both
  --typing-fade-animation: loadingFade var(--typing-speed) infinite both

.typing
  display none
  padding: 12px
  font-size: 0
  column-gap 12px
  border: 1px solid var(--typing-bullet-bg)
  border-radius: 20px 20px 20px 0

  &__bullet
    display: inline-block
    width: var(--typing-bullet-size)
    height: var(--typing-bullet-size)
    border-radius: 50%
    background-color: var(--typing-bullet-color)
    transition: all calc(var(--typing-speed) / 2) linear

  &._on
    display inline-flex

    .typing__bullet
      background-color: var(--typing-bullet-bg)
      animation: var(--typing-bounce-animation)

      &:nth-child(2)
        animation-delay: var(--typing-bullet-delay)

      &:nth-child(3)
        animation-delay: calc(var(--typing-bullet-delay) * 2)


@keyframes bounce
  0%, 80%, 100%
    opacity: 1
    transform: translateY(30%)

  50%
    opacity: 0.3
    transform: translateY(-70%)

@keyframes loadingFade
  0%
    opacity: 0
  50%
    opacity: 0.8
  100%
    opacity: 0
</style>
