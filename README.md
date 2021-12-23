# Updating a Readme (Page)

## Learning Goals

- Update the contents of a lesson in GitHub and Canvas
- Understand how to automate updates using GitHub actions

## Introduction

Now that we've **created** a repository in GitHub and the lesson in Canvas,
let's see how to make **updates** to the repository and have them reflected in
Canvas.

## Updating a Lesson Locally

We'll be working with the same repository as the previous lesson, so go ahead
and open it up in your text editor.

In your local repository, make an edit to the README.md file (whatever you want
to change is fine), and commit:

```console
$ git commit -am 'Fix typo in README'
```

To synchronize these changes with Canvas, we can use the github-to-canvas gem:

```console
$ github-to-canvas -a -lr
```

The `-a` flag is used to **align** changes from a local repository to Canvas.
This command uses the `.canvas` file from the repo to correctly associate the
repository with one or more lessons in Canvas, and push updates using the Canvas
API.

Head back to Canvas and open up the lesson. Refresh the page to see your change
reflected in Canvas.

While this workflow works, it can be easy to forget that last step of running
the github-to-canvas command after every change. Wouldn't it be nice if there
was a way to automate that?

## Automating Updates with GitHub Actions

Try this out. In your local repository, make an edit to the README.md file
(whatever you want to change is fine). This time, commit **and** push:

```console
$ git commit -am 'Fix typo in README'
$ git push
```

Now, open up the GitHub page for the repo in the browser and click the "Actions"
tab. You should see a workflow run with "Sync with Canvas" listed next to your
commit message. This indicates that GitHub is running the workflow defined in
the repo's `.github/workflows` folder based on your latest commit!

This workflow runs any time changes are made to the README.md file in either the
`main` or `master` branch of the repository, and uses the `github-to-canvas` gem
to sync changes to Canvas. It's the equivalent of running this command in your
local repository:

```console
$ github-to-canvas -a -lr --forkable
```

> **Note**: The `--forkable` command creates a "Fork" link in Canvas, but it
> only shows up for assignments (not pages). We include it in the GitHub action
> in all repos so that we can reuse the same action for all lessons, regardless
> of their type.

When the workflow finishes running, head back to Canvas and open up the lesson.
Refresh the page to see your change reflected in Canvas.

## Conclusion

Thanks to GitHub actions, we're able to focus or curriculum maintenance work on
simply making update to the GitHub repository and letting automation handle the
rest! As long as a lesson has:

- a well-formed `.canvas` file
- a GitHub action that uses the github-to-canvas gem

We can rely on this automation to simplify the curriculum maintenance process.
