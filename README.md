# Subdir buildpack

This buildpack is used to deploy an application to Heroku from a subdirectory of a git repository, rather than from the repository root. It is based on [timanovsky's subdir-heroku-buildpack](https://github.com/timanovsky/subdir-heroku-buildpack).

When this buildpack is set to be the first buildpack in the Heroku build chain, application deployment from a subdirectory happens in three steps:

 1. The contents of the directory specified by `PROJECT_PATH` are saved in a temporary location.
 2. All non-hidden files are deleted from the repository root.
 3. The contents of the temporary directory are copied into the repository root.

## Usage

Add this buildpack as the first (or one of the first) buildpacks in your application's build chain. It must certainly appear before any buildpacks that expect to be able to operate on the root directory. You must also set the `PROJECT_PATH` configuration variable on your application to indicate the subdirectory to deploy.

To prepend this buildpack to your application's build chain, run the command:

    heroku buildpacks:add --index=1 --app=<your-app-name> https://github.com/owenniles/subdir-heroku-buildpack.git

To set the `PROJECT_PATH` configuration variable, run the command:

    heroku config:set --app=<your-app-name> PROJECT_PATH=<path/to/subdirectory>