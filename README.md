# React SPA Release Demo

A demo used to deploy a react SPA into aws cloudfront via github actions.


## Deployment Secrets & vars:

The following secrets are used

Secret | Description
--- | ---
AWS_ACCESS_KEY_ID | User used for deploying upon AWS S3 BUCKETS
AWS_SECRET_ACCESS_KEY | Aws secret

Whilst the following env vars should be defined

Name | Description
--- | ---
S3_BUCKET | The bucket where the app would be deployed upon
CLOUDFRONT_DIST_ID | The cloudfront distribution to invalidate upon

Each variable should be upon its respective github `Environment` as shown in `Settings`->`Environments` of this project.

## Dev Release

```
git checkout dev
git add .
git commit -am "Stuff to commit"
git push origin dev
```

## Prod release

### Step 0: Checkout master and merge dev

```
git cherckout master
# Is test is used use `test` branch instead
git merge dev
```

### Step 1: Bump Version

Patch eg. `0.0.0`->`0.0.1`

```
npm version patch
```

Minor eg `0.0.0`->`0.1.1`

```
npm version minor
```

Major eg `0.0.0`->`1.0.0`

```
npm version major
```

### Step2: Commit package.json

```
git add package.json
git commit -am "Version Bump"
```

### Step3: Push

```
git push origin master
```

### Rollback:

You can rollback a version like this:

```
gh workflow run "release" --ref master --field tag=v0.0.2
```

Replace `v0.0.2` with your own version.