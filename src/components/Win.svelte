<script>
    export let openWinModal;
    export let selectRandomWord;
    export let openLoseModal;
    export let word;

    function playAgain(){
        openWinModal=false
        openLoseModal=false
        selectRandomWord();
    }
</script>

{#if openWinModal}
    <div
        class="modal z-50 fixed w-full h-full top-0 left-0 flex items-center justify-center p-8 lg:p-0"
    >
        <div class="modal-overlay fixed w-full h-full bg-gray-900 opacity-50" />
        <div
            class="bg-white w-1/3 h-1/3 mx-auto rounded-lg shadow-xl z-50 overflow-y-auto relative"
        >
            <div class="head bg-gray-100 py-5 px-8 text-2xl font-extrabold text-center text-green-600">
                YOU WIN!!!
            </div>
            <div class="content p-8 flex flex-col items-center text-xl" />
            <div class="absolute bottom-0 right-0 m-10">
                <button
                    on:click={() => playAgain()}
                    class="rounded-lg bg-gray-700 h-16 w-24 text-white"
                    >PLAY AGAIN</button
                >
            </div>
        </div>
    </div>
{/if}
{#if openLoseModal}
    <div
        class="modal z-50 fixed w-full h-full top-0 left-0 flex items-center justify-center p-8 lg:p-0"
    >
        <div class="modal-overlay fixed w-full h-full bg-gray-900 opacity-50" />
        <div
            class="bg-white w-1/3 h-1/3 mx-auto rounded-lg shadow-xl z-50 overflow-y-auto relative"
        >
            <div class="head bg-gray-100 py-5 px-8 text-2xl font-extrabold text-center text-red-400">
                YOU LOSE :c
            </div>
            <div class="content p-8 flex flex-col items-center text-xl" >
                correct word - {word}
            </div>
            <div class="absolute bottom-0 right-0 m-10">
                <button
                    on:click={() => playAgain()}
                    class="rounded-lg bg-gray-700 h-16 w-24 text-white"
                    >PLAY AGAIN</button
                >
            </div>
        </div>
    </div>
{/if}
