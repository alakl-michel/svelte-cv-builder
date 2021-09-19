<script>
export let type
export let displayName

import { createEventDispatcher } from 'svelte'
const dispatch = createEventDispatcher()

function handleClick(){
    dispatch('saveSingleList', { value : document.querySelector(`.singleListInput__${type}`).value, type : type } )
    document.querySelector(`.singleListInput__${type}`).value = ''
}


import Languages from "../json/languages.json"
let listData = (  type == 'languageSkills') ? 'languages' : ''
const LanguagesList = Object.values(Languages)

//import { onMount } from "svelte";
// onMount(() => {
//     console.log(Languages)
// });



</script>
    
<div class="singleList__formHolder">
    <label for="singleListInput">Add {displayName}</label>


    <input type="text" class="singleListInput__{type}"  list="{listData}" />
    {#if type == 'languageSkills'}
        <datalist id="languages">
            {#each LanguagesList as language }
                <option value="{language.name} - {language.nativeName}">
            {/each}
        </datalist>
    {/if}    
    
    <button on:click|preventDefault={ handleClick }>ADD</button>
</div>