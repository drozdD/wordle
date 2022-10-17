<script>
  // @ts-nocheck

  import { createEventDispatcher } from "svelte";
  export let open = false;
  const dispatch = createEventDispatcher();
  // @ts-ignore
  export let settings;

  let files = [];
  export let checked;
  export let json;
  let err = false;
  let file;
  let numberOfLetters = settings.lettersNumber;
  let warning = false;
  function saveSettings() {
    if (numberOfLetters < 4 || numberOfLetters > 9) {
      warning = true;
      return;
    }
    // @ts-ignore
    if (checked) {
      if (files.length == 0) {
        err = true;
        return;
      }
      json = file;
    }
    warning = false;
    settings.lettersNumber = numberOfLetters;

    dispatch("close");
  }

  async function read() {
    const text = await files[0].text();
    file = JSON.parse(text);
    console.log(json);
  }
</script>

{#if open}
  <div
    class="modal z-50 fixed w-full h-full top-0 left-0 flex items-center justify-center p-8 lg:p-0"
  >
    <div class="modal-overlay fixed w-full h-full bg-gray-900 opacity-50" />
    <div
      class="bg-white w-1/2 h-1/2 mx-auto rounded-lg shadow-xl z-50 overflow-y-auto relative"
    >
      <div class="head bg-gray-100 py-5 px-8 text-2xl font-extrabold">
        Settings
        <button
          class="p-2 bg-gray-200 hover:bg-gray-300 rounded-full ml-4 float-right"
          on:click={() => dispatch("close")}
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            height="24px"
            viewBox="0 0 24 24"
            width="24px"
            fill="#000000"
            ><path d="M0 0h24v24H0V0z" fill="none" /><path
              d="M19 6.41L17.59 5 12 10.59 6.41 5 5 6.41 10.59 12 5 17.59 6.41 19 12 13.41 17.59 19 19 17.59 13.41 12 19 6.41z"
            /></svg
          >
        </button>
      </div>
      <div class="content p-8 flex flex-col items-center text-xl">
        <label for="lettersNumber">- Wpisz ilosc liter (4-9)</label>
        <input
          type="number"
          id="lettersNumber"
          bind:value={numberOfLetters}
          class="border-2 rounded-md border-gray-400 text-4xl w-12 h-14 text-center"
        />
        {#if warning}
          <p class="text-red-500 border-3 border-gray-900 rounded-lg">
            Wybierz ilosc liter między 4 a 9
          </p>
        {/if}
        <div>
          <label for="checkBox">- Użyj słów z pliku json </label>
          <input
            type="checkbox"
            class="border-1 rounded-md border-gray-400 w-6 h-6 align-middle"
            id="checkBox"
            bind:checked
          />
        </div>
        {#if checked}
          <input
            type="file"
            bind:files
            accept="application/json"
            on:change={read}
            class="text-sm mt-2"
          />
          {#if err}
            <p class="text-red-500 border-3 border-gray-900 rounded-lg">
              Nie dodałeś pliku!
            </p>
          {/if}
        {/if}
      </div>
      <div class="absolute bottom-0 right-0 m-10">
        <button
          on:click={() => saveSettings()}
          class="rounded-lg bg-gray-700 h-12 w-14 text-white">SAVE</button
        >
      </div>
    </div>
  </div>
{/if}
