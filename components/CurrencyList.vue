<template>
  <FilterInput v-model="filter" />
  <div id="new-component">
    <div id="filter-value">
      {{ filter }}
    </div>
    <button
      type="button"
      class="mt-3 rounded-lg border border-red-700 px-5 py-2.5 text-center text-sm font-medium text-red-700 hover:bg-red-800 hover:text-white focus:outline-none focus:ring-4 focus:ring-red-300"
      data-testid="clear-filter"
      @click="clearFilter"
    >
      Clear Filter
    </button>
    <div id="has-active-filter">
      Is the filter active: {{ isFilterActive ? "Yes" : "No" }}
    </div>
  </div>
  
  <div>
    <button
      type="button"
      class="mt-3 rounded-lg border border-blue-700 px-5 py-2.5 text-center text-sm font-medium text-blue-700 hover:bg-blue-800 hover:text-white focus:outline-none focus:ring-4 focus:ring-blue-300"
      data-testid="set-filter-eth"
      @click="setFilterToETH"
    >
      Set Filter To ETH
    </button>
  </div>

  <div
    class="mt-4 grid grid-cols-1 gap-4 min-[530px]:grid-cols-2 md:mt-6 md:grid-cols-3 md:gap-6 lg:grid-cols-4 xl:grid-cols-5"
    data-testid="card-container"
  >
    <NuxtLink
      v-for="currency in currencyListFiltered"
      :key="`currency-${currency.id}`"
      :to="`currency/${currency.symbol}`"
    >
      <CurrencyCard :symbol="currency.symbol" class="h-full" />
    </NuxtLink>
  </div>
</template>

<script lang="ts" setup>
import type { ICurrency } from "~/types";

const props = withDefaults(
  defineProps<{ currencyList: ICurrency[]; isLoading?: boolean }>(),
  {
    currencyList: () => [],
    isLoading: false,
  }
);

const filter = ref("bitcoin");
const isFilterActive = computed(() => filter.value !== "");

const currencyListFiltered = computed(() => {
  const lowerCaseFilter = filter.value.toLowerCase();
  return props.currencyList.filter(currency =>
    currency.symbol.toLowerCase().includes(lowerCaseFilter)
  );
});

const clearFilter = () => {
  filter.value = "";
};

const setFilterToETH = () => {
  filter.value = "ETH";
};
</script>

