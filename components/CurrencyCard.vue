<template>
  <div class="group relative cursor-pointer" data-testid="currency-card">
    <div
      class="absolute -inset-0.5 rounded-lg bg-gradient-to-r from-rose-400 via-fuchsia-500 to-indigo-500 opacity-0 blur transition duration-300 group-hover:opacity-75"
    ></div>
    <div
      class="flex-grow-1 relative flex h-full w-full flex-col justify-between rounded-md bg-white p-4 shadow-lg"
    >
      <div class="flex gap-1">
        <div class="grow text-zinc-700">
          <h2 data-testid="title" class="text-xl">{{ currency.name }}</h2>
          <h3 data-testid="formatted-price" class="mt-2 text-sm font-bold">
            {{ formattedPrice }}
          </h3>
        </div>
        <img
          data-testid="logo"
          class="h-10 w-10"
          src="/img/svg-crypto-logos/btc.svg"
          alt="Logo"
        />
      </div>
      <div class="mt-4 flex items-center justify-between">
        <img
          data-testid="toggle-favorite-button"
          class="h-8 w-8"
          src="/img/icons/favorite-inactive.svg"
          alt="Favorite toggle"
        />
        <img
          data-testid="currency-details-button"
          class="h-6 w-6"
          src="/img/icons/chevron-right.svg"
          alt="View Details"
        />
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { useCurrency } from "~/composables/currency";

const props = defineProps<{ symbol: string }>();

const { symbol, toggleFavorite, isFavorite, formattedPrice, currency } =
  useCurrency(props.symbol);
</script>
