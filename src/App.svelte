<script>

	import { onMount } from 'svelte';
	
	let recents = [];
	let newRecent = "";
	let errorMessage = "";

	let repos = [];
	let issues = [];

	let currentProject = "";
	let projectLayout = false;

	const debugmode = true;
	const username = "RobinBoers";

	let showFinished = false;

	let showNoOpen = true;

	let clickedIssues = [];

	onMount(() => {
		const existingRecents = localStorage.getItem("recents");
		recents = JSON.parse(existingRecents) || [];

		repos = getRepos(username);
		console.log(repos);
		if(repos.message) {
			errorMessage = repos.message;
			repos = null;
		}
	});

	function Get(yourUrl){
		var Httpreq = new XMLHttpRequest(); // a new request
		Httpreq.open("GET",yourUrl,false);
		Httpreq.send(null);
		return Httpreq.response;   
	}

	function getRepos(username) {
		if(debugmode) {
			return [ { "id": 289456707, "node_id": "MDEwOlJlcG9zaXRvcnkyODk0NTY3MDc=", "name": "BetterPainting", "full_name": "RobinBoers/BetterPainting", "private": false, "owner": { "login": "RobinBoers", "id": 60298132, "node_id": "MDQ6VXNlcjYwMjk4MTMy", "avatar_url": "https://avatars.githubusercontent.com/u/60298132?v=4", "gravatar_id": "", "url": "https://api.github.com/users/RobinBoers", "html_url": "https://github.com/RobinBoers", "followers_url": "https://api.github.com/users/RobinBoers/followers", "following_url": "https://api.github.com/users/RobinBoers/following{/other_user}", "gists_url": "https://api.github.com/users/RobinBoers/gists{/gist_id}", "starred_url": "https://api.github.com/users/RobinBoers/starred{/owner}{/repo}", "subscriptions_url": "https://api.github.com/users/RobinBoers/subscriptions", "organizations_url": "https://api.github.com/users/RobinBoers/orgs", "repos_url": "https://api.github.com/users/RobinBoers/repos", "events_url": "https://api.github.com/users/RobinBoers/events{/privacy}", "received_events_url": "https://api.github.com/users/RobinBoers/received_events", "type": "User", "site_admin": false }, "html_url": "https://github.com/RobinBoers/BetterPainting", "description": "A Datapack wich adds an easy to use painting tools to Minecraft", "fork": false, "url": "https://api.github.com/repos/RobinBoers/BetterPainting", "forks_url": "https://api.github.com/repos/RobinBoers/BetterPainting/forks", "keys_url": "https://api.github.com/repos/RobinBoers/BetterPainting/keys{/key_id}", "collaborators_url": "https://api.github.com/repos/RobinBoers/BetterPainting/collaborators{/collaborator}", "teams_url": "https://api.github.com/repos/RobinBoers/BetterPainting/teams", "hooks_url": "https://api.github.com/repos/RobinBoers/BetterPainting/hooks", "issue_events_url": "https://api.github.com/repos/RobinBoers/BetterPainting/issues/events{/number}", "events_url": "https://api.github.com/repos/RobinBoers/BetterPainting/events", "assignees_url": "https://api.github.com/repos/RobinBoers/BetterPainting/assignees{/user}", "branches_url": "https://api.github.com/repos/RobinBoers/BetterPainting/branches{/branch}", "tags_url": "https://api.github.com/repos/RobinBoers/BetterPainting/tags", "blobs_url": "https://api.github.com/repos/RobinBoers/BetterPainting/git/blobs{/sha}", "git_tags_url": "https://api.github.com/repos/RobinBoers/BetterPainting/git/tags{/sha}", "git_refs_url": "https://api.github.com/repos/RobinBoers/BetterPainting/git/refs{/sha}", "trees_url": "https://api.github.com/repos/RobinBoers/BetterPainting/git/trees{/sha}", "statuses_url": "https://api.github.com/repos/RobinBoers/BetterPainting/statuses/{sha}", "languages_url": "https://api.github.com/repos/RobinBoers/BetterPainting/languages", "stargazers_url": "https://api.github.com/repos/RobinBoers/BetterPainting/stargazers", "contributors_url": "https://api.github.com/repos/RobinBoers/BetterPainting/contributors", "subscribers_url": "https://api.github.com/repos/RobinBoers/BetterPainting/subscribers", "subscription_url": "https://api.github.com/repos/RobinBoers/BetterPainting/subscription", "commits_url": "https://api.github.com/repos/RobinBoers/BetterPainting/commits{/sha}", "git_commits_url": "https://api.github.com/repos/RobinBoers/BetterPainting/git/commits{/sha}", "comments_url": "https://api.github.com/repos/RobinBoers/BetterPainting/comments{/number}", "issue_comment_url": "https://api.github.com/repos/RobinBoers/BetterPainting/issues/comments{/number}", "contents_url": "https://api.github.com/repos/RobinBoers/BetterPainting/contents/{+path}", "compare_url": "https://api.github.com/repos/RobinBoers/BetterPainting/compare/{base}...{head}", "merges_url": "https://api.github.com/repos/RobinBoers/BetterPainting/merges", "archive_url": "https://api.github.com/repos/RobinBoers/BetterPainting/{archive_format}{/ref}", "downloads_url": "https://api.github.com/repos/RobinBoers/BetterPainting/downloads", "issues_url": "https://api.github.com/repos/RobinBoers/BetterPainting/issues{/number}", "pulls_url": "https://api.github.com/repos/RobinBoers/BetterPainting/pulls{/number}", "milestones_url": "https://api.github.com/repos/RobinBoers/BetterPainting/milestones{/number}", "notifications_url": "https://api.github.com/repos/RobinBoers/BetterPainting/notifications{?since,all,participating}", "labels_url": "https://api.github.com/repos/RobinBoers/BetterPainting/labels{/name}", "releases_url": "https://api.github.com/repos/RobinBoers/BetterPainting/releases{/id}", "deployments_url": "https://api.github.com/repos/RobinBoers/BetterPainting/deployments", "created_at": "2020-08-22T09:14:48Z", "updated_at": "2020-08-24T08:52:01Z", "pushed_at": "2020-08-22T13:30:33Z", "git_url": "git://github.com/RobinBoers/BetterPainting.git", "ssh_url": "git@github.com:RobinBoers/BetterPainting.git", "clone_url": "https://github.com/RobinBoers/BetterPainting.git", "svn_url": "https://github.com/RobinBoers/BetterPainting", "homepage": null, "size": 9, "stargazers_count": 1, "watchers_count": 1, "language": "mcfunction", "has_issues": true, "has_projects": true, "has_downloads": true, "has_wiki": true, "has_pages": false, "forks_count": 0, "mirror_url": null, "archived": false, "disabled": false, "open_issues_count": 4, "license": null, "forks": 0, "open_issues": 0, "watchers": 1, "default_branch": "master" }, { "id": 329600855, "node_id": "MDEwOlJlcG9zaXRvcnkzMjk2MDA4NTU=", "name": "blogger-theme-collection", "full_name": "RobinBoers/blogger-theme-collection", "private": false, "owner": { "login": "RobinBoers", "id": 60298132, "node_id": "MDQ6VXNlcjYwMjk4MTMy", "avatar_url": "https://avatars.githubusercontent.com/u/60298132?v=4", "gravatar_id": "", "url": "https://api.github.com/users/RobinBoers", "html_url": "https://github.com/RobinBoers", "followers_url": "https://api.github.com/users/RobinBoers/followers", "following_url": "https://api.github.com/users/RobinBoers/following{/other_user}", "gists_url": "https://api.github.com/users/RobinBoers/gists{/gist_id}", "starred_url": "https://api.github.com/users/RobinBoers/starred{/owner}{/repo}", "subscriptions_url": "https://api.github.com/users/RobinBoers/subscriptions", "organizations_url": "https://api.github.com/users/RobinBoers/orgs", "repos_url": "https://api.github.com/users/RobinBoers/repos", "events_url": "https://api.github.com/users/RobinBoers/events{/privacy}", "received_events_url": "https://api.github.com/users/RobinBoers/received_events", "type": "User", "site_admin": false }, "html_url": "https://github.com/RobinBoers/blogger-theme-collection", "description": "My custom blogger themes", "fork": false, "url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection", "forks_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/forks", "keys_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/keys{/key_id}", "collaborators_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/collaborators{/collaborator}", "teams_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/teams", "hooks_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/hooks", "issue_events_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/issues/events{/number}", "events_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/events", "assignees_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/assignees{/user}", "branches_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/branches{/branch}", "tags_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/tags", "blobs_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/git/blobs{/sha}", "git_tags_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/git/tags{/sha}", "git_refs_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/git/refs{/sha}", "trees_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/git/trees{/sha}", "statuses_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/statuses/{sha}", "languages_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/languages", "stargazers_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/stargazers", "contributors_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/contributors", "subscribers_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/subscribers", "subscription_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/subscription", "commits_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/commits{/sha}", "git_commits_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/git/commits{/sha}", "comments_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/comments{/number}", "issue_comment_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/issues/comments{/number}", "contents_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/contents/{+path}", "compare_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/compare/{base}...{head}", "merges_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/merges", "archive_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/{archive_format}{/ref}", "downloads_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/downloads", "issues_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/issues{/number}", "pulls_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/pulls{/number}", "milestones_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/milestones{/number}", "notifications_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/notifications{?since,all,participating}", "labels_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/labels{/name}", "releases_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/releases{/id}", "deployments_url": "https://api.github.com/repos/RobinBoers/blogger-theme-collection/deployments", "created_at": "2021-01-14T11:54:44Z", "updated_at": "2021-08-09T19:03:27Z", "pushed_at": "2021-08-09T19:03:25Z", "git_url": "git://github.com/RobinBoers/blogger-theme-collection.git", "ssh_url": "git@github.com:RobinBoers/blogger-theme-collection.git", "clone_url": "https://github.com/RobinBoers/blogger-theme-collection.git", "svn_url": "https://github.com/RobinBoers/blogger-theme-collection", "homepage": "", "size": 102, "stargazers_count": 0, "watchers_count": 0, "language": null, "has_issues": true, "has_projects": true, "has_downloads": true, "has_wiki": true, "has_pages": false, "forks_count": 0, "mirror_url": null, "archived": false, "disabled": false, "open_issues_count": 0, "license": null, "forks": 0, "open_issues": 0, "watchers": 0, "default_branch": "master" }, { "id": 236207866, "node_id": "MDEwOlJlcG9zaXRvcnkyMzYyMDc4NjY=", "name": "BloggerAPP", "full_name": "RobinBoers/BloggerAPP", "private": false, "owner": { "login": "RobinBoers", "id": 60298132, "node_id": "MDQ6VXNlcjYwMjk4MTMy", "avatar_url": "https://avatars.githubusercontent.com/u/60298132?v=4", "gravatar_id": "", "url": "https://api.github.com/users/RobinBoers", "html_url": "https://github.com/RobinBoers", "followers_url": "https://api.github.com/users/RobinBoers/followers", "following_url": "https://api.github.com/users/RobinBoers/following{/other_user}", "gists_url": "https://api.github.com/users/RobinBoers/gists{/gist_id}", "starred_url": "https://api.github.com/users/RobinBoers/starred{/owner}{/repo}", "subscriptions_url": "https://api.github.com/users/RobinBoers/subscriptions", "organizations_url": "https://api.github.com/users/RobinBoers/orgs", "repos_url": "https://api.github.com/users/RobinBoers/repos", "events_url": "https://api.github.com/users/RobinBoers/events{/privacy}", "received_events_url": "https://api.github.com/users/RobinBoers/received_events", "type": "User", "site_admin": false }, "html_url": "https://github.com/RobinBoers/BloggerAPP", "description": "Webapp to manage, create and publish blogposts, using blogspot", "fork": false, "url": "https://api.github.com/repos/RobinBoers/BloggerAPP", "forks_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/forks", "keys_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/keys{/key_id}", "collaborators_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/collaborators{/collaborator}", "teams_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/teams", "hooks_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/hooks", "issue_events_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/issues/events{/number}", "events_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/events", "assignees_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/assignees{/user}", "branches_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/branches{/branch}", "tags_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/tags", "blobs_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/git/blobs{/sha}", "git_tags_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/git/tags{/sha}", "git_refs_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/git/refs{/sha}", "trees_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/git/trees{/sha}", "statuses_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/statuses/{sha}", "languages_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/languages", "stargazers_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/stargazers", "contributors_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/contributors", "subscribers_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/subscribers", "subscription_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/subscription", "commits_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/commits{/sha}", "git_commits_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/git/commits{/sha}", "comments_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/comments{/number}", "issue_comment_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/issues/comments{/number}", "contents_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/contents/{+path}", "compare_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/compare/{base}...{head}", "merges_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/merges", "archive_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/{archive_format}{/ref}", "downloads_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/downloads", "issues_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/issues{/number}", "pulls_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/pulls{/number}", "milestones_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/milestones{/number}", "notifications_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/notifications{?since,all,participating}", "labels_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/labels{/name}", "releases_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/releases{/id}", "deployments_url": "https://api.github.com/repos/RobinBoers/BloggerAPP/deployments", "created_at": "2020-01-25T17:59:36Z", "updated_at": "2020-05-28T12:13:53Z", "pushed_at": "2020-01-26T16:58:55Z", "git_url": "git://github.com/RobinBoers/BloggerAPP.git", "ssh_url": "git@github.com:RobinBoers/BloggerAPP.git", "clone_url": "https://github.com/RobinBoers/BloggerAPP.git", "svn_url": "https://github.com/RobinBoers/BloggerAPP", "homepage": "http://code.geheimesite.nl/beta/bloggr", "size": 4325, "stargazers_count": 2, "watchers_count": 2, "language": "PHP", "has_issues": true, "has_projects": true, "has_downloads": true, "has_wiki": true, "has_pages": false, "forks_count": 1, "mirror_url": null, "archived": false, "disabled": false, "open_issues_count": 0, "license": null, "forks": 1, "open_issues": 0, "watchers": 2, "default_branch": "master" }, { "id": 277351770, "node_id": "MDEwOlJlcG9zaXRvcnkyNzczNTE3NzA=", "name": "Bloggr_Letter_Correcter", "full_name": "RobinBoers/Bloggr_Letter_Correcter", "private": false, "owner": { "login": "RobinBoers", "id": 60298132, "node_id": "MDQ6VXNlcjYwMjk4MTMy", "avatar_url": "https://avatars.githubusercontent.com/u/60298132?v=4", "gravatar_id": "", "url": "https://api.github.com/users/RobinBoers", "html_url": "https://github.com/RobinBoers", "followers_url": "https://api.github.com/users/RobinBoers/followers", "following_url": "https://api.github.com/users/RobinBoers/following{/other_user}", "gists_url": "https://api.github.com/users/RobinBoers/gists{/gist_id}", "starred_url": "https://api.github.com/users/RobinBoers/starred{/owner}{/repo}", "subscriptions_url": "https://api.github.com/users/RobinBoers/subscriptions", "organizations_url": "https://api.github.com/users/RobinBoers/orgs", "repos_url": "https://api.github.com/users/RobinBoers/repos", "events_url": "https://api.github.com/users/RobinBoers/events{/privacy}", "received_events_url": "https://api.github.com/users/RobinBoers/received_events", "type": "User", "site_admin": false }, "html_url": "https://github.com/RobinBoers/Bloggr_Letter_Correcter", "description": "A App to make blogging in the new Blogger editor easy", "fork": false, "url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter", "forks_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/forks", "keys_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/keys{/key_id}", "collaborators_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/collaborators{/collaborator}", "teams_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/teams", "hooks_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/hooks", "issue_events_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/issues/events{/number}", "events_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/events", "assignees_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/assignees{/user}", "branches_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/branches{/branch}", "tags_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/tags", "blobs_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/git/blobs{/sha}", "git_tags_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/git/tags{/sha}", "git_refs_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/git/refs{/sha}", "trees_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/git/trees{/sha}", "statuses_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/statuses/{sha}", "languages_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/languages", "stargazers_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/stargazers", "contributors_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/contributors", "subscribers_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/subscribers", "subscription_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/subscription", "commits_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/commits{/sha}", "git_commits_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/git/commits{/sha}", "comments_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/comments{/number}", "issue_comment_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/issues/comments{/number}", "contents_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/contents/{+path}", "compare_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/compare/{base}...{head}", "merges_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/merges", "archive_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/{archive_format}{/ref}", "downloads_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/downloads", "issues_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/issues{/number}", "pulls_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/pulls{/number}", "milestones_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/milestones{/number}", "notifications_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/notifications{?since,all,participating}", "labels_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/labels{/name}", "releases_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/releases{/id}", "deployments_url": "https://api.github.com/repos/RobinBoers/Bloggr_Letter_Correcter/deployments", "created_at": "2020-07-05T17:33:39Z", "updated_at": "2021-01-24T12:10:56Z", "pushed_at": "2020-12-13T10:24:36Z", "git_url": "git://github.com/RobinBoers/Bloggr_Letter_Correcter.git", "ssh_url": "git@github.com:RobinBoers/Bloggr_Letter_Correcter.git", "clone_url": "https://github.com/RobinBoers/Bloggr_Letter_Correcter.git", "svn_url": "https://github.com/RobinBoers/Bloggr_Letter_Correcter", "homepage": null, "size": 72, "stargazers_count": 1, "watchers_count": 1, "language": "HTML", "has_issues": true, "has_projects": true, "has_downloads": true, "has_wiki": true, "has_pages": false, "forks_count": 0, "mirror_url": null, "archived": true, "disabled": false, "open_issues_count": 0, "license": null, "forks": 0, "open_issues": 0, "watchers": 1, "default_branch": "master" }, { "id": 320361409, "node_id": "MDEwOlJlcG9zaXRvcnkzMjAzNjE0MDk=", "name": "code.geheimesite.nl", "full_name": "RobinBoers/code.geheimesite.nl", "private": false, "owner": { "login": "RobinBoers", "id": 60298132, "node_id": "MDQ6VXNlcjYwMjk4MTMy", "avatar_url": "https://avatars.githubusercontent.com/u/60298132?v=4", "gravatar_id": "", "url": "https://api.github.com/users/RobinBoers", "html_url": "https://github.com/RobinBoers", "followers_url": "https://api.github.com/users/RobinBoers/followers", "following_url": "https://api.github.com/users/RobinBoers/following{/other_user}", "gists_url": "https://api.github.com/users/RobinBoers/gists{/gist_id}", "starred_url": "https://api.github.com/users/RobinBoers/starred{/owner}{/repo}", "subscriptions_url": "https://api.github.com/users/RobinBoers/subscriptions", "organizations_url": "https://api.github.com/users/RobinBoers/orgs", "repos_url": "https://api.github.com/users/RobinBoers/repos", "events_url": "https://api.github.com/users/RobinBoers/events{/privacy}", "received_events_url": "https://api.github.com/users/RobinBoers/received_events", "type": "User", "site_admin": false }, "html_url": "https://github.com/RobinBoers/code.geheimesite.nl", "description": "Website for my betaprojects", "fork": false, "url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl", "forks_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/forks", "keys_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/keys{/key_id}", "collaborators_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/collaborators{/collaborator}", "teams_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/teams", "hooks_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/hooks", "issue_events_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/issues/events{/number}", "events_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/events", "assignees_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/assignees{/user}", "branches_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/branches{/branch}", "tags_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/tags", "blobs_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/git/blobs{/sha}", "git_tags_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/git/tags{/sha}", "git_refs_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/git/refs{/sha}", "trees_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/git/trees{/sha}", "statuses_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/statuses/{sha}", "languages_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/languages", "stargazers_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/stargazers", "contributors_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/contributors", "subscribers_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/subscribers", "subscription_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/subscription", "commits_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/commits{/sha}", "git_commits_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/git/commits{/sha}", "comments_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/comments{/number}", "issue_comment_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/issues/comments{/number}", "contents_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/contents/{+path}", "compare_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/compare/{base}...{head}", "merges_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/merges", "archive_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/{archive_format}{/ref}", "downloads_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/downloads", "issues_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/issues{/number}", "pulls_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/pulls{/number}", "milestones_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/milestones{/number}", "notifications_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/notifications{?since,all,participating}", "labels_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/labels{/name}", "releases_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/releases{/id}", "deployments_url": "https://api.github.com/repos/RobinBoers/code.geheimesite.nl/deployments", "created_at": "2020-12-10T18:49:26Z", "updated_at": "2021-03-26T11:19:14Z", "pushed_at": "2021-03-26T11:19:11Z", "git_url": "git://github.com/RobinBoers/code.geheimesite.nl.git", "ssh_url": "git@github.com:RobinBoers/code.geheimesite.nl.git", "clone_url": "https://github.com/RobinBoers/code.geheimesite.nl.git", "svn_url": "https://github.com/RobinBoers/code.geheimesite.nl", "homepage": "https://code.geheimesite.nl", "size": 7953, "stargazers_count": 0, "watchers_count": 0, "language": "HTML", "has_issues": true, "has_projects": true, "has_downloads": true, "has_wiki": true, "has_pages": false, "forks_count": 0, "mirror_url": null, "archived": false, "disabled": false, "open_issues_count": 0, "license": null, "forks": 0, "open_issues": 0, "watchers": 0, "default_branch": "master" } ];
		} else return JSON.parse(Get("https://api.github.com/users/"+ username +"/repos?per_page=100"));
	}

	function getIssues(username, repo) {
		if(debugmode) {
			return [
					{
						"url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/issues/11",
						"repository_url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor",
						"labels_url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/issues/11/labels{/name}",
						"comments_url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/issues/11/comments",
						"events_url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/issues/11/events",
						"html_url": "https://github.com/RobinBoers/SkyLight-Website-Editor/issues/11",
						"id": 980053810,
						"node_id": "MDU6SXNzdWU5ODAwNTM4MTA=",
						"number": 11,
						"title": "Add options to edit new site settings (description, site language etc)",
						"user": {
						"login": "RobinBoers",
						"id": 60298132,
						"node_id": "MDQ6VXNlcjYwMjk4MTMy",
						"avatar_url": "https://avatars.githubusercontent.com/u/60298132?v=4",
						"gravatar_id": "",
						"url": "https://api.github.com/users/RobinBoers",
						"html_url": "https://github.com/RobinBoers",
						"followers_url": "https://api.github.com/users/RobinBoers/followers",
						"following_url": "https://api.github.com/users/RobinBoers/following{/other_user}",
						"gists_url": "https://api.github.com/users/RobinBoers/gists{/gist_id}",
						"starred_url": "https://api.github.com/users/RobinBoers/starred{/owner}{/repo}",
						"subscriptions_url": "https://api.github.com/users/RobinBoers/subscriptions",
						"organizations_url": "https://api.github.com/users/RobinBoers/orgs",
						"repos_url": "https://api.github.com/users/RobinBoers/repos",
						"events_url": "https://api.github.com/users/RobinBoers/events{/privacy}",
						"received_events_url": "https://api.github.com/users/RobinBoers/received_events",
						"type": "User",
						"site_admin": false
						},
						"labels": [
						{
							"id": 1863813033,
							"node_id": "MDU6TGFiZWwxODYzODEzMDMz",
							"url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/labels/bug",
							"name": "bug",
							"color": "d73a4a",
							"default": true,
							"description": "Something isn't working"
						}
						],
						"state": "closed",
						"locked": false,
						"assignee": null,
						"assignees": [],
						"milestone": null,
						"comments": 0,
						"created_at": "2021-08-26T09:52:46Z",
						"updated_at": "2021-08-26T09:52:46Z",
						"closed_at": null,
						"author_association": "OWNER",
						"active_lock_reason": null,
						"body": "Option to edit new site settings introduced in v0.04-beta (3659bf8)",
						"performed_via_github_app": null
					},
					{
						"url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/issues/10",
						"repository_url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor",
						"labels_url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/issues/10/labels{/name}",
						"comments_url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/issues/10/comments",
						"events_url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/issues/10/events",
						"html_url": "https://github.com/RobinBoers/SkyLight-Website-Editor/issues/10",
						"id": 980052102,
						"node_id": "MDU6SXNzdWU5ODAwNTIxMDI=",
						"number": 10,
						"title": "Add option to upload favicon",
						"user": {
						"login": "RobinBoers",
						"id": 60298132,
						"node_id": "MDQ6VXNlcjYwMjk4MTMy",
						"avatar_url": "https://avatars.githubusercontent.com/u/60298132?v=4",
						"gravatar_id": "",
						"url": "https://api.github.com/users/RobinBoers",
						"html_url": "https://github.com/RobinBoers",
						"followers_url": "https://api.github.com/users/RobinBoers/followers",
						"following_url": "https://api.github.com/users/RobinBoers/following{/other_user}",
						"gists_url": "https://api.github.com/users/RobinBoers/gists{/gist_id}",
						"starred_url": "https://api.github.com/users/RobinBoers/starred{/owner}{/repo}",
						"subscriptions_url": "https://api.github.com/users/RobinBoers/subscriptions",
						"organizations_url": "https://api.github.com/users/RobinBoers/orgs",
						"repos_url": "https://api.github.com/users/RobinBoers/repos",
						"events_url": "https://api.github.com/users/RobinBoers/events{/privacy}",
						"received_events_url": "https://api.github.com/users/RobinBoers/received_events",
						"type": "User",
						"site_admin": false
						},
						"labels": [
						{
							"id": 3236327221,
							"node_id": "MDU6TGFiZWwzMjM2MzI3MjIx",
							"url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/labels/feature%20request",
							"name": "feature request",
							"color": "d4c5f9",
							"default": false,
							"description": "Requested featues that could be implemented"
						}
						],
						"state": "open",
						"locked": false,
						"assignee": null,
						"assignees": [],
						"milestone": null,
						"comments": 0,
						"created_at": "2021-08-26T09:50:50Z",
						"updated_at": "2021-08-26T09:50:50Z",
						"closed_at": null,
						"author_association": "OWNER",
						"active_lock_reason": null,
						"body": null,
						"performed_via_github_app": null
					},
					{
						"url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/issues/9",
						"repository_url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor",
						"labels_url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/issues/9/labels{/name}",
						"comments_url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/issues/9/comments",
						"events_url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/issues/9/events",
						"html_url": "https://github.com/RobinBoers/SkyLight-Website-Editor/issues/9",
						"id": 980051447,
						"node_id": "MDU6SXNzdWU5ODAwNTE0NDc=",
						"number": 9,
						"title": "Generate clean HTML from Quill instead of copying from editor using JS",
						"user": {
						"login": "RobinBoers",
						"id": 60298132,
						"node_id": "MDQ6VXNlcjYwMjk4MTMy",
						"avatar_url": "https://avatars.githubusercontent.com/u/60298132?v=4",
						"gravatar_id": "",
						"url": "https://api.github.com/users/RobinBoers",
						"html_url": "https://github.com/RobinBoers",
						"followers_url": "https://api.github.com/users/RobinBoers/followers",
						"following_url": "https://api.github.com/users/RobinBoers/following{/other_user}",
						"gists_url": "https://api.github.com/users/RobinBoers/gists{/gist_id}",
						"starred_url": "https://api.github.com/users/RobinBoers/starred{/owner}{/repo}",
						"subscriptions_url": "https://api.github.com/users/RobinBoers/subscriptions",
						"organizations_url": "https://api.github.com/users/RobinBoers/orgs",
						"repos_url": "https://api.github.com/users/RobinBoers/repos",
						"events_url": "https://api.github.com/users/RobinBoers/events{/privacy}",
						"received_events_url": "https://api.github.com/users/RobinBoers/received_events",
						"type": "User",
						"site_admin": false
						},
						"labels": [
						{
							"id": 1863813036,
							"node_id": "MDU6TGFiZWwxODYzODEzMDM2",
							"url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/labels/enhancement",
							"name": "enhancement",
							"color": "a2eeef",
							"default": true,
							"description": "New feature or request"
						}
						],
						"state": "open",
						"locked": false,
						"assignee": null,
						"assignees": [],
						"milestone": null,
						"comments": 0,
						"created_at": "2021-08-26T09:50:04Z",
						"updated_at": "2021-08-26T09:50:04Z",
						"closed_at": null,
						"author_association": "OWNER",
						"active_lock_reason": null,
						"body": "Currently, when writing a blogpost, I get output from Quill by copying the HTML from the editor area.\r\n\r\nQuill outputs clean JSON, which we can parse to get clean HTML instead of the hack I currently implemented :)",
						"performed_via_github_app": null
					},
					{
						"url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/issues/8",
						"repository_url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor",
						"labels_url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/issues/8/labels{/name}",
						"comments_url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/issues/8/comments",
						"events_url": "https://api.github.com/repos/RobinBoers/SkyLight-Website-Editor/issues/8/events",
						"html_url": "https://github.com/RobinBoers/SkyLight-Website-Editor/issues/8",
						"id": 974561767,
						"node_id": "MDU6SXNzdWU5NzQ1NjE3Njc=",
						"number": 8,
						"title": "Add site language to lang attribute HTML",
						"user": {
						"login": "RobinBoers",
						"id": 60298132,
						"node_id": "MDQ6VXNlcjYwMjk4MTMy",
						"avatar_url": "https://avatars.githubusercontent.com/u/60298132?v=4",
						"gravatar_id": "",
						"url": "https://api.github.com/users/RobinBoers",
						"html_url": "https://github.com/RobinBoers",
						"followers_url": "https://api.github.com/users/RobinBoers/followers",
						"following_url": "https://api.github.com/users/RobinBoers/following{/other_user}",
						"gists_url": "https://api.github.com/users/RobinBoers/gists{/gist_id}",
						"starred_url": "https://api.github.com/users/RobinBoers/starred{/owner}{/repo}",
						"subscriptions_url": "https://api.github.com/users/RobinBoers/subscriptions",
						"organizations_url": "https://api.github.com/users/RobinBoers/orgs",
						"repos_url": "https://api.github.com/users/RobinBoers/repos",
						"events_url": "https://api.github.com/users/RobinBoers/events{/privacy}",
						"received_events_url": "https://api.github.com/users/RobinBoers/received_events",
						"type": "User",
						"site_admin": false
						},
						"labels": [],
						"state": "open",
						"locked": false,
						"assignee": null,
						"assignees": [],
						"milestone": null,
						"comments": 0,
						"created_at": "2021-08-19T11:25:43Z",
						"updated_at": "2021-08-19T11:25:43Z",
						"closed_at": null,
						"author_association": "OWNER",
						"active_lock_reason": null,
						"body": "Add the site language from siteinformation.php to the lang attribute in the HTML for the default themes",
						"performed_via_github_app": null
					}
					];
		} else return JSON.parse(Get("https://api.github.com/repos/"+username+"/"+repo+"/issues?per_page=100&state=all"));
	}

	// Manage recents
	function addItemToRecents(item) {
		recents = [item, ...recents];
		recents.length = 5;
 		localStorage.setItem('recents', JSON.stringify(recents));
	}
	function inRecents(item) {
		let isInRecents = false;
		
		for(let i = 0;i<recents.length;i++) {
			if(recents[i] == item) isInRecents = true;
		}

		return isInRecents;
	}
	function putAtTopOfRecents(item) {

		// Remove from recents
		for(let i = 0;i<recents.length;i++) {
			for(let i = 0;i<recents.length;i++) {
				if(recents[i] == item) recents.splice(i, 1);
			}
		}

		// Put back at the top
		addItemToRecents(item);
	}

	// Select repositorie to edit
	function selectRepo(repo) {

		if(!repo) repo = newRecent;

		if(!inRecents(repo)) addItemToRecents(repo);
		else putAtTopOfRecents(repo);

		currentProject = repo;
		
		issues = getIssues(username, repo);
		if(issues.message) {
			errorMessage = issues.message;
			issues = null;
		}

		console.log(issues)

		projectLayout = true;

		if(issues !== null) {
			for(let i =0;i<issues.length;i++) {
				clickedIssues[i] = false;
			}
		}

	}

	function getURL(repo) {
		let link = "about:blank";
		repos.forEach((val, i) => {
			console.log(val);
			if(val.name === repo) link = val.html_url;
		});

		return link;
	}

	function clickIssue(issue) {
		for(let i =0;i<issues.length;i++) {
			if(issues[i] === issue) clickedIssues[i] = !clickedIssues[i];
			else clickedIssues[i] = false; // disable this to click multiple issues at onece
		}
	}

