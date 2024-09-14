<script>
  import { onMount } from "svelte";

  import Card from "./lib/components/CardProxy.svelte";

  let showcase;
  let isLoading = true;

  const getCards = async () => {
    let cardFetch = await fetch("/data/cards.json");
    let cards = await cardFetch.json();
    return cards;
  };

  const loadCards = async () => {
    return getCards().then((cards) => {
      showcase = cards[0];
      isLoading = false;
    });
  };

  onMount(() => {
    loadCards();
  });
</script>

<main>
  <div class="showcase">
    {#if !showcase}
      loading...
    {:else}
      <Card
        id={showcase.id}
        name={showcase.name}
        set={showcase.set}
        number={showcase.number}
        types={showcase.types}
        supertype={showcase.supertype}
        subtypes={showcase.subtypes}
        rarity={showcase.rarity}
        isReverse={showcase.isReverse}
        showcase={true}
      />
    {/if}
  </div>
</main>
