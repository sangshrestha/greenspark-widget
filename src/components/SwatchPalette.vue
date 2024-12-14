<template>
  <div class="palette">
    <label v-for="colour in ['blue', 'green', 'beige', 'white', 'black']">
      <input
        class="palette__input"
        @change="$emit('swatch', colour)"
        type="radio"
        :name="name"
        :value="colour"
        :checked="selectedColour === colour"
      />
      <span class="palette__swatch"></span>
    </label>
  </div>
</template>

<script setup lang="ts">
defineProps({
  name: { type: String, required: true },
  selectedColour: { type: String, required: true },
});
</script>

<style lang="scss" scoped>
.palette {
  display: flex;
  gap: 4px;

  &__input {
    display: none;

    &:checked {
      & + .palette__swatch {
        border: 2px solid #b0b0b0;
      }
    }
  }

  @each $colour, $hex in $colours {
    &__input[value="#{$colour}"] {
      & + .palette__swatch {
        background-color: #{$hex};

        &:hover {
          opacity: 0.8;
        }
      }
    }
  }

  &__swatch {
    @include square(16px);

    display: block;

    border: 1px solid #d4d4d4;
  }
}
</style>
