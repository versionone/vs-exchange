# vs-exchange
A place to exchange VersionOne VS automation and other system customizations.

## What should an item that I want to add to the exchange contain?
For a new add-on, you should add a new directory whose name matches the name of your add-on at the root of the repo. This name MUST be unique within the repo.
The directory should contain a README.md file that describes what your add-on does. The README.md should also describe any dependencies your add-on has (plugins, progressions, assets, etc.)

The directory should contain one or more of the following subdirectories:
  - packages
  - pipelines
  - projects
  - tasks
  - canvases

The directory may also contain an optional registries subdirectories.

The packages, pipelines, projects, and tasks subdirectories, if they exists, should contain one or more files containing the JSON representation of the appropriate type. The name of the JSON file should match the name of the item. All names in a subdirectory must be unique. An identifier unique to your add-on should be included in all names in order to minimize the chance of a name conflict on import. We recommend prepending the name of the add-on. 

JSON files representing packages, pipelines, projects, and tasks can be obtained via  the ctm-export-catalog CLI. The ctm-export-package, ctm-export-pipeline, ctm-export-project, and ctm-export-task CLI and the associated APIs can also be used. For more information see https://versionone.github.io/continuum-api-docs/.

The canvases subdirectory, if it exists, should contain one or more subdirectories representing canvas projects. Each of these should directly match the output of the ctm-export-canvas CLI command. An identifier unique to your add-on should be included in all canvas project names in order to minimize the chance of a name conflict on import. Again, we recommend using the name of the add-on. 
As a guideline, the ctm-export-canvas command creates one or more directories which each represent a canvas project. These directories have proj_ prepended to the name of the canvas project. Each proj_ directory contains one or more subdirectories representing a canvas component. These subdirectories have comp_ prepended to the name of the canvas component. Each comp_ directory contains one or more files representing a canvas item. These files have item_ prepended to the name of the canvas item.

The registries subdirectory, if it exists, should contain one or more files containing the JSON representation of a global registry. The name of the JSON file should match the name of the registry. The JSON representation of a registry can be obtained via the get_registry API. All registry names in the subdirectory must be unique. We recommend prepending the name of the add-on to the registry to minimize the chance of a name conflict on import.

All files should have proper extensions for the filetype. For files outside of the canvases directory, this extension should be .json.

You will also need to add an entry to the manifest.json file at the root of the repo. The entry should include all the pieces of your add-on and is required for your add-on to be available through the exchange. Your entry should be added inside the add_ons array and have the following shape:
  
```    {
      "name": "exchange_example",
      "desc": "This is an example for the vs-exchange. It contains a README.md file to provide a brief description of this add-on, as well as a project, a package, a pipeline, a task, a canvas, and a registry document. Please use this as a guideline for how to structure new add-ons that you wish to submit to the exchange.",
      "contents": {
        "packages": ["myTeamPkg.json"],
        "pipelines": ["myTeamPipe.json"],
        "projects": ["myTeamProj.json"],
        "registries": ["myRegistry.json"],
        "tasks": ["myTeamTask.json"],
        "canvases": [
          {
            "project_name": "proj_exchange_demo",
            "components": [
              {
                "component_name": "comp_demo",
                "contents": ["item_port.css", "item_port.html", "item_port.js", "item_port.layout", "item_quort.css"]
              }
            ]
          }
        ]
      }
    }
```
