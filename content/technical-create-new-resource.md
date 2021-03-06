---
title: "Creating a New Resource"
permalink: /technical/new-resource/
lang: en
# translators: # Uncomment (remove #) for translations, one - name line per translator.
# - name: Translator 1
# - name: Translator 2
# contributors:
# - name: Contributor 1
# - name: Contributor 2
github:
  repository: w3c/wai-website-theme
  path: content/technical-create-new-resource.md
footer: > # Text in footer in HTML
  <p> This is the text in the footer </p>
---

{::nomarkdown}
{% include box.html type="start" title="Summary" class="" %}
{:/}

Creating a new resource is relatively straight forward.

{::nomarkdown}
{% include box.html type="end" %}
{:/}

{% include toc.html %}

## Creating the Repository

1. Visit the [github.com/new](https://github.com/new)
2. Select w3c/wai-resource-template as the template of the repository.
3. Set the name of the repository to a name starting with `wai-` – usually we use just lowercase letters but sometimes we use camel case
4. Set the visibility setting to public
5. Click on create repository
6. In the new repository, configure as below:

**All content is edited inside the `content` folder.**

## Configuring the Repository

After creation, the repository needs to be prepared to make it integrate with Netlify and the rest of the website properly. Those are a couple of manual steps, some must be done in preparation by the repository creator on GitHub, some have to be done on the command line for now (we try to do configure GitHub actions in the future to work around this).

### Prepare Some Variables

Search and replace every instance of `wai-resource-template` with the name of your repository. The easiest way is to check the repository out locally, change all the references and commit & push it to the server again. (There’s hope that this is automatable at some point in the future.)

### Finish Repository Set-Up on the Command Line

#### 1. Delete the Symlinks That Have Been Copied but That Don’t Work With the Github Template Process.

```bash
cd _data
rm *.*
cd ..
```

#### 2. Re-Add the Submodules and Recreate the Symlinks; Copy the navigation.yml File to the _Data Directory So That the Repository Has a Separate Navigation.

```bash
git submodule add https://github.com/w3c/wai-website-data.git _external/data
cd _data
ln -s ../_external/data/lang.json
ln -s ../_external/data/techniques.yml
ln -s ../_external/data/translations.yml
ln -s ../_external/data/wcag.yml
cp ../_external/data/navigation.yml navigation.yml
cd ..
git submodule update --remote
```

#### 3. Update Bundler; Run `Netlify Init` to Set Up Netlify; Commit All Data to the Repository

```bash
bundle update
netlify init
git add *
git commit -m "Theme/Tech update"
git push
```
