<script>
    import { createEventDispatcher } from 'svelte'
    const dispatch = createEventDispatcher()

	let companyRef
	let websiteRef
	let positionRef
	let fromRef
	let toRef
    
    function submitForm(){
        const myExperience = {
            company : companyRef.value,
			website : websiteRef.value,
            position : positionRef.value,
            from : fromRef.value,
			to : toRef.value,
            //to : document.querySelector('.experience__to').value,
            description : editorData
        }
		console.log(companyRef.value)

        dispatch('saveExperience', myExperience )
        document.querySelector('.experienceForm').reset()
        editorData = ''
    }



    	//CkEditor
	import CKEditor from "ckeditor5-svelte";
	import DecoupledEditor from "@ckeditor/ckeditor5-build-decoupled-document/build/ckeditor";

	// Setting up editor prop to be sent to wrapper component
	let editor = DecoupledEditor;
	// Reference to initialised editor instance
	let editorInstance = null;
	// Setting up any initial data for the editor
	let editorData = "";

	// If needed, custom editor config can be passed through to the component
	// Uncomment the custom editor config if you need to customise the editor.
	// Note: If you don't pass toolbar object then Document editor will use default set of toolbar items.
	let editorConfig = {
		toolbar: {
		items: [
			"heading",
			"|",
			"fontFamily",
			"fontSize",
			"bold",
			"italic",
			"underline",
			'link', 
			'bulletedList', 
			'numberedList', 
			'blockQuote'
		]
		}
	};

	function onReady({ detail: editor }) {
		// Insert the toolbar before the editable area.
		editorInstance = editor;
		editor.ui
		.getEditableElement()
		.parentElement.insertBefore(
			editor.ui.view.toolbar.element,
			editor.ui.getEditableElement()
		);
	}
	//CkEditor

    
</script>



    
<form class="experienceForm" on:submit|preventDefault={submitForm}>
	<div class="input_label_holder">
		<label for="experience__company">Company name <span>*</span></label>
		<input type="text" class="experience__company" required bind:this={companyRef}/>
	</div>
	<div class="input_label_holder">
		<label for="experience__website">Company website</label>
		<input type="text" class="experience__website" bind:this={websiteRef}/>
	</div>
	<div class="input_label_holder">
		<label for="experience__position">Position title <span>*</span></label>
		<input type="text" class="experience__position" required bind:this={positionRef}/>
	</div>
	<div class="input_label_holder --fromTo">
		<div>
			<label for="experience__from">From <span>*</span></label>
			<input type="text" class="experience__from" required bind:this={fromRef}/>
		</div>
		<div>
			<label for="experience__to">To <span>*</span></label>
			<input type="text" class="experience__to" required bind:this={toRef}/>
		</div>
	</div>
    <div class="input_label_holder --ckEditor">
		<label for="experience__description">Description</label>
		<CKEditor
        bind:editor
        on:ready={onReady}
        bind:config={editorConfig}
        bind:value={editorData} 
        />
    </div>
	<div class="callToActionRight__addButton">
		<button >ADD EXPERIENCE</button>
	</div>
    
</form>


<style>


</style>