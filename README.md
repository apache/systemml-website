# Apache SystemDS Website

This repository contains the code for the SystemDS [main website](https://systemds.apache.org).

> If you would like to develop on the browser:
> 
> [![Open in Gitpod online](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/apache/systemds-website)

## Dependencies

### Node.js and npm

In order to build this project you will need the latest version of [node.js and npm](https://nodejs.org/).
Detailed instructions for download and installation can be found [here](https://github.com/nodejs/node#download).

### Gulp

We use Gulp to compile Sass and JS as well as run the Jekyll build. You can install it with npm:

```bash
sudo npm install -g gulp
```

## Building the website

### Download website dependancies

```bash
npm install
```

### Build website contents

```bash
gulp
```

If all goes well it open the site in your browser at `http://localhost:3000`.

### Troubleshooting

`Error: spawn jekyll.bat ENOENT` can be resolved by 

```bash
gem install jekyll
```

If you are still facing the issue, perhaps the discussion
[here](https://github.com/j143/systemds-website/issues/3) might would give some pointers.


## Updating the website

After generating files by following above instructions.

1. Create a new branch (for example, `update-website`) from the `asf-staging` branch.

```bash
git checkout asf-staging
git checkout -b update-website
```

2. Copy the generated files to the website `content` folder.

```bash
cp -r _site/* content/
git add content/*
git commit -m "Update SystemDS website with latest changes"
```

3. Add changes to the personal fork and create a PR against `asf-staging` branch.

```bash
git push https://github.com/<id>/systemds-website update-website
```

An example, [PR#83](https://github.com/apache/systemds-website/pull/83).

### Release Docs

Instruction for adding release specific version of docs to https://systemds.apache.org/docs

**Step 0: Prerequisites**

```sh
git clone https://github.com/apache/systemds
git clone https://github.com/apache/systemds-website
```

**Step 1:** 

generate docs with as per https://github.com/apache/systemds/tree/master/docs

```sh

# In this case the release tag is 2.1.0-rc3
git checkout 2.1.0-rc3

cd systemds/docs

./updateAPI.sh
```

**Step 2:**

copy the contents to `systemds-website` repo

```sh
cd systemds-website

# create a new directory with release no.
mkdir content/docs/2.1.0

# copy the files in docs/_site folder to 2.1.0
cp -r ../systemds/docs/_site/* content/docs/2.1.0
```

Then follow, https://github.com/apache/systemds-website#updating-the-website

**Step 3:**

Open a PR against `asf-staging` branch.

> Example PR: https://github.com/apache/systemds-website/pull/94

Website Preview at https://systemds.staged.apache.org

**Step 4:**

Production release via `asf-site` branch. For this approval from the
team is recommended.

> Example PR: https://github.com/apache/systemds-website/pull/95

Now, sync `asf-staging` and `asf-site` as:

```sh
# apply asf-staging commits onto asf-site
git rebase asf-staging asf-site

git push origin asf-site
```

> Important: Along with this update project metadata by modifying `release_version:` in
> [_src/_data/project.yml](https://github.com/apache/systemds-website/blob/master/_src/_data/project.yml#L46)

## How to add new dataset

To add a new dataset,

1. create `<dataset-name>.md` file in the [`_src/_datasets`](_src/_datasets) folder.
2. Upload dataset files to [`_src/assets/datasets/<dataset-name>`](_src/assets/datasets) folder.

And follow the _Updating the website_ procedure.
