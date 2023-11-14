# CASE IQ - Upgrading an Application

Helpful Tips:

It is helpful to know whether you are doing a major version upgrade, a patch upgrade, or perhaps multiple upgrades. We can find this out by going to Confluence and looking up the release notes for the version we are upgrading to

![Screen Shot 2023-11-14 at 1 28 27 PM](https://github.com/CExKForsyth/kyle_notes/assets/95767293/e5bce4b3-8413-4e67-bee9-977eb9335baf)

From the these Release Notes, we can found out all sorts of information about the version we're upgrading to. Take some time to peruse the page to find out more about what changes are being made.

![Screen Shot 2023-11-14 at 1 29 02 PM](https://github.com/CExKForsyth/kyle_notes/assets/95767293/16e4a9d0-06d4-4c3f-8941-a9e821c864fd)

On the left side of the page you will see Release Notes listed for different versions. These are the MAJOR releases. If we are upgrading from a Major Release to another, we need to ensure that we are taking careful precautions to read the Release Notes and usually when doing these upgrades we have to run `make p-release-upgrade` when deploying to Jenkins. To find out exactly what needs to be done on the development side, scroll to the bottom of the release notes on Confluence, and you'll find a link to the platform [RELEASE_UPGRADE.md](https://github.com/i-Sight/isight_main_v5_beta/blob/bba2f365536cfc8b22b013215526866631520975/RELEASE_UPGRADE.md) on Github.

Here we can find specific instructions on changes that may need to be made to our projects when upgrading to this version, especially things that may be considered edge-cases, commonly customized features in our config repos, Environment Variables that may have changed, become defunct, or that may be newly required.
![Screen Shot 2023-11-14 at 1 35 40 PM](https://github.com/CExKForsyth/kyle_notes/assets/95767293/3daf4691-a7cc-4f7a-9371-b0df1aaa4548)

For the sake of this document, I will walk through upgrading a project from `v9.0.3` to `v9.1.0`

## Step 1: Set up your project locally. 

If you haven't already, create a directory in your local machine where you can store this project. 

The project I'm using as an example is called Farmers, so I would create a directory called `farmers-project`

Clone the [`isight_main` repository](https://github.com/i-Sight/isight_main_v5_beta) and the [project config repository](https://github.com/i-Sight/config_FARMER00_v5) both into this new directory. 

Update your bash_profile variables `PLATFORM_PATH` and `APP_CONFIG_PATH` to point to these respective directories.

Run `. ~/.bash_profile` in your terminal to refresh these bash variables. 

Set up this project locally as you normally would. Ensure that you checkout the starting version in your platform. In this case I would checkout `v9.0.3`. We haven't upgraded any of our files yet to `v9.1.0`, so do not worry about the version that we are upgrading to just yet. 

Once you have the project set up locally. Test it out, ensure it has set up and is functioning as expected. Run the project in your browser, and navigate to the /Settings/System/About page to check that the correct version is indeed displaying. 

![Screen Shot 2023-11-14 at 1 46 42 PM](https://github.com/CExKForsyth/kyle_notes/assets/95767293/b20a90b2-f4a2-4737-aaaa-2fc10bbcbf1b)

## Step 2: Make the Config Changes.

Now we need to make all the necessary changes to our config files. These changes can be found by navigating to the [config_base_v5](https://github.com/i-Sight/config_base_v5/compare) project on GitHub, and running a compare between the version we are starting from, and the version we are upgrading to.

For the `base:` -> Set it to the version the application is currently on.
For the `compare` -> Set it to the version we are upgrading to.

Like so:

![Screen Shot 2023-11-14 at 1 50 51 PM](https://github.com/CExKForsyth/kyle_notes/assets/95767293/59983d51-a21e-4a70-b615-b43eef9172d8)

Then click the `Files Changed` tab. All of the file changes you see here are what we need to complete in our local project, in our code editor. 

Create a new branch in your terminal, and name the branch the same name as the [Upgrade Ticket](https://caseiq.atlassian.net/browse/FIER-6?focusedCommentId=820847) in Jira. So I would name my branch `FIER-6`.

In this branch, make all the changes seen on that [compare page](https://github.com/i-Sight/config_base_v5/compare/v9.0.3...v9.1.0)

When you get to the package.json changes. Do not change the version # to match what's shown. The version can be left as is. Also, instead of manually editing any dependencies in the package.json, just run the code outlined in the [RELEASE_UPGRADE.md](https://github.com/i-Sight/isight_main_v5_beta/blob/v9.1.0/RELEASE_UPGRADE.md). It will be something like this:
`yarn upgrade isight@git+ssh://git@github.com/i-Sight/isight_main_v5_beta#v9.1.0`

## Step 3: Once all changes have been made, it is good to reference the [RELEASE_UPGRADE.md](https://github.com/i-Sight/isight_main_v5_beta/blob/v9.1.0/RELEASE_UPGRADE.md) document once again.

This time we are looking for any changes mentioned that maybe were not included in the config compare file. Read through this document. 

** Also, if the project you are working on is large, and heavily-customized, you may need to look through the config for files that have been overwritten from platform, and compare it to the [platform compare changes](https://github.com/i-Sight/isight_main_v5_beta/compare/v9.0.3...v9.1.0). Of course you don't need to scroll through all 1195+ files.. but anything overwritten in the config, or in the `webpack-overrides` file of your config, should be double checked to ensure that the upgrade won't be breaking previously built custom features.

Another thing to do while reading through the [RELEASE_UPGRADE.md](https://github.com/i-Sight/isight_main_v5_beta/blob/v9.1.0/RELEASE_UPGRADE.md) is ensure that any altered or new ENV variables are accounted for. If some are optional, ask the BA listed on your Upgrade Ticket whether the client will be requiring those features. We can test these new variables by adding them into our `bash_profile`. 

## Step 4: Test Locally

Now that we've made all of our changes for the upgrade, and added any Environment Variables that may be needed to our bash_profile, and run `. ~/.bash_profile` to refresh those variables, we are ready to test the upgrade locally. 

`CTRL + C` in your terminal to stop your server if it's running. ** Do not run `make breakdown` if you don't have to. It's best to test this upgrade without breaking down the environment, as we are assuming that we will not be breaking down the app when we deploy the upgrade either.

![Screen Shot 2023-11-14 at 2 13 55 PM](https://github.com/CExKForsyth/kyle_notes/assets/95767293/df72f3b4-5ae9-4949-9b21-573f19dc40c7)

In your terminal window that has `.../farmers-project/config_FARMER00_v5` open, run `yarn unlink isight`.

![Screen Shot 2023-11-14 at 2 14 16 PM](https://github.com/CExKForsyth/kyle_notes/assets/95767293/ef17e8eb-a81e-473e-91da-26774830e786)

Navigate to your terminal that has the `.../farmers-project/isight_main_v5_beta` directory open and run `yarn unlink`.
In this same terminal, run `git checkout tags/v9.1.0` (or whatever version you're upgrading to)
Run `nvm use`
Next run `yarn install --frozen-lockfile`

Once that's done, run: `yarn link`

![Screen Shot 2023-11-14 at 2 13 55 PM](https://github.com/CExKForsyth/kyle_notes/assets/95767293/df72f3b4-5ae9-4949-9b21-573f19dc40c7)

In your terminal window that has `.../farmers-project/config_FARMER00_v5` open, run `yarn link isight`.
Run `nvm use`
Next run `yarn install`

Now is the moment where we would run whatever commands are needed for the particular upgrade. Again, this can be found in the [RELEASE_UPGRADE.md](https://github.com/i-Sight/isight_main_v5_beta/blob/v9.1.0/RELEASE_UPGRADE.md) file. And if we are doing a major upgrade, it will usually just be:

`make p-release-upgrade`

Once that has completed running, you can run your server again, and test the changes in your local environment.

## Step 5: Push & Merge Code Changes

If it's all good, commit your changes, and push that branch to GitHub.
`git add .`
`git commit -m "[FIER-6] Upgrade from v9.0.3 to v9.1.0"`
`git push origin FIER-6`

Then create a [Upgrade PR](https://github.com/i-Sight/config_FARMER00_v5/pull/5) in GitHub into the develop branch.

I usually include a lot of details so that I have a page to reference all the necessary changes before I deploy them. 

It helps to include a link to the Release Notes, the Compare changes, the Envars that are needed, and the Deployment instructions/Commands to run on Jenkins. (not everyone does this, but I do find it helpful)

Once this is approved and you've merged the PR into the `develop` branch, it is time to deploy.

## Step 6: Deployment

First, head to the Slack channel for this specific project, and ask the BA, (usually I just ping the whole channel by typing `@here`) if you are clear to deploy an upgrade to `v9.1.0`.

![Screen Shot 2023-11-14 at 2 20 42 PM](https://github.com/CExKForsyth/kyle_notes/assets/95767293/38efc650-22c6-4e66-aa86-97acf2cb9bf8)

Once you are given the go ahead to deploy, open Jenkins and locate your project. 

If you are having trouble figuring out which Orchestration the project is hosted on, look in the Pinned Messages on the Slack Channel and it might tell you. If not, a general rule of thumb is that these projects are sorted inot Orchestrations based on their global location. I follow this chart to help me figure it out sometimes:

orch01 - Azure US Gov
orch02 - Azure US East
orch03 - Azure Canada
orch04 - Azure Australia
orch05 - Azure Europe

To get to your project, click `Delivery`

![Screen Shot 2023-11-14 at 2 23 32 PM](https://github.com/CExKForsyth/kyle_notes/assets/95767293/07289d6a-cc86-4441-abca-af5a6d1ba501)

Then click `Non-prod`

![Screen Shot 2023-11-14 at 2 23 46 PM](https://github.com/CExKForsyth/kyle_notes/assets/95767293/2c3d5e72-e03a-4b52-be18-ef7233607584)

Then find it in the list, and click it.

![Screen Shot 2023-11-14 at 2 24 04 PM](https://github.com/CExKForsyth/kyle_notes/assets/95767293/d32b069e-657c-4dcf-b3fb-87d75d10f169)

From here, click the latest build on the left-hand side list of builds, and then from the drop-down, select `Rebuild`.

![Screen Shot 2023-11-14 at 2 26 38 PM](https://github.com/CExKForsyth/kyle_notes/assets/95767293/d942de88-0bac-494b-a513-f4569360099b)



