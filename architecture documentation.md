## Architecture and purpose of the system:
### Description:
JabRef is an open-source, cross-platform citation and reference management tool. It helps to collect and organize sources, find relevant papers and explore researches. It's a cross-platform apllication which is available for Windows, Linux and Mac OS X.

## Code structure:

![alt text](https://github.com/txing001/dads111/blob/master/architecture.png)

### Model:
It's in the center part of the whole architecture. It represents the most important data structures (BibDatases, BibEntries, Events, and related aspects) with a little bit logic attached to. It should have no dependencies to other classes of JabRef.

### Logic:
It acts as the function of intermediate layer. It helps to manipulate the model (responsible for reading/writing/importing/exporting and usually build as an API which GUI can call and use).It should only depend on model classes.

### GUI:
It acts as the function of interface with the actual users and help them to solve tasks. 

### Junit tests:
It is responsible for detecting violations of the most crucial dependencies (between logic, model, and gui), and the build will fail automatically in these cases.

### Additional utility packages:
It is for preferences and the cli.The cli package bundles classes that are responsible for JabRef's command line interface. The preferences convey all information customizable by a user for personal needs.

## Things to note:
For each layer, packages are formed based on their responsibilities,i.e.vertical structuring.We use an event bus to publish events from the model to the other layers. This allows us to keep the architecture but still be able to react upon changes within the core in the outer layers.

## Reference Link:
[high-level documentation](https://devdocs.jabref.org/high-level-documentation)