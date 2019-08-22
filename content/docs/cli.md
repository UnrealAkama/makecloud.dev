# CLI Usage

## mc invoke

This is the main Makecloud command that is used which runs the complete set of nodes in a Makecloud project. You can also specify the project path after the command in the style of `mc invoke ~/project_path`

`--nocache` disables all the caching in the project. This can be useful if you want to force rebuild in certain circumstances such as dealing with side effects in the build process.

`--deploy` is the flag to enable nodes with the `deploy` keyword to be run. Typically the usage of this is that all nodes without deploy flag are for building, running tests, and security checks. This means that individual users can run the invoke command and no code in production should change.

## mc graphviz

This subcommand is used for generating a graphviz dot diagram. This can be used to evaluate the shape of the build graph and ensure that all dependencies are correct.

## mc show-configs

Often it's useful to quickly ensure that all the configs are present and being seen.
