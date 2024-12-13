<template>
  <div class="widget" :class="[selectedColor, contrast]">
    <div class="widget__header">
      <div class="widget__logo">
        <GreensparkLogo :dark="contrast === 'light'" />
      </div>
      <div class="widget__heading">
        <p class="widget__heading-top">This product {{ action }}</p>
        <p class="widget__heading-bottom">{{ amount }} {{ type }}</p>
      </div>
    </div>
    <div class="widget__option">
      <label class="widget__option-text">Link to Public Profile </label>
      <a href="#" class="public-profile-link">
        <InfoIcon />
      </a>
      <label class="checkbox">
        <input type="checkbox" :checked="linked" />
        <div class="checkbox__style">
          <TickIcon /></div
      ></label>
    </div>
    <div class="widget__option">
      <p class="widget__option-text">Badge colour</p>
    </div>
    <div class="widget__option">
      <p class="widget__option-text">Activate badge</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import GreensparkLogo from "./GreensparkLogo.vue";
import InfoIcon from "./InfoIcon.vue";
import TickIcon from "./TickIcon.vue";

const props = defineProps({
  action: { type: String, required: true },
  amount: { type: Number, required: true },
  type: { type: String, required: true },
  linked: { type: Boolean, required: true },
  selectedColor: { type: String, required: true },
});

const lightColors = ["white", "beige"];

const contrast = lightColors.includes(props.selectedColor) ? "light" : "dark";
</script>

<style lang="scss" scoped>
$colour-green: #3b755f;
$colour-black: #212121;

.widget {
  display: flex;
  flex-direction: column;
  gap: 10px;
  width: 222px;

  &__icon {
    width: fit-content;
    height: fit-content;
  }

  &__header {
    display: flex;
    align-items: center;
    height: 66px;
    gap: 14px;
    padding: 8px;

    border-radius: 6px;
  }

  &__heading {
    display: flex;
    flex-direction: column;
    gap: 4px;

    color: #fff;
    font-size: 12.41px;

    &-bottom {
      font-size: 17.86px;
      font-weight: 700;
    }
  }

  &__option {
    display: flex;
    align-items: center;
  }

  &__option-text {
    color: #3b755f;
    font-size: 14px;
  }

  $colours: (
    "blue": #2e3a8c,
    "white": #fff,
    "black": $colour-black,
    "beige": #f2ebdb,
    "green": $colour-green,
  );

  &.light {
    .widget__heading {
      color: $colour-green;
    }
  }

  @each $colour, $hex in $colours {
    &.#{$colour} {
      .widget__header {
        background-color: #{$hex};
      }
    }
  }

  .checkbox {
    position: relative;
    width: 18px;
    height: 18px;

    margin-left: auto;

    &__style {
      width: 100%;
      height: 100%;
      border-radius: 3px;
      border: 2px solid $colour-black;
    }

    svg {
      display: none;
      position: absolute;
      inset: 0;

      width: 100%;
      height: 100%;
    }

    input {
      position: absolute;
      height: 0;
      width: 0;

      &:checked {
        accent-color: red;

        & + .checkbox__style {
          border: none;
          background-color: $colour-green;

          svg {
            display: block;
          }

          &::after {
            display: none;
          }
        }
      }
    }

    &:hover {
      .checkbox__style::after {
        content: "";
        position: absolute;
        top: 50%;
        left: 50%;

        height: 36px;
        width: 36px;

        border-radius: 50%;
        background-color: rgba(#afc6bd, 0.5);
        transform: translate(-50%, -50%);
      }
    }
  }
}

.public-profile-link {
  height: 11px;
  margin-left: 3px;
  align-self: flex-start;

  svg {
    display: block;
  }
}
</style>
