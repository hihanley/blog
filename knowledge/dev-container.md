# dev container config

## m1 mac
> this image support arm64
```json
// For format details, see https://aka.ms/devcontainer.json. For config options, see the README at:
// https://github.com/microsoft/vscode-dev-containers/tree/v0.209.6/containers/ubuntu
{
	"name": "dev",
	"image": "mcr.microsoft.com/vscode/devcontainers/base:hirsute",

	// Set *default* container specific settings.json values on container create.
	"settings": {},

	// Add the IDs of extensions you want installed when the container is created.
	"extensions": [],

	// Comment out connect as root instead. More info: https://aka.ms/vscode-remote/containers/non-root.
	"remoteUser": "vscode",
}
```
