<script>
	export let repos, recents, newRecent, config, selectRepo;
</script>

<h1>To-Boo<span>Your New To-Do App!</span></h1>	

{#if recents.length !== 0}
	<h2>Recently opened</h2>

	<div class="ul-wrapper">
		<ul>
			{#each recents as item}
				
				{#if item !== null && item !== ""}
					<li on:click={selectRepo(item)}>
						<svg aria-label="Repository" role="img" height="18" viewBox="0 0 18 18" version="1.1" width="16" data-view-component="true" class="icon">
							<path fill-rule="evenodd" d="M2 2.5A2.5 2.5 0 014.5 0h8.75a.75.75 0 01.75.75v12.5a.75.75 0 01-.75.75h-2.5a.75.75 0 110-1.5h1.75v-2h-8a1 1 0 00-.714 1.7.75.75 0 01-1.072 1.05A2.495 2.495 0 012 11.5v-9zm10.5-1V9h-8c-.356 0-.694.074-1 .208V2.5a1 1 0 011-1h8zM5 12.25v3.25a.25.25 0 00.4.2l1.45-1.087a.25.25 0 01.3 0L8.6 15.7a.25.25 0 00.4-.2v-3.25a.25.25 0 00-.25-.25h-3.5a.25.25 0 00-.25.25z"></path>
						</svg> {item}
					</li>
				{/if}

			{:else}
				<p>Loading recents...</p>
			{/each}
		</ul>
	</div>

	<h2>Select repository</h2>
{:else}
	<p>Looks like you're new, select a repository to get started!</p>
	<h2 class="select">Select repository</h2>
{/if}

<form on:submit|preventDefault={() => selectRepo(newRecent)}>
	<select bind:value={newRecent}>
		<option value="" disabled selected>
			Select repository
		</option>
		{#each repos as repo}
			{#if repo.has_issues === true && repo.archived !== true && repo.disabled !== true} 
				{#if repo.open_issues_count > 0 || config.showNoOpen}
					<option value="{repo.name}">
						{repo.name}
					</option>
				{/if}
			{/if}
		{:else}
			<p>Loading repositories...</p>
		{/each}
	</select>
	<input type="submit" value="Open"><br>

	<label for="noOpen">
		<input bind:checked={config.showNoOpen} type="checkbox" id="noOpen" name="noOpen">
		&nbsp;Show repositories with 0 open issues
	</label>
</form>