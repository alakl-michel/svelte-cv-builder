<script>

	import SingleList from './components/singleList.svelte'

	import Experience from './components/experience.svelte'
	import ExperienceListItem from './components/experienceListItem.svelte'

	import Education from './components/education.svelte'
	import EducationListItem from './components/educationListItem.svelte'
	
	let formValues = {
			firstName : '',
			lastName : '',
			address:'',
			phone:'',
			dob:'',
			email:'',
			position:'',
			profile:'',
			technicalSkills : [],
			languageSkills : [],
			experience : [],
			education : [],
			interests : [],
			references : []
	}
	
	const A4_HEIGHT = 1055 - 110 // mt-mb

	if (localStorage.getItem("formValues")) {
		formValues = JSON.parse(localStorage.getItem('formValues'))
	}

	$: {
		localStorage.setItem("formValues", JSON.stringify(formValues))
	}

	$: experienceCount = formValues.experience.length
	$: educationCount = formValues.education.length

	/// single item lists controls
	function handleSingleList(item){
		if(!item?.detail?.value) return
		formValues[item?.detail?.type] = [...formValues[item?.detail?.type], item?.detail?.value]
	}

	function deleteSingleItem(type, index){
		let dupArray = [...formValues[type]]
		dupArray.splice(index, 1)
		formValues[type] = dupArray
	}





	/// experience controls
	function handleSaveExperience(item){
		if(!item?.detail) return
		formValues.experience = [...formValues.experience, item?.detail]
	}

	function deleteExperienceItem(index){
		let dupArray = [...formValues.experience]
		dupArray.splice(index, 1)
		formValues.experience = dupArray
	}

	function orderUpExperience(index){
		let dupArray = [...formValues.experience]
		const from = index

		const to = ( index > 0 ) ? ( index - 1 ) : 0
		
		dupArray.splice(to, 0, dupArray.splice(from, 1)[0])
		formValues.experience = dupArray
	}

	function orderDownExperience(index){
		let dupArray = [...formValues.experience]
		const from = index
		const item_count = document.querySelectorAll('.experience__list__item').length

		const to = ( index < item_count - 1 ) ? ( index + 1 ) : item_count - 1

		dupArray.splice(to, 0, dupArray.splice(from, 1)[0])
		formValues.experience = dupArray
	}



	/// education controlls
	function handleSaveEducation(item){
		if(!item?.detail) return
		formValues.education = [...formValues.education, item?.detail]
	}

	function deleteEducationItem(index){
		let dupArray = [...formValues.education]
		dupArray.splice(index, 1)
		formValues.education = dupArray
	}

	function orderUpEducation(index){
		let dupArray = [...formValues.education]
		const from = index

		const to = ( index > 0 ) ? ( index - 1 ) : 0
		
		dupArray.splice(to, 0, dupArray.splice(from, 1)[0])
		formValues.education = dupArray
	}

	function orderDownEducation(index){
		let dupArray = [...formValues.education]
		const from = index
		const item_count = document.querySelectorAll('.education__list__item').length

		const to = ( index < item_count - 1 ) ? ( index + 1 ) : item_count - 1

		dupArray.splice(to, 0, dupArray.splice(from, 1)[0])
		formValues.education = dupArray
	}

	function AddPrintPage(){
		const printPreview = document.querySelector('.printPreview')
		const page = document.createElement('div')
		page.className = "printPage"
		printPreview.appendChild(page)
	}

	window.onbeforeprint = function(event) { 

		const printPreviewElems = document.querySelectorAll('.printPreviewElem')
		let currentPage = 0
		let remainingPageHeight = A4_HEIGHT
		
		let printPages = document.querySelectorAll('.printPage')
		if( printPages.length == 0 ) AddPrintPage()

		printPreviewElems.forEach( (element,index) => {
			const elementHeight = element.offsetHeight + element.style.marginTop + element.style.marginBottom

			if( remainingPageHeight >= elementHeight && remainingPageHeight > 100 )
			{
				const printPages = document.querySelectorAll('.printPage')
				printPages[currentPage].appendChild(element)
				remainingPageHeight -= elementHeight
			}else{
				AddPrintPage()
				currentPage++
				remainingPageHeight = A4_HEIGHT

				const printPages = document.querySelectorAll('.printPage')
				printPages[currentPage].appendChild(element)
				remainingPageHeight -= elementHeight
			}

		})

		printPages = document.querySelectorAll('.printPage')
		printPages.forEach( (element,index) => {
			if( element.childElementCount  ==  0) element.remove()
		})

	}// before print

	function saveToPdf(){
		window.print();
	}


</script>

