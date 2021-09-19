
<script>
    export let  item
    export let  index

    import { createEventDispatcher } from 'svelte'
    const dispatch = createEventDispatcher()
</script>

<li class="experience__list__item">
    <div class="experience__list__item__info">
        <div class="input_label_holder">
            <label for="education__institution">Institution name</label>
            <input type="text" class="education__institution" disabled bind:value={item.institution}/>
        </div>
        <div class="input_label_holder">
            <label for="education__degree">Degree</label>
            <input type="text" class="education__degree" disabled bind:value={item.degree}/>
        </div>
        <div class="input_label_holder">
            <label for="education__from">From</label>
            <input type="text" class="education__from" disabled bind:value={item.from}/>
        </div>
        <div class="input_label_holder">
            <label for="education__to">To</label>
            <input type="text" class="education__to" disabled bind:value={item.to}/>
       </div>	

    </div>
    <div class="OrderDeleteBlock__controls">
        <div class="blockOrderUp" on:click={ () => dispatch('orderUpEducation', index ) }> </div> 
        <div class="blockOrderDown" on:click={ () => dispatch('orderDownEducation', index ) }> </div>
        <div class="blockDelete" on:click={ () => dispatch('deleteEducationItem', index )}></div>
    </div>	
</li>


