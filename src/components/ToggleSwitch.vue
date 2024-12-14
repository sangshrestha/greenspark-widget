<template>
  <label class="switch">
    <input class="switch__input" type="radio" :name="name" :checked="checked" />
    <div class="switch__box"><span class="switch__slider"></span></div>
  </label>
</template>

<script setup lang="ts">
defineProps({
  name: { type: String, required: true },
  checked: { type: Boolean, default: false },
});
</script>

<style lang="scss" scoped>
$width: 45px;
$height: 20px;

.switch {
  width: 45px;
  height: $height;

  &__input {
    display: none;

    &:checked + .switch__box {
      background-color: $colour-green;

      .switch__slider {
        border-color: $colour-green;
        transform: translateX($width - $height);
      }
    }
  }

  &__box {
    @include square(100%);
    position: relative;

    background-color: #fff;
    border: 1px solid $colour-green-light;
    border-radius: calc($height / 2);
  }

  &__slider {
    @include circle($height);

    content: "";

    position: absolute;
    z-index: 1;
    top: -1px;

    background-color: $colour-white;
    box-shadow: 0 0 2px 0 #000;
    border: 1px solid #f2ebdb;
    transition: $transition;

    &::before {
      @include circle(0);

      content: "";

      position: absolute;
      z-index: -1;
      top: 50%;
      left: 50%;

      background-color: $colour-green-light;
      opacity: 0.5;
      transition: $transition;
      transform: translate(-50%, -50%);
    }

    &:hover {
      &::before {
        @include circle(38px);

        transition-delay: 0.2s;
        pointer-events: none;
      }
    }
  }
}
</style>
