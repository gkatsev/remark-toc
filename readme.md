# mdast-toc [![Build Status](https://img.shields.io/travis/wooorm/mdast-toc.svg?style=flat)](https://travis-ci.org/wooorm/mdast-toc) [![Coverage Status](https://img.shields.io/coveralls/wooorm/mdast-toc.svg?style=flat)](https://coveralls.io/r/wooorm/mdast-toc?branch=master)

Generate a Table of Contents (TOC) for [Markdown](http://daringfireball.net/projects/markdown/syntax)
files with [mdast](https://github.com/wooorm/mdast).

## Installation

[npm](https://docs.npmjs.com/cli/install):

```bash
npm install mdast-toc
```

[Component.js](https://github.com/componentjs/component):

```bash
component install wooorm/mdast-toc
```

[Bower](http://bower.io/#install-packages):

```bash
bower install mdast-toc
```

[Duo](http://duojs.org/#getting-started):

```javascript
var toc = require('wooorm/mdast-toc');
```

UMD (globals/AMD/CommonJS) ([uncompressed](mdast-toc.js) and [compressed](mdast-toc.min.js)):

```html
<script src="path/to/mdast.js"></script>
<script src="path/to/mdast-toc.js"></script>
<script>
  mdast.use(mdastTOC);
</script>
```

## Table of Contents

*   [Usage](#usage)

*   [API](#api)

    *   [mdast.use(toc, options)](#mdastusetoc-options)

*   [License](#license)

## Usage

Require/read dependencies:

```javascript
var toc = require('mdast-toc');
var fs = require('fs');
var mdast = require('mdast').use(toc);
var readme = fs.readFileSync('readme.md', 'utf-8');
```

Parse markdown (this TOC is the 14th child).

```javascript
var contents = mdast.run(mdast.parse(readme)).children[14];
```

Stringify:

```javascript
var doc = mdast.stringify(contents);
```

Yields:

```markdown
-   [Usage](#usage)

-   [API](#api)

    -   [mdast.use(toc, options)](#mdastusetoc-options)

-   [License](#license)
```

## API

### [mdast](https://github.com/wooorm/mdast#api).[use](https://github.com/wooorm/mdast#mdastuseplugin-options)(toc, options)

Adds a [Table of Contents](#table-of-contents) to a Markdown document.

*   Looks for the first heading containing `"Table of Contents"`, `"toc"`,
    or `table-of-contents` (case insensitive, supports alt/title attributes
    for links and images too);

*   Removes all following contents until an equal or higher heading is found;

*   Inserts a list representation of the hierarchy of following headings;

*   Adds links to following headings, using the same slugs as GitHub.

**Signatures**

*   `mdast.use(toc, options?)`.

**Parameters**

*   `toc` — This plugin;

*   `options` (`Object?`) — Settings:

    *   `library` (`string?` or `Function?`, default: `"github"`):

        *   `"github"` — Slugs just like GitHub;

        *   `"npm"`
            — Slugs just like npm (but npm doesn’t support links in headings,
            [yet](https://github.com/npm/marky-markdown/pull/38));

        *   `string` (e.g., `"slug"`, `"slugg"`)
            — Library to require (not in the browser);

        *   `Function` (e.g., `require("slugg")"`)
            — Library to use.

    *   `heading` (`string?`, default: `"toc|table[ -]of[ -]contents?"`)
        — heading to look for, wrapped in
        `new RegExp('^(' + value + ')$', 'i');`.

## License

[MIT](LICENSE) © [Titus Wormer](http://wooorm.com)