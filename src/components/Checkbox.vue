<template>
  <label class="checkbox">
    <input class="checkbox__input" type="checkbox" :checked="checked" />
    <div class="checkbox__visual">
      <TickIcon />
    </div>
  </label>
</template>

<script setup lang="ts">
import TickIcon from "./icon/TickIcon.vue";

defineProps({
  checked: { type: Boolean, default: false },
});
</script>

<style lang="scss" scoped>
.checkbox {
  @include square(18px);

  position: relative;

  &:hover {
    .checkbox__visual {
      &::after {
        @include square(200%);

        opacity: 1;
        transition-delay: 0.2s;
      }
    }
  }

  &__visual {
    @include square(100%);

    border: 2px solid $colour-black;
    border-radius: 3px;

    svg {
      display: none;
    }

    // Hover effect
    &::after {
      @include square(0);

      content: "";

      position: absolute;
      top: 50%;
      left: 50%;

      opacity: 0;
      border-radius: 50%;
      background-color: rgba($colour-green-light, 0.5);
      transform: translate(-50%, -50%);
      transition: $transition;
    }
  }

  &__input {
    display: none;

    &:checked {
      & + .checkbox__visual {
        border: none;
        background-color: $colour-green;

        svg {
          display: block;
        }

        &::after {
          @include square(0);

          opacity: 0;
        }
      }
    }
  }
}
</style>
