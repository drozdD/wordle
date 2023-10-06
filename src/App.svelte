<script>
  // @ts-nocheck

  import { onMount } from "svelte";
  import Header from "./components/Header.svelte";
  import GameBoard from "./components/GameBoard.svelte";
  import Keyboard from "./components/Keyboard.svelte";
  import wordList from "word-list-json";
  import Win from "./components/Win.svelte";

  let json;
  let openLoseModal = false;
  let checked = false;
  let showModal = false;
  let openWinModal = false;
  let words;
  let word;
  let settings = {
    lettersNumber: Math.floor(Math.random() * (9 - 4 + 1)) + 4,
  };
  let currentWord = 0;
  let currentWords = [];
  let lettersToHighlight = {};

  function selectRandomWord() {
    if (checked) {
      let num = settings.lettersNumber.toString()
      words = json[num]
    } else {
      words = wordList.filter(checkLength);

      function checkLength(x) {
        return x.length == settings.lettersNumber;
      }
    }
    let randomWord = Math.floor(Math.random() * (words.length + 1));
    word = words[randomWord];
    currentWord = 0;
    currentWords = [];
    for(var i = 0; i <= settings.lettersNumber; i++){
      currentWords.push("")
    }
    lettersToHighlight = {};
    console.log(word);
    console.log(words);
  }

  function onKeyDown(e) {
    if (showModal) {
      return;
    }
    if (
      e.keyCode > 64 &&
      e.keyCode < 91 &&
      currentWords[currentWord].length < word.length
    ) {
      currentWords[currentWord] += String.fromCharCode(e.keyCode);
    }
    if (e.keyCode == 8) {
      currentWords[currentWord] = currentWords[currentWord].slice(0, -1);
    }
    if (e.keyCode == 13 && currentWords[currentWord].length == word.length) {
      checkWord();
    }
  }

  function checkWord() {
    let checkingWord = currentWords[currentWord].toLocaleLowerCase();
    if (checkingWord == word) {
      for (var i = 0; i <= word.length; i++) {
        lettersToHighlight[checkingWord.charAt(i)] = "gray";
        if (word.indexOf(checkingWord.charAt(i)) != -1) {
          lettersToHighlight[checkingWord.charAt(i)] = "yellow";
        }
        if (word.charAt(i) == checkingWord.charAt(i)) {
          lettersToHighlight[checkingWord.charAt(i)] = "green";
        }
      }
      openWinModal = true;
      console.log("win");
      //win
    } else {
      if (words.includes(checkingWord)) {
        for (var i = 0; i <= word.length; i++) {
          lettersToHighlight[checkingWord.charAt(i)] = "gray";
          if (word.indexOf(checkingWord.charAt(i)) != -1) {
            lettersToHighlight[checkingWord.charAt(i)] = "yellow";
          }
          if (word.charAt(i) == checkingWord.charAt(i)) {
            lettersToHighlight[checkingWord.charAt(i)] = "green";
          }
        }
        currentWord++;
        console.log("ta");
      } else {
        console.log("nie");
      }
    }
    console.log(currentWord, currentWords.length)
    if(currentWord >= currentWords.length){
      openLoseModal = true
    }

  }

  //selectRandomWord();

  $: settings.lettersNumber, selectRandomWord();
  $: json, selectRandomWord();
</script>

<Header bind:settings bind:showModal bind:checked bind:json />
<!-- svelte-ignore a11y-no-noninteractive-tabindex -->
<main class="h-auto flex flex-col items-center mt-10 text-[#213547]">
  <GameBoard {settings} {currentWord} {currentWords} {word} />
  <Keyboard {lettersToHighlight} />
  <Win bind:openWinModal={openWinModal} bind:openLoseModal={openLoseModal} {selectRandomWord} {word}/>
</main>

<svelte:window on:keydown={onKeyDown} />
