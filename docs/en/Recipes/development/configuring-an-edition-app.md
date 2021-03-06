---
title: Configuring an Edition App
description: "If you already match all requirements to become a Sponsor Account, learn now how to configure your own Edition Apps for child accounts!"
date: "2020-03-23"
tags: ["sponsor", "sponsor-account", "edition", "edition-app", "configure", "configuring"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/adding-new-docs/docs/en/Recipes/development/configuring-an-edition-app.md"
---

# Configuring an Edition App

The hierarchical relationship between a [Sponsor Account](https://vtex.io/docs/concepts/sponsor-account/) and its children, established by an [Edition app](https://vtex.io/docs/concepts/edition-app/), creates uniformity throughout an account family.

Hence, it can be advantageous for **complex account families** under the same brand or holding to have its own Edition App.

Once you have [enabled Sponsor Account behavior](https://vtex.io/docs/recipes/development/becoming-a-sponsor-account) in one of your accounts, follow the steps below to create your own Edition app.

## Step by step

If you aim to develop and install an Edition App in a child account, and if your account is already [**qualified**](https://vtex.io/docs/recipes/development/becoming-a-sponsor-account/) for that, check the following step by step.

## Step 1 - Creating an Edition app

1. Using your terminal and the [VTEX IO Toolbelt](https://vtex.io/docs/recipes/development/vtex-io-cli-installment-and-command-reference), log into your Sponsor Account.
2. Run the `vtex init` command.
3. Choose the `edition app` option. This will create a boilerplate repository in your local files.
4. Navigate to the `edition-app` folder and open the `manifest.json` file. It should look something like this:

```json
{
  "vendor": "vtex",
  "name": "edition-hello",
  "version": "0.1.1",
  "title": "Getting Started with VTEX Edition Apps",
  "description": "A sample edition app with a blank apps.json",
  "builders": {
    "edition": "0.x"
  },
  "dependencies": {
    "vtex.edition-business": "0.x"
  },
  "$schema": "https://raw.githubusercontent.com/vtex/node-vtex-api/master/gen/manifest.schema"
}
```

5. In the `manifest.json` file, change:

   - The `vendor` field to the name of the account you are logged in.
   - The `name` field to one of your choosing, which will be your new Edition's name. We suggest to use an `edition-` prefix in your edition name, for easy identification among app lists.

## Step 2 - Setting the Edition dependencies

Note that `vtex.edition-business` is listed in the `dependencies` section of the `manifest.json` file. This indicates that the new Edition app extends it, by inheriting all its apps and configurations.

According to your development needs, you might have to change the `dependencies`:

- If your store was built with our [legacy CMS](https://help.vtex.com/tutorial/o-que-e-o-cms--EmO8u2WBj2W4MUQCS8262) and this is your first Edition app, keep it as `"vtex.edition-business": "0.x"`.
- If your store was built with our [Store Framework](https://vtex.io/docs/getting-started/build-stores-with-store-framework/1/) and this is your first Edition app, change it to `"vtex.edition-store": "2.x"`.
- If you have more complex inheritance needs, change it to an Edition app you have previously developed (i.e. the `vendor` needs to be the same in both apps)
 
<div class="alert alert-warning">Every Edition app <strong>must</strong> declare a <code>dependency</code>. Only a single Edition app may be declared as a <code>dependency</code>.</div>

## Step 3 - Declaring apps

After setting up the initial configurations needed to develop your own Edition App, you can advance to declaring the bundle of apps and configurations that your Edition App will include.

For that, open the `edition/apps.json` file and add, under `apps`, all the apps and settings you want to impose to the child accounts.

```
{
    "apps": {
    }
}
```

<div class="alert alert-warning">
Be aware that an Edition App can only contain apps exclusively developed by the same <code>vendor</code> responsible for its release.
</div>

Notice that the new Edition App will consist of the union of the apps and configurations inherited from the parent Edition and the entries that you will add to the Edition's `apps.json` file.

<div class="alert alert-info">
Keep in mind that if any conflict arises from this, for example, both Editions declaring the same app on different majors, the priority is always given to the parent Edition. That means: it's impossible to change any inherited app or configuration - only extend them.
</div>

## Step 4 - Deploying the Edition app

Once you are sure of all the changes performed, it's time to **[publish and deploy](https://vtex.io/docs/recipes/store/publishing-an-app)** your Edition app.

## Step 5 - Installing the Edition App in a child account

After developing and deploying your new Edition App, you must 
[open a new ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) to the VTEX Support team asking for the installation of your new Edition App in the desired accounts.

In the following, once you receive a successful reply from the support ticket, you'll start to have child accounts sponsored by the account you just used to develop and release your new Edition App.

This implies that, from the child accounts point of view, the apps specified by the Sponsor will be immutable, meaning that these accounts won't be able to perform any changes, nor uninstall any of these apps.

Hence, in case you want to modify any app or configuration of your Edition App, you'll need to **launch a new version** bearing these changes. For that, you can go through our documentation on [updating Edition apps](https://vtex.io/docs/recipes/development/updating-edition-apps/).
