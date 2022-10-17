<script>
    export let settings;
    export let currentWords;
    export let currentWord;
    export let word;

</script>

<div class="flex flex-col">
    {#each Array(currentWords.length) as _, i}
        <div class="flex m-1">
            {#each Array(settings.lettersNumber) as _, j}
                {#if currentWords[i].charAt(j) != ""}
                    {#if currentWord > i}
                        <div class="w-16 h-16 border-2 border-gray-800 float-left mx-1 text-4xl text-center pt-2
                            {word.indexOf(currentWords[i].charAt(j).toLocaleLowerCase()) != -1 ? 'bg-yellow-200' : 'bg-gray-200'}
                            {word.charAt(j) == currentWords[i].charAt(j).toLocaleLowerCase() ? 'bg-green-400' : ''}
                        ">
                            {currentWords[i].charAt(j)}
                        </div>
                    {:else}
                        <div class="w-16 h-16 border-2 border-gray-800 float-left mx-1 text-4xl text-center pt-2">
                            {currentWords[i].charAt(j)}
                        </div>
                    {/if}
                {:else}
                    <div class="w-16 h-16 border-2 border-gray-400 float-left mx-1">
                        
                    </div>
                {/if}
            {/each}
        </div>
    {/each}
</div>  


