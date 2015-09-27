# [TW5 2 Github pages](https://github.com/danielo515/TW5-auto-publish2gh-pages)

This repository is both a template and a set of instructions to host a TiddlyWiki5 on your own Github pages repository. The wiki will be automatically rebuilt each time the Github repository changes.

# Requirements
The list of pre-requisites is small:

- [Git](http://git-scm.com/download) installed on your workstation
- A [Github](https://github.com) account
- A [Travis-ci](https://travis-ci.org/ "go to travis site") account

# Preparation
These steps are required before setting up your first TW5 on Github pages:
### Create a Github token

We need to create a `Personal access token` to allow the scripts on Travis-ci to push to the managed Github account. This token needs to be created only once, as the same token may be used on Travis-ci for multiple managed repositories.

- Go to [Github's tokens management page](https://github.com/settings/tokens)
- Create a new token clicking on `Generate new token`
- Provide a meaningful token description -- this will be the only clue to identify the token usage.
- Make sure `repo` and `public_repo` options are selected
- Click on `Generate token`. Here is an overview of this step:
![Generate token](/../screenshots/github-token.png?raw=true)
- Github will generate an unique token -- copy this token now and save it somewhere safe as you will not have another opportunity

### Clone the codebase

We need make a clone of the required codebase -- we will later push this to each Github repository we intend to use for hosting a TW5 wiki.

- Open a terminal and  enter the following to create your clone of the codebase:
- `$ git clone --bare https://github.com/danielo515/TW5-auto-publish2gh-pages`
- Move into the newly created directory containing the codebase:
- `$cd TW5-auto-publish2gh-pages.git`

We are now set to create our first wiki.

# Creating a wiki

- Go to your [Github](https://github.com) account and create new repositories to host your wikis (choose an appropriate name for each repository, reflecting the contents of your new wiki.) For the purposes of these instructions we will be creating three new wikis named "wiki1", "wiki2" and "wiki3".
- Go to [Travis-ci](https://travis-ci.org/ "go to travis site") and sign in using your Github account (on first use, authorise the application to access your Github account)
- You will be directed to your dashboard; on the left side of your dashboard you should have a list of the repositories under Travis management (on first access this list should be empty)
- Click the plus sign next to `My Repositories` to bring the new repositories into Travis management; you should be redirected to your profile:
![Add Repository](/../screenshots/Travis-CI_addRepo.png?raw=true "Add repo")

We are now going to place each of the new repositories under Travis management and prepare them for Travis to auto-build each time we commit a change to Github

- Locate "wiki1" and activate the "switch" to put it under Travis management. 
- If you don't find the repository you are looking for, click the `Sync` button to refresh the list of repositories:
![Add Repository](/../screenshots/Travis-CI_sync.png?raw=true "Add repo")
- In our example we are activating this Github repository:
![Activate Repository](/../screenshots/Travis-CI_activate.png?raw=true)
- Setup the global variables required by our build scripts
- Click on the gear icon adjacent the 'Activate' switch of "wiki1"
- ![config Repository](/../screenshots/Travis-CI_config.png?raw=true)
- You should be redirected to the 'Settings' page of "wiki1"
- Leave the General settings as they are by default.
- Add the required variables in the 'Variables' section:

1. First enter `GH_REF`
2. The value for `GH_REF` must reflect the url of your forked repository without the `https` prefix and with a `.git` extension (copy this from the relevant Github repository)
3. For this variable you may set to `on` the `Display value in build log` (this enables display of the linked repository for future reference)
4. Click add
5. Follow the same process to add the `GH_TOKEN` variable, but this time make sure that `Display value in build log` is set to off for security reasons. Paste here the Github token we have generated previously:
    ![Token variable](/../screenshots/Travis-CI_GH_TOKEN.png?raw=true)
6. Repeat this process to add `GH_EMAIL` variable. This should be the email you have used to register your account on Github. After this process you should see something like this:
    ![Variables Setup](/../screenshots/Travis-CI_Variables.png?raw=true)
        
Changes are saved automatically; at this point we are done with configuring wiki1 and should repeat the above steps for each of wiki2 and wiki3
    
Now push a copy go the codebase to each of your new Github wikis -- this will also trigger the first build from Travis

- `$ git push --mirror https://github.com/username/wiki1`
- `$ git push --mirror https://github.com/username/wiki2`
- `$ git push --mirror https://github.com/username/wiki3`
- The build process happens each time you push a change to your repository (and not before.) An ongoing build looks like this:
![Building](/../screenshots/Travis-CI_Building.png?raw=true)
- Once the build has finished - you may visit your new wikis at either `<your-git-username>.github.io/wiki1` or `<your-git-username>.github.io/wiki2` or  `<your-git-username>.github.io/wiki3`

You are now set to go: 

- You may now edit any file in your Github repositories and your new wiki will be re-built as soon as these changes are pushed
- This may be done directly on Github, or you may prefer using your favourite editor before pushing the changes to Github with git, or you may edit your pages using a web client such as [Prose](#Prose)
- Remember - the first build of each wiki will only occur after you have committed an edit to the respective Github repository and will, therefore, not be available on Github pages before that 

## Prose
- Visit [Prose](http://prose.io/); on first use you will need to authorise Prose to access your Github account
- Once authorised, you may begin using the application to edit your tiddlers:

1. Select the repository of your wiki
2. Navigate to `wiki`>`tiddlers` directory
3. Select the tiddler you want to edit or create a new file. When creating a new file make sure to give it a `.tid` extension.
4. Once you  have completed editing your tiddler, click the save icon. You can provide a commit message if you want.
5. Click on `IMPORT FROM` 
6. On the drop down select `Github`
7. Authorise the application if needed
8. Select the repository you want to edit, and select the master branch
9. Navigate to `wiki`>`tiddlers` directory
10. Select the tiddler you want to edit
11. Once you  have your "tiddler ready" click `SAVE TO` and select Github
