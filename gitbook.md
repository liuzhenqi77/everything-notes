# Gitbook

## Init

Start a Gitbook project from the [website](https://www.gitbook.com).

## Credentials

Configure the credentials according to

[How can I use Git to update my book? · GitBook Help Center](https://help.gitbook.com/books/how-can-i-use-git.html)

## Working with repo

To clone the repo to local,

```bash
git clone https://git.gitbook.com/{{UserName}}/{{Book}}.git
```

The methods mentioned in the documentation can be used.

```bash
git remote add gitbook https://git.gitbook.com/{{UserName}}/{{Book}}.git
git push -u -f gitbook master
```

Of course it is possible to use an advanced IDE to simplify the process (of interacting with git).

## Debugging

Install new packages

```bash
gitbook install
```

Start local debugging

```bash
gitbook serve
```

## Example of `book.json`

```json
{
  "plugins": ["anchor-navigation-ex",
              "katex",
              "gist",
              "etoc",
              "splitter",
              "prism", "-highlight",
              "image-captions",
              "advanced-emoji",
              "search-pro", "-lunr", "-search"],
  "pluginsConfig": {
    "fontsettings": {
      "theme": "white",
      "family": "sans",
      "size": 1
    },
    "etoc": {
      "h2lb": 3,
      "header": 1,
      "mindepth": 2,
      "maxdepth": 4,
      "notoc": false
    },
    "anchor-navigation-ex": {
      "showLevel": false,
      "associatedWithSummary": false,
      "multipleH1": false,
      "mode": "float",
    "float": {
        "showLevelIcon": false,
        "level1Icon": "fa fa-hand-o-right",
        "level2Icon": "fa fa-hand-o-right",
        "level3Icon": "fa fa-hand-o-right"
      }
    }
  }
}
```

## Functions

Gitbook Official

[GitBook Help Center](https://help.gitbook.com)

[GitBook Toolchain Documentation](https://toolchain.gitbook.com)

Markdown

[markdown-guide 0.1 documentation](http://markdown-guide.readthedocs.io/en/latest/basics.html)

Code highlighting

[Prism](http://prismjs.com/)

Gist

use the package as follows:

```bash
{% gist id="https://gist.github.com/SamyPesse/6ceb8cb8d531ffab75f0" %}{% endgist %}

{% gist id="SamyPesse/6ceb8cb8d531ffab75f0" %}{% endgist %}

{% gist id="SamyPesse/6ceb8cb8d531ffab75f0",file="README.md" %}{% endgist %}

{% gist id="SamyPesse/6ceb8cb8d531ffab75f0",hideFooter=true %}{% endgist %}
```

Emoji

[emojify.js](https://github.com/emojione/emojify.js)

[Emoji cheat sheet for GitHub, Basecamp and other services](https://www.webpagefx.com/tools/emoji-cheat-sheet/)