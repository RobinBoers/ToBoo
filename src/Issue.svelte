<script>
    export let item, clickIssue, clickedIssues, i;
    let converter = new showdown.Converter();
</script>

<span on:click={() => {
    clickIssue(item);
}} class="issue-head">

    {#if item.locked}
        <svg aria-hidden="true" height="18" viewBox="0 0 18 18" version="1.1" width="18" data-view-component="true" class="icon"><path fill-rule="evenodd" d="M4 4v2h-.25A1.75 1.75 0 002 7.75v5.5c0 .966.784 1.75 1.75 1.75h8.5A1.75 1.75 0 0014 13.25v-5.5A1.75 1.75 0 0012.25 6H12V4a4 4 0 10-8 0zm6.5 2V4a2.5 2.5 0 00-5 0v2h5zM12 7.5h.25a.25.25 0 01.25.25v5.5a.25.25 0 01-.25.25h-8.5a.25.25 0 01-.25-.25v-5.5a.25.25 0 01.25-.25H12z"></path></svg>
    {:else}
        <svg class="icon" viewBox="0 0 18 18" version="1.1" width="18" height="18" aria-hidden="true"><path d="M8 9.5a1.5 1.5 0 100-3 1.5 1.5 0 000 3z"></path><path fill-rule="evenodd" d="M8 0a8 8 0 100 16A8 8 0 008 0zM1.5 8a6.5 6.5 0 1113 0 6.5 6.5 0 01-13 0z"></path></svg>
    {/if}

    <span class="num">#{item.number}</span>
    {item.title}

    {#if item.state === "closed"}
        <i class="right state">Finished</i>
    {/if}
    {#if item.locked}
        <strong><i class="right state">Locked</i></strong>
    {/if}
</span>
{#if clickedIssues[i] === true}
    <span class="issue-body">
        {#if item.body !== null} 
            <span class="issue-text">{@html converter.makeHtml(item.body)}</span>
        {:else}
            <i class="empty">No description provided. </i><br>
        {/if}
        <button on:click={() => {window.open(item.html_url, "_blank")}}><i class="fab fa-github"></i> Open</button>
        <span class="postedby">Posted by <strong>{item.user.login}</strong></span>
    </span>
{/if}
