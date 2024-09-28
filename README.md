# Welcome to github flow CI/CD example

The repo is an example of how CI/CD flow can work using simple github flow.  It easier to show how it works then tell so let's walk through some basic code scenerios.

### Enhancement

To add an enhancement to the code first create a new branch off of main for you feature branch.  Next commit changes to you branch that implement the feature.  For testing the could be just adding a simple test file to the repo.  When you think that your enhancement is ready open a PR with your branch.  Make sure that you label the PR an enhancement and that it's title is descriptive.  This will be used in the auto-generate release notes later.

As you will see the automated test ran and the checks passed.  In a real project we should have linting, test, and test coverage reports to ensure safe continuous code integration.  

Each enhancement should be ready for production on merge.  This might require using feature, versioned end points, or other defensive coding measures.

### Release to Dev

Now that the enhancement is feature complete and the tests have passed we are ready to incorporate it into the code.  Merge the PR.  Squash and merging will reduce all of the commits on the PR to a single commit on main.  This can be more legible in the future.

After tthe merge the code auto-deploys to the dev environment.  You can click on the actions to see that it ran.

### Release to QA

Now that we've incorporated the code we are ready to prepare for a release.  Follow the steps below to setup a prerelease

- Click on releases from the main page of the repo
- Click draft new release
- Create a tag with the desired standard for this we can use the next semantic version such as v1.2
- Give the release a title
- Click prerelease on the bottom
- Generate Release Notes

As you might have notices the release notes get the title of the PR and are categorized by type.  

Now click publish release.  This will trigger a build of the project and a deploy to production.  From the release list in the repo click on the release you just created.  You'll notice there is a build.js attach to the release.  This can be any asset such as the build output of a react project.  By saving the asset to the release we can speed up the release when ready.

Go to the actions section and you'll see a build and deploy pre-release action waiting.  Click on the action.  QA is a protected ENV.  This means that the deployment action to QA requires an authorization.  Click review deployment add a comment and approve.  This will trigger the actual deployment to QA with a note of who approved the deployment.

### Release to production

Now that we've reviewed the hotfix and are ready to go to production we follow the same steps as above, but generate a release instead of a pre-release.  The release branch action deploys to production which has different users allowed to authorize the deployment.

### Hotfix

If have commited a new change to our main branch but need to apply a hotfix to production on the previous version.  Create a hotfix branch off the previous release (not prerelease).  Once this hotfix is complete we can create a release directly on the hotfix branch.  For instance if the last release was `1.0.0` we can create a `hotfix-1.0.1` branch and create a release on the last commit on that branch of `1.0.1`.  We can create a pre-release first if we want to force a deployment to QA.  After the hotfix is complete merge the hotfix branch back into main so that the changes are reflected in future releases

### New feature freeze

Say you want to do some exstensive QA test, but don't want to pause future test.  Create a pre-release at the time you are ready to start QA.  When a bug fix is needed create a fix branch off of the pre-release.  Once the feature is complete create a new pre-release on the last commit of the branch and merge the branch into main.

## Notes

This is just an example of a CI/CD flow with github flow.  Gitflow can be used without the continuous deployment and the continous deployment can be adjusted as desired.

#### Wins

- clear list of changes between releases
- ensure proper flow through environments
- clear log of deployment flow
- greatly reduced possibility of merge conflicts
- no need for separate dev and main branch
- reduced manual processes
- reduced chances for typo
- reduced time required for a code change
- faster deployment/rollback by prebuilding code
- deploy services and apps independently