<main class="builder">
	<!--
	<div>
		
		<pre>
			{JSON.stringify(formValues,null, 2)}
		</pre>
	
	</div>
	-->
	<form>
		<div class="safearea">
			
			<div class="basicInformation">
				<h3>Basic Information</h3>
				<div class="input_label_holder">
					<label for="firstName">First Name <span>*</span></label>
					<input type="text" id="firstName" bind:value={formValues.firstName} required/>
				</div>
				<div class="input_label_holder">
					<label for="lastName">Last Name <span>*</span></label>
					<input type="text" id="lastName" bind:value={formValues.lastName} required/>
				</div>
				<div class="input_label_holder">
					<label for="address">Address <span>*</span></label>
					<input type="text" id="address" bind:value={formValues.address} required/>
				</div>
				<div class="input_label_holder">
					<label for="phone">Phone <span>*</span></label>
					<input type="text" id="phone" bind:value={formValues.phone} required/>
				</div>
				<div class="input_label_holder">
					<label for="dob">DOB <span>*</span></label>
					<input type="text" id="dob" bind:value={formValues.dob} required/>
				</div>
				<div class="input_label_holder">
					<label for="email">Email <span>*</span></label>
					<input type="email" id="email" bind:value={formValues.email} required/>
				</div>
				<div class="input_label_holder">
					<label for="position">Position <span>*</span></label>
					<input type="text" id="position" bind:value={formValues.position} required/>
				</div>
				<div class="input_label_holder">
					<label for="profile">Profile</label>
					<textarea id="profile" bind:value={formValues.profile}></textarea>
				</div>
			</div>


			<div class="singleList technicalSkillsList">
				<h3>Technical Skills</h3>
				<ul class="singleList__ul">
					{#each formValues.technicalSkills as item, index}
					<li>{item} <span on:click={ () => deleteSingleItem('technicalSkills', index ) }></span></li>
					{/each}
				</ul>
				<SingleList type="technicalSkills" displayName="technical skill" on:saveSingleList={(event) => handleSingleList(event)}/>
			</div>
			


			<div class="singleList languageSkillsList">
				<h3>Language Skills</h3>
				<ul class="singleList__ul">
					{#each formValues.languageSkills as item, index}
					<li>{item} <span on:click={ () => deleteSingleItem('languageSkills', index ) }></span></li>
					{/each}
				</ul>
				<SingleList type="languageSkills" displayName="language skill" on:saveSingleList={(event) => handleSingleList(event)}/>
			</div>	



			<div class="singleList interestsList">
				<h3>Interests</h3>
				<ul class="singleList__ul">
					{#each formValues.interests as item, index}
					<li>{item} <span on:click={ () => deleteSingleItem('interests', index ) }></span></li>
					{/each}
				</ul>
				<SingleList type="interests" displayName="interest" on:saveSingleList={(event) => handleSingleList(event)}/>
			</div>



			<div class="experinceSection">
				<h3>Experience</h3>
				<ul class="experience__list">
					{#each formValues.experience as item, index}
						<ExperienceListItem 
						item={item} 
						index={index}
						on:orderUpExperience={ () => orderUpExperience(index )}
						on:orderDownExperience={ () => orderDownExperience(index )}
						on:deleteExperienceItem={ () =>  deleteExperienceItem(index)}
						/>
					{/each}
				</ul>
				{#if experienceCount > 0 }
					<h3>Add Experience</h3>
				{/if}
				<Experience  on:saveExperience={(event) => handleSaveExperience(event)}/>
			</div>

			<div class="educationSection">
				<h3>Education</h3>
				<ul class="education__list">
					{#each formValues.education as item, index}
						<EducationListItem 
						item={item} 
						index={index}
						on:orderUpEducation={ () => orderUpEducation(index )}
						on:orderDownEducation={ () => orderDownEducation(index )}
						on:deleteEducationItem={ () =>  deleteEducationItem(index)}
						/>
					{/each}
				</ul>
				{#if educationCount > 0 }
					<h3>Add Education</h3>
				{/if}
				<Education on:saveEducation={(event) => handleSaveEducation(event)}/>
			<div/>	

			<div class="callToActionRight__addButton --upperSeparator">
				<button on:click|preventDefault={saveToPdf}>SAVE PDF</button>
			</div>

		<div/><!--safearea-->
	</form>
	
</main>


<div class="printPreview theme-0">

		<div class="printPreview__basicInfo printPreviewElem">
			<address>Address: {formValues.address}</address>
			<label for="printPreview__phone">Phone: <span>{formValues.phone}</span></label>
			<label for="printPreview__dob">Date of Birth: <span>{formValues.dob}</span></label>
			<label for="printPreview__email">E-mail: <span>{formValues.email}</span></label>

			<div class="printPreview__nameHolder">
				<label for="printPreview__name">{formValues.firstName} {formValues.lastName} - <span>{formValues.position}</span></label>
			</div>

			<h3>PROFILE</h3>
			<div class="printPreview__profile">{formValues.profile}</div>
		</div>

		<h3 class="printPreviewElem">EXPERIENCE</h3>
		
		{#each formValues.experience as item, index}
			<ul class="printPreview__experience__list printPreviewElem">
				<li class="printPreview__experience__list__item " >
					<div class="printPreview__experience__list__head">{item.company}, <a href="{item.website}">{item.website}</a> <span> - {item.position}</span></div>
					<div class="printPreview__experience__list__fromTo">{item.from} - {item.to}</div>
					<div class="printPreview__experience__list__description">{@html item.description}</div>
				</li>
			</ul>
		{/each}

		<h3 class="printPreviewElem">EDUCATION</h3>
		
		{#each formValues.education as item, index}
			<ul class="printPreview__experience__list printPreviewElem">
				<li class="printPreview__experience__list__item " >
					<div class="printPreview__experience__list__head">{item.institution}</div>
					<div class="printPreview__experience__list__head"><span>{item.degree}</span></div>
					<div class="printPreview__experience__list__fromTo">{item.from} - {item.to}</div>
				</li>
			</ul>
		{/each}
		

		
		<ul class="printPreview__technicalSkills printPreviewElem">	
			<h3>TECHNICAL SKILLS</h3>
			{#each formValues.technicalSkills as skill, index}
				<li class="printPreview__technicalSkill ">{skill}</li>
			{/each}
		</ul>
		
		<ul class="printPreview__technicalSkills printPreviewElem">	
			<h3>LANGUAGE SKILLS</h3>
			{#each formValues.languageSkills as skill, index}
				<li class="printPreview__technicalSkill ">{skill}</li>
			{/each}
		</ul>
		
		<ul class="printPreview__technicalSkills printPreviewElem">
			<h3>INTERESTS </h3>
			{#each formValues.interests as interest, index}
				<li class="printPreview__technicalSkill">{interest}</li>
			{/each}
		</ul>
		
		
</div>
