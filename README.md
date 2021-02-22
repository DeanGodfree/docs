# Deans Docs

This is the source code to the documentation available on [github pages](https://deangodfree.github.io/docs/#/).
If you'd like to read the documentation, it's probably easiest to do it there.
If you find something you think is inaccurate, feel free to [create an issue](https://github.com/DeanGodfree/docs/issues/new).

## Contributing

If you would like to suggest an edit to the docs, feel free to submit a pull request.
You'll probably want to chat with us in our [MS Teams Channel](https://www.microsoft.com/en-gb/microsoft-teams/group-chat-software) first if it's a large change
to make sure we're in alignment.

The process is typically to create a branch, work on new content, push a commit, then open a pull request with @deangodfree as reviewer. When you are creating a brand new page, try to find a suitable slot for it in the nav sidebar; and create an entry for your new page in src/docs/\_sidebar.md. (Commit the \_sidebar.md edit along with your other content and submit a PR on the whole thing.)

You may consult [this page](https://deangodfree.github.io/docs/#/how-to-contribute) for detailed information on how best to submit content.

## Overview

Deans Docs is a static site built using Markdown files and powered by [Docsify][docsify].

### Requirements

- [node](https://nodejs.org)
- [nvm](http://nvm.sh)
- [yarn](https://yarnpkg.com)

### Developing Locally

The first time you run after cloning the repository to your machine, you need to do the following to bootstrap the build:
```bash
nvm install
yarn install
yarn build
yarn start
```

Thereafter, you can just run
```bash
nvm use 
yarn start
```

This will spin up a local instance of the docs at http://localhost:3000.

If you get an error like `node\r: No such file or directory` it's because docsify has DOS line endings, 
and you need to remove them with 

```bash
sed -i.bak s/$'\r'// node_modules/docsify-cli/bin/docsify
```

And don't forget to re-run `yarn install` any time you pull new code. 

### Submitting Changes

To submit changes, create a branch off main, add your commits, and create a pull request from your branch to master.
If the branch is in this repo (not a fork) and the name begins with `feature/` our build system will build it and let you know if it passed in the PR.
Once the PR is merged into main, it will be auto-deployed to https://deangodfree.github.io/docs/#/ .

### Formatting conventions

In general, try to keep everything as simple as possible.
Use heading 1s (`# Title`) for the page title, then heading 2s (`## Title`) for major sections, section 3s for subsections and so on.
Don't choose headings based on the font size.

Separate sentences with a single carriage return.
When rendered this will just put a single space between the sentences.
Keeping sentences on separate lines helps to keep the markdown easily viewable without paragraphs running way off the screen.
For an actual paragraph break, separate with two carriage returns.

#### How to add important content or general tip snippets.

See the [docsify documentation](https://docsify.js.org/#/helpers) for the available helpers.
Our conventions for this repo are as follows:

- `>` is used for generally helpful hints and tips.
- `?>` is used for more important hints and tips.
While `>` notes could probably be skipped over by the reader and they'd still be successful, we expect they need to read the `?>` notes.
- `!>` is used for warnings about deprecated or otherwise problematic "land mines" the user should stay away from.


#### How to add code examples

Note the code type distinction after the 3 backticks.  It can be any of the following codes:

- graphql
- json
- javascript
- python
- bash
- http
- css
- html

```graphql
query {
  temporalDataObjects {
    records {
      id
      name
      description
      tasks {
        records {
          id
          name
          description
        }
      }
    }
  }
}
```

#### Using Tables

Tables are great for displaying multi-dimensional information.
Unfortunately, they're a bit of a pain to deal with in Markdown.
Don't try to line everything up perfectly in the markdown; just ensure you have all the right separators.
Line up the table headers and the line under them, and for the rows, just add separators where appropriate.

```markdown
| Parameter | Value |
| --------- | ----- |
| `preferredInputFormat` | `"text/plain"` |
| `supportedInputFormats` | `["text/plain"]` |
| `engineMode` | `"chunk"` |
```

#### Advanced Formatting

If needed, Markdown does support using HTML directly inside of it, but try to avoid it wherever possible.
For example, don't sprinkle around a bunch of `<br>` tags just to get more spacing; let the site handle the formatting for you.
If we start to see that we need extra padding after h3s for example, we can apply it globally in the future.

If there is an advanced feature that you want added to lots of different places, consider building a plugin to render it based on very simple markdown (e.g. )
See the [docsify documentation](https://docsify.js.org/#/helpers) for the available helpers.
Our conventions for this repo are as follows:

### How to add a new link to the side bar

To add a new link to the sidebar, please add a new entry to the [_sidebar.md file](docs/_sidebar.md).

### How to add a new child link to an existing side bar link

To add a child link to the sidebar, navigate to the child folder and update the `_sidebar.md` file to include the child link.

### Useful Resources

- [Markdown Cheatsheet][markdown-cheat]
- [Docsify Docs][docsify]

## Testing

There is a suite of end-to-end tests at [test/e2e](test/e2e).
They are written using [CodeceptJS with Puppeteer](https://codecept.io/puppeteer).
To add a test file, just add any file under the test/e2e with `.test.js` at the end of it.

The test suite is run automatically as part of the Jenkins and Docker builds.
The test suite is also run as a git commit hook.
This ensures that you cannot commit unless tests are passing.

To quickly run the test suite manually while you already have a docs instance running on port 3000 (via `yarn start`)
you can run `yarn test:only` in another console.

### JUnit Test Results

All the test scripts are configured to output basic information to stdout and to also write a JUnit test result report at `test-results.xml`.
The JUnit results should then be able to be visualized in CI pipelines like Jenkins or other tools.

### Pretty Test Results

To generate a nice pretty interactive report of test results, you can run `yarn test`.
It will run the full test suite in a way that generates detailed results and then open a UI called [Allure](http://allure.qatools.ru/) to view those results in an interactive web report.

> Allure requires Java to be installed

## Docker Test

To test the Docker build locally, you can do the following:

```bash
# First, connect to VPN
# Export github access token
export GITHUB_ACCESS_TOKEN=redacted

# Build
docker build --build-arg GITHUB_ACCESS_TOKEN=$GITHUB_ACCESS_TOKEN --build-arg ENVIRONMENT=dev -t docs .

# Run
docker run -it --rm -p 9000:9000 docs:latest
```

This is for local testing only.  Production builds happen through Jenkins.

[docsify]: https://docsify.js.org/#/?id=docsify
[markdown-cheat]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
