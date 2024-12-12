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
      <p class="widget__option-text">Link to Public Profile</p>
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

const props = defineProps({
  action: { type: String, required: true },
  amount: { type: Number, required: true },
  type: { type: String, required: true },
  selectedColor: { type: String, required: true },
});

const lightColors = ["white", "beige"];

const contrast = lightColors.includes(props.selectedColor) ? "light" : "dark";
</script>

<style lang="scss" scoped>
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

  &__option-text {
    color: #3b755f;
    font-size: 14px;
  }

  $colours: (
    "blue": #2e3a8c,
    "white": #fff,
    "black": #212121,
    "beige": #f2ebdb,
    "green": #3b755f,
  );

  &.light {
    .widget__heading {
      color: #3b755f;
    }
  }

  @each $colour, $hex in $colours {
    &.#{$colour} {
      .widget__header {
        background-color: #{$hex};
      }
    }
  }
}
</style>
