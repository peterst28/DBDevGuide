# Working in Teams on Databricks

A quick note: This document assumes git and Python, but it will work equally well with other tools and languages.

## Version Control

### Today

Individual developers should be able to:

1. Have isolation from other developers while they work
1. Be able to integrate their work with the work of others

Git is a great tool for this, but unfortunately, Databricks' integration with git is lacking.  You can only save out to git one file at a time.  This is not ideal, but there is a reasonably elegant way to accomplish this with the [Databricks command-line client](https://docs.databricks.com/dev-tools/cli/index.html).

The solution is this:

1. Pull the git repo to your laptop
1. Use the CLI to copy the contents of the repo to your Databricks user folder
`databricks workspace import_dir localpath /Users/example@databricks.com/example`
1. Do your work in Databricks
1. Use the CLI to copy the contents of the repo to your laptop.
`databricks workspace import_dir /Users/example@databricks.com/example localpath`
1. Use git on your laptop to commit and push the changes.

### Future

Expect better direct integration with Git in the future.

## Modularization

Legible and maintainable code is broken up into logical parts.  How do you accomplish this in the Databricks environment?  The following are a couple of approaches.

### Import Using %run

Include other notebooks in your notebook using the %run magic command.  For example:

`%run ./Includes/MyIncludedNotebook`

The notebook `MyIncludedNotebook` can contain standard Python class definitions, function definitions, etc.  Once you've included the `MyIncludedNotebook` using %run, you can make use of any functionality it defines.

### Libraries

Common code can be installed to clusters using the built-in library functionality.  This is a popular way to make relatively static code available to notebooks running on Databricks.  To get started take a look at this [documentation](https://docs.databricks.com/libraries.html#cluster-installed-library).  For more detail, this functionality is extensively documented [here](https://docs.databricks.com/libraries.html).

## Notebook-Scoped Library Dependencies

Sometimes, a developer may need a different library than the one installed on a shared cluster.  You can install notebook-scoped libraries to accomplish this using `%pip` or `%conda`, but be aware that this is a relatively expensive operation.  It's only recommended for development, not production.  

Here are some examples:

`%pip install matplotlib`
`%conda install matplotlib`
`%pip install -r /dbfs/requirements.txt`

This feature is [documented here](https://docs.databricks.com/notebooks/notebooks-python-libraries.html)

## Moving to Production
