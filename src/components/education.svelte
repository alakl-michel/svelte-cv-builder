<script>
    import { createEventDispatcher } from 'svelte'
    const dispatch = createEventDispatcher()

    let institutionRef
    let degreeRef
	let fromRef
	let toRef
    
    function submitForm(){
        let myEducation = {
            institution : institutionRef.value,
            degree : degreeRef.value,
            from : fromRef.value,
            to : toRef.value
            //to : document.querySelector('.education__to').value
        }
        dispatch('saveEducation', myEducation )
        document.querySelector('.educationForm').reset()
    }



    
</script>
    
<form class="educationForm" on:submit|preventDefault={submitForm}>
    <div class="input_label_holder">
        <label for="education__institution">Institution name</label>
        <input type="text" class="education__institution" required bind:this={institutionRef}/>
    </div>
    <div class="input_label_holder">
        <label for="education__degree">Degree</label>
        <input type="text" class="education__degree" required bind:this={degreeRef}/>
    </div>   
    <div class="input_label_holder">
        <label for="education__from">From</label>
        <input type="text" class="education__from" required bind:this={fromRef}/>
    </div> 
    <div class="input_label_holder">
        <label for="education__to">To</label>
        <input type="text" class="education__to" required bind:this={toRef}/>
    </div> 
    <div class="callToActionRight__addButton">
        <button>ADD EDUCATION</button>
    </div>
</form>


