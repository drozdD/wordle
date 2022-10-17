<!-- //https://samvcodes.medium.com/how-to-make-a-modal-component-in-svelte-and-tailwind-css-b3f20f9d1624 -->
<script>
// @ts-nocheck

    // @ts-ignore
    import logo from "../assets/logo.png";
    import SettingsModal from "./SettingsModal.svelte";

    export let json;
    export let checked;
    export let settings;
    export let showModal = false;
    const handleToggleModal = () => {
        showModal = !showModal;
    };
</script>

<header class="text-gray-600 body-font">
    <div
        class="container mx-auto flex flex-wrap p-5 flex-col md:flex-row items-center"
    >
        <a
            class="flex title-font font-medium items-center text-gray-900 mb-4 md:mb-0"
            href="/"
        >
            <img src={logo} width="50" height="50" alt="logo" />
            <span class="ml-3 text-xl">Wordle</span>
        </a>
        <nav
            class="md:ml-auto flex flex-wrap items-center text-base justify-center"
        />
        <button
            on:click={() => handleToggleModal()}
            class="inline-flex items-center bg-gray-100 border-0 py-1 px-3 focus:outline-none hover:bg-gray-200 rounded text-base mt-4 md:mt-0"
        >
            <p class="mr-2">Settings</p>
            <svg xmlns="http://www.w3.org/2000/svg" height="24" width="24"
                ><path
                    d="m9.7 21.5-.4-3.05q-.4-.125-.812-.375-.413-.25-.763-.525L4.9 18.75l-2.3-4 2.45-1.85q-.05-.225-.062-.45-.013-.225-.013-.45 0-.2.013-.425.012-.225.062-.475L2.6 9.25l2.3-3.975L7.725 6.45q.35-.275.763-.512Q8.9 5.7 9.3 5.55l.4-3.05h4.6l.4 3.05q.45.175.812.387.363.213.738.513l2.85-1.175 2.3 3.975-2.475 1.875q.05.25.05.45V12q0 .2-.013.412-.012.213-.062.488l2.45 1.85-2.3 4-2.8-1.2q-.375.3-.762.525-.388.225-.788.375l-.4 3.05ZM12 15q1.25 0 2.125-.875T15 12q0-1.25-.875-2.125T12 9q-1.25 0-2.125.875T9 12q0 1.25.875 2.125T12 15Z"
                /></svg
            >
        </button>
    </div>
    <SettingsModal
        open={showModal}
        on:close={() => handleToggleModal()}
        bind:settings={settings}
        bind:checked={checked}
        bind:json={json}
    >
        
    </SettingsModal>
</header>

<!-- {#if showModal} -->

<!-- {/if} -->
