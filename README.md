# Working in Teams on Databricks

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

### Notebook Workflows

You can call 

### Libraries

## Notebook-Scoped Library Dependencies

## Moving to Production
