# vs-exchange
A place to exchange VersionOne VS automation and other system customizations.

## Table of Contents
1. [Name & Shape Requirements](#name--shape-requirements)
    1. [API Export Commands](#api-export-commands)
    2. [Canvases Subdirectory](#canvases-subdirectory)
    3. [Manifest](#manifest)
2. [Contributing](#contributing)
    1. [Creating a Pull Request](#creating-a-pull-request)
    2. [Questions](#questions)
    3. [Reporting Issues](#reporting-issues)

## Name & Shape Requirements

**What should an item that I want to add to the exchange contain?**

For a new Add-On, you should add a new directory whose name matches the name of your Add-On at the root of the repo. 

**Note:** This name MUST be unique within the repo.

The directory should contain a `README.md` file that describes what your Add-On does. The `README.md` should also describe any dependencies your Add-On has (plugins, progressions, assets, etc.)

All files outside of the `canvases` subdirectory should have the proper `.json` extension.

**The directory should contain one or more of the following subdirectories:**
  - packages
  - pipelines
  - projects
  - tasks
  - canvases
  - registries*

*_must include one of the other subdirectories as well._

The packages, pipelines, projects, tasks and registries subdirectories, if they exists, should contain one or more files containing the JSON representation of the appropriate type. The name of the JSON file should match the name of the item. All names in a subdirectory must be unique. An identifier unique to your Add-On should be included in all names in order to minimize the chance of a name conflict on import. We recommend prepending the name of the Add-On.

For an example of how your Add-On should look, see the [exchange-example Add-On](https://github.com/versionone/vs-exchange/tree/master/exchange_example)

### API Export Commands
JSON files representing Packages, Pipelines, Projects, and Tasks can be obtained via  the `ctm-export-catalog` CLI. The `ctm-export-package`, `ctm-export-pipeline`, `ctm-export-project`, and `ctm-export-task` CLI and the associated APIs can also be used. To obtain the JSON representaion of a Registry, you can use the `get_registry` API. For more information see https://versionone.github.io/continuum-api-docs/.

### Canvases Subdirectory
The canvases subdirectory, if it exists, should contain one or more subdirectories representing Canvas Projects. Each of these should directly match the output of the `ctm-export-canvas` CLI command. An identifier unique to your Add-On should be included in all Canvas Project names in order to minimize the chance of a name conflict on import. Again, we recommend using the name of the Add-On. [See example Add-On Canvas](https://github.com/versionone/vs-exchange/tree/master/exchange_example/canvases) for clarification

As a guideline, the `ctm-export-canvas` command creates one or more directories which each represent a Canvas Project. These directories have `proj_` prepended to the name of the Canvas Project. Each `proj_` directory contains one or more subdirectories representing a Canvas Component. These subdirectories have `comp_` prepended to the name of the Canvas Component. Each `comp_` directory contains one or more files representing a Canvas Item. These files have `item_` prepended to the name of the Canvas Item.

### Manifest
You will also need to add an entry to the `manifest.json` file at the root of the repo. The entry should include all the pieces of your Add-On and is required for your Add-On to be available through the exchange. Your entry should be added in alphabetical order by `name` inside the `add_ons` array and have the following shape:
  
```json
{
    "name": "exchange_example",
    "desc": "This is an example Add-On for vs-exchange. It contains a README.md file to provide a brief description of the Add-On, as well as a list of the Project, Package, Pipeline, Task, Canvas, and Registry documents included in the Add-On. Please use this as a guideline for how to structure a new Add-On that you wish to submit to the exchange.",
    "contents": {
        "packages": ["example_myTeamPkg.json"],
        "pipelines": ["example_myTeamPipe.json"],
        "projects": ["example_myTeamProj.json"],
        "registries": ["example_myRegistry.json"],
        "tasks": ["example_myTeamTask.json"],
        "canvases": [
            {
                "project_name": "proj_example_exchange_demo",
                "components": [
                    {
                        "component_name": "comp_demo",
                        "contents": [
                            "item_port.css",
                            "item_port.html",
                            "item_port.js",
                            "item_port.layout",
                            "item_quort.css"
                        ]
                    }
                ]
            }
        ]
    }
}
```

## Contributing

Thank you for your interest in `vs-exchange`. All forms of contribution are welcome, from issue reports to pull requests and documentation.

### Creating a Pull Request
Make a fork of `vs-exchange`, make your changes and [create a pull request](https://github.com/versionone/vs-exchange/pulls) from your fork against `vs-exchange:master`.

**Before you open a pull request:**
- Validate all JSON through a linter such as https://jsonlint.com/
- Verify that your Add-On meets the [Name & Shape Requirements](https://github.com/versionone/vs-exchange#name--shape-requirements) described above
- If you have questions don't hesitate to reach out!

### Questions
If you have questions about implementation details, help, or support please [create an issue](https://github.com/versionone/vs-exchange/issues) and tag it with `question`.

### Reporting Issues
If you have found what you think is a bug, please [create an issue](https://github.com/versionone/vs-exchange/issues) and tag it with `bug`. Add-On authors are responsible for the ongoing maintenance of their Add-Ons.
