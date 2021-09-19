
<script>
    export let  item
    export let  index

    import { createEventDispatcher } from 'svelte'
    const dispatch = createEventDispatcher()
</script>

<li class="experience__list__item">
    <div class="experience__list__item__info">
        <div class="input_label_holder">
            <label for="experience__company">Company name</label>
            <input type="text" class="experience__company" disabled bind:value={item.company}/>
        </div>
        <div class="input_label_holder">
            <label for="experience__website">Company website</label>
            <input type="text" class="experience__website" disabled bind:value={item.website}/>
        </div>
        <div class="input_label_holder">
            <label for="experience__position">Position title</label>
            <input type="text" class="experience__position" disabled bind:value={item.position}/>
        </div>
        <div class="input_label_holder --fromTo">
            <div>
                <label for="experience__from">From</label>
                <input type="text" class="experience__from" disabled bind:value={item.from}/>
            </div>
            <div>
                <label for="experience__to">To</label>
                <input type="text" class="experience__to" disabled bind:value={item.to}/>
            </div>
        </div>	
        <div class="input_label_holder --ckEditor">
            <label for="experience__description">Description</label>
            <div class="experience__description">{@html item.description} </div>
        </div>
    </div>
    <div class="OrderDeleteBlock__controls">
        <div class="blockOrderUp" on:click={ () => dispatch('orderUpExperience', index ) }> </div> 
        <div class="blockOrderDown" on:click={ () => dispatch('orderDownExperience', index ) }> </div>
        <div class="blockDelete" on:click={ () => dispatch('deleteExperienceItem', index )}></div>
    </div>	
</li>

<style>


</style>
