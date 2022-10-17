<script>
    import backspace from '../assets/backspace.svg';
    export let lettersToHighlight;
    let letters1 = ["Q","W","E","R","T","Y","U","I","O","P"]
    let letters2 = ["A","S","D","F","G","H","J","K","L"]
    let letters3 = ["ENTER","Z","X","C","V","B","N","M"]
</script>
<div class="flex flex-col items-center mt-5">
    <div class="flex m-1 items-center">
        {#each letters1 as letter}
            <div class="w-10 h-12 bg-gray-200 rounded-md text-black float-left mx-1 text-center justify-center leading-10
                {lettersToHighlight[letter.toLowerCase()] == "gray" ? 'bg-gray-400' : ''}
                {lettersToHighlight[letter.toLowerCase()] == "yellow" ? 'bg-yellow-400' : ''}
                {lettersToHighlight[letter.toLowerCase()] == "green" ? 'bg-green-400' : ''}
            ">
                {letter}
            </div>
        {/each}
    </div>
    <div class="flex m-1 items-center">
        {#each letters2 as letter}
            <div class="w-10 h-12 bg-gray-200 rounded-md text-black float-left mx-1 text-center justify-center leading-10
            {lettersToHighlight[letter.toLowerCase()] == "gray" ? 'bg-gray-400' : ''}
            {lettersToHighlight[letter.toLowerCase()] == "yellow" ? 'bg-yellow-400' : ''}
            {lettersToHighlight[letter.toLowerCase()] == "green" ? 'bg-green-400' : ''}
            ">
                {letter}
            </div>
        {/each}
    </div>
    <div class="flex m-1 items-center">
        {#each letters3 as letter, i}
            {#if i==0}
                <div class="w-14 h-12 bg-gray-200 rounded-md text-black float-left mx-1 text-center justify-center leading-10">
                    {letter}
                </div>
            {:else}
                <div class="w-10 h-12 bg-gray-200 rounded-md text-black float-left mx-1 text-center justify-center leading-10
                {lettersToHighlight[letter.toLowerCase()] == "gray" ? 'bg-gray-400' : ''}
                {lettersToHighlight[letter.toLowerCase()] == "yellow" ? 'bg-yellow-400' : ''}
                {lettersToHighlight[letter.toLowerCase()] == "green" ? 'bg-green-400' : ''}
                ">
                    {letter}
                </div>
            {/if}
        {/each}
        <div class="w-14 h-12 bg-gray-200 rounded-md text-black float-left mx-1 text-center justify-center flex">
            <img src={backspace} alt="adawdw"/>
        </div>
    </div>
</div>
