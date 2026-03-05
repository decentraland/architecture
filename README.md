# Decentraland Architecture

This repository contains the main Decentraland Architecture diagram, defined using [D2 language](https://d2lang.com). The goal is to help you understand its components, responsibilities, how they interact, and help you navigate through them.

You will find the documentation index [here](docs/dcl-architecture.md) and, also, the content of this repository is published on the [Technical Documentation Site](https://docs.decentraland.org/contributor/).

## How to Update this Repository

The architecture is something live and from time to time we may need to update this diagram and information.

### Prerequisites

Install D2 by following the [official installation guide](https://d2lang.com/tour/install):

```bash
# macOS
brew install d2

# Linux
curl -fsSL https://d2lang.com/install.sh | sh -s --

# Other methods: https://d2lang.com/tour/install
```

### Editing the Diagram

The file [architecture.d2](architecture.d2) contains the diagram definition. D2 uses a simple, human-readable syntax:

```d2
service-name: Service Label {
  tooltip: "Description of the service"
  link: https://github.com/decentraland/repo-name

  sub-component: Sub Component {
    tooltip: "Description"
  }
}

service-name -> other-service
```

**Recommended VS Code extension**: [D2 Extension](https://marketplace.visualstudio.com/items?itemName=terrastruct.d2) for syntax highlighting and live preview.

### Generating the Architecture Image

Once the D2 file is updated, regenerate the architecture image:

```bash
make architecture
```

This will produce both `docs/architecture.svg` and `docs/architecture.png`.

> **Note**: With any change to the diagram, make sure the [documentation](docs/dcl-architecture.md) describing its components is still up to date.

### D2 Resources

- [D2 Tour](https://d2lang.com/tour/intro) - Learn the language basics
- [D2 Playground](https://play.d2lang.com) - Try D2 in the browser
- [D2 Examples](https://d2lang.com/tour/layouts) - Layout and styling examples
