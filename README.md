## jist

jist is a little python script for working with multi-file, multi-directory
private [gists](https://gist.github.com).

[Blog post describing jist](http://charlesleifer.com/blog/jist-a-command-line-utility-for-managing-multi-file-multi-directory-private-gists/).

### Configuring an API token

In order to be able to create new gists from the command-line, we need to use an API token. GitHub makes this very easy to do, so I will walk you through the steps.

First log in to your github account and click the wrench/screwdriver icon to navigate to your account settings. In the account settings page, click the *Applications* tab on the left-hand navigation. Then select the *Generate new token* button:

![](http://media.charlesleifer.com/blog/photos/thumbnails/github-applications-page_800x800.png)

You will come to a page where you can configure permissions for your new API token. For our purposes we only need permission to create gists, so select the *Gist* checkbox:

![](http://media.charlesleifer.com/blog/photos/thumbnails/s1401674187.6_800x800.png)

Give your new token a name and save. You will be taken to a page where you can copy your new token. **Do not lose this token** since this is the only time you will be able to view it:

![](http://media.charlesleifer.com/blog/photos/thumbnails/s1401674140.76_800x800_800x800.png)

To configure `jist` to use your access token, run the following commands:

```
git config --global jist.user my_github_username
git config --global jist.token my_github_api_token
```

## Usage

The basic workflow consists of 3 commands, `clone`, `init` and `push`.

#### clone

Clone a private gist with the given ID. Any flattened directories
will be expanded.

    jist clone [gist id] [optional: path/for/code]

#### init

Initialize a Git repo and create a new Gist.

    jist init [optional: path/to/files] [optional: gist description]

#### push

Commit and push changes to GitHub. Any directories will be flattened
before commiting and pushing, then re-expanded afterwards.

    jist push [optional: path/to/code]

#### commit

Commit changes to current working directory.

    jist commit

### Additional commands

#### expand

Expand flattened files into directories. For example `foo___bar.js`
would be expanded to `foo/bar.js`. If no path is specified, command
will run in the current working directory.

    jist expand [optional: path/to/expand]

#### flatten

Flatten all directories, renaming files so the directories can be
reconstructed using `expand`.

    jist flatten [optional: path/to/files]

#### help

Print available commands.

#### pull

Update local checkout with the latest changes from GitHub. Execute
this command from within the repository's root directory.

    jist pull