</script>

<main>
	{#if repos !== null && issues !== null}

		{#if projectLayout === false}

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

			<form on:submit|preventDefault={() => selectRepo()}>
				<select bind:value={newRecent}>
					{#each repos as repo}
						{#if repo.has_issues === true && repo.archived !== true && repo.disabled !== true} 
							{#if repo.open_issues_count > 0 || showNoOpen}
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
					<input bind:checked={showNoOpen} type="checkbox" id="noOpen" name="noOpen">
					&nbsp;Show repositories with 0 open issues
				</label>
			</form>
		
		{:else}

			<h1>{currentProject}</h1>

			<button on:click={() => {projectLayout = false}}><i class="fas fa-arrow-left"></i> Back</button>
			<button on:click={() => {window.location = getURL(currentProject)+"/issues/"}}><i class="fab fa-github"></i> View on GitHub</button>



			<button on:click={() => {showFinished = !showFinished}}>

				{#if showFinished}
					<i class="fas fa-eye-slash"></i> Hide finished
				{:else}
					<i class="far fa-eye-slash"></i> Show finished 
				{/if}
			
			</button>



			<button on:click={() => {window.location = getURL(currentProject)+"/issues/new"}}  class="right"><i class="fas fa-plus"></i> New</button>

			{#each issues as item, i}
							
				{#if item !== null && item !== ""}

					{#if item.state === "open" || showFinished === true}

						{#if clickedIssues[i] === true}

							<li class="selected">
								<span on:click={clickIssue(item)} class="issue-head">
									<svg class="icon" viewBox="0 0 18 18" version="1.1" width="18" height="18" aria-hidden="true"><path d="M8 9.5a1.5 1.5 0 100-3 1.5 1.5 0 000 3z"></path><path fill-rule="evenodd" d="M8 0a8 8 0 100 16A8 8 0 008 0zM1.5 8a6.5 6.5 0 1113 0 6.5 6.5 0 01-13 0z"></path></svg>

									<span class="num">#{item.number}</span>
									{item.title}

									{#if item.state === "closed"}
										<i class="right">Finished</i>
									{/if}
								</span>
								<span class="issue-body">
									{#if item.body !== null} 
										{@html item.body}
									{:else}
										<i>Empty</i>
									{/if}
								</span>
							</li>

						{:else}

							<li on:click={clickIssue(item)} >
								<svg class="icon" viewBox="0 0 18 18" version="1.1" width="18" height="18" aria-hidden="true"><path d="M8 9.5a1.5 1.5 0 100-3 1.5 1.5 0 000 3z"></path><path fill-rule="evenodd" d="M8 0a8 8 0 100 16A8 8 0 008 0zM1.5 8a6.5 6.5 0 1113 0 6.5 6.5 0 01-13 0z"></path></svg>

								<span class="num">#{item.number}</span>
								{item.title}

								{#if item.state === "closed"}
										<i class="right">Finished</i>
								{/if}
							</li>

						{/if}

					{/if}
				{/if}

			{:else}
				<p>This project doesn't have any todos.</p>
			{/each}

		{/if}

	{:else} 

	<h2 class="select">Oops!</h2>

	<p>{errorMessage}</p>

	{/if}

	<footer>
		<p>Proudly built using Svelte.</p>
	</footer>
</main>
