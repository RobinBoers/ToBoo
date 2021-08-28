# To-Boo

To-Boo is a simple todo app to keep track of your GitHub issues. I made it for myself to experiment with JavaScript frameworks. I use the GitHub issues as a todo list with things I want to do for specific projects. I made this so I can have a simple overview of all my todos at once. It connects via the GitHub REST API, so doesn't need a API key and stuff.

[Live demo (using my account)](https://robinboers.github.io/ToBoo/)

## Development

Clone the git repo:

```
git clone https://github.com/RobinBoers/ToBoo
```

Install dependencies:

```
npm install
```

Run live server to test:

```
npm run dev
```

To build for production:

```
npm run build
```

## Configuration

You can configure three options:

- username (the account to pull repos and issues from)
- showFinished (wether or not the closed issues should be visible by default)
- debugmode (if turned on, it will use demo data to prevent going above the API rate limit)
- showNoOpen (if turned on, it will show repositories with no open issues by default)

![Screenshot](screenshot.png)