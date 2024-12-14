<template>
  <div class="widget" :class="[currentColour, contrast]">
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
      <p class="widget__option-text">
        Link to Public Profile
        <InfoInline />
      </p>
      <Checkbox :checked="linked" />
    </div>
    <div class="widget__option">
      <p class="widget__option-text">Badge colour</p>
      <SwatchPalette
        @swatch="updateColour"
        :name="`colour-group-${id}`"
        :selected-colour="selectedColor"
      />
    </div>
    <div class="widget__option">
      <p class="widget__option-text">Activate badge</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";
import Checkbox from "./Checkbox.vue";
import GreensparkLogo from "./GreensparkLogo.vue";
import InfoInline from "./InfoInline.vue";
import SwatchPalette from "./SwatchPalette.vue";

const props = defineProps({
  id: { type: Number, required: true },
  action: { type: String, required: true },
  amount: { type: Number, required: true },
  type: { type: String, required: true },
  linked: { type: Boolean, required: true },
  selectedColor: { type: String, required: true },
});

const currentColour = ref(props.selectedColor);

const lightColors = ["white", "beige"];

const contrast = computed(() =>
  lightColors.includes(currentColour.value) ? "light" : "dark"
);

function updateColour(colour: string) {
  currentColour.value = colour;
}
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

  &__option {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  &__option-text {
    color: $colour-green;
    font-size: 14px;
  }

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
}
</style>
