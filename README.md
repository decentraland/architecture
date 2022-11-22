# Decentraland Architecture 

This repository aims to have the main Decentraland Architecture, defined using [dot language](https://graphviz.org/doc/info/lang.html). The goal is to help you understand it's components, responsibilities, how they interact and help you navigate through them. 

You will find the documentation index [here](docs/dcl-architecture.md) and, also, the content of this repository is published on the [Technical Documentation Site](https://docs.decentraland.org/contributor/). 

# How to Update this Repository

The architecture is something live and from time to time we may need to update this diagram and information, in order to do so the file [architecture.dot](architecture.dot) contains the definition of the image [architecture.png](docs/architecture.png). It can be a bit challenging to update and make it look nice, the VSCode extension [Graphviz Interactive Preview](https://marketplace.visualstudio.com/items?itemName=tintinweb.graphviz-interactive-preview) can be very helpful to view your changes as you make them. 
Once the architecture dot file is updated, you need to compile it and regenerate the architecture.svg file, for that you first need to [install graphviz](https://graphviz.org/download/) and then you can just run the `make` command and replace the architecture.svg file under `/docs`. Note that with any change on the diagram you need to validate that this documentation describing it's components is still updated. 
