<template>
  <header>
    <h1>Per product widgets</h1>
  </header>

  <main>
    <p v-if="widgetIsLoading">Loading widget...</p>
    <template v-else>
      <ProductWidget
        v-for="widget in widgets"
        :id="widget.id"
        :action="widget.action"
        :active="widget.active"
        :amount="widget.amount"
        :type="widget.type"
        :linked="widget.linked"
        :selected-color="widget.selectedColor"
      />
    </template>
  </main>
</template>

<script setup lang="ts">
import { ref, type Ref } from "vue";
import ProductWidget from "./components/ProductWidget.vue";

interface WidgetProperty {
  id: number;
  type: string;
  amount: number;
  action: string;
  active: boolean;
  linked: boolean;
  selectedColor: string;
}

const widgetIsLoading = ref(true);
const widgets: Ref<WidgetProperty[]> = ref([]);

async function fetchWidgets() {
  try {
    const response = await fetch(
      "https://b795b019-1f84-41f4-93a3-a702d686c75a.mock.pstmn.io/product-widgets"
    );
    const jsonResponse = await response.json();
    return jsonResponse;
  } catch (error) {
    console.error(error);
    // dummy data just so frontend works if fetch fails for any reason
    const defaultImport = (await import("@/dummy.ts")).default;
    return defaultImport;
  }
}

fetchWidgets().then((e) => {
  widgetIsLoading.value = false;
  widgets.value = e;
});
</script>

<style lang="scss" scoped>
header {
  padding-bottom: 12px;

  color: $colour-black;

  border-bottom: 2px solid #b0b0b0;
}

main {
  display: flex;
  gap: 58px;

  @media screen and (max-width: 900px) {
    flex-direction: column;
    align-items: center;
  }
}
</style>
