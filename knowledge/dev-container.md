# dev container config

## m1 mac
> this image support arm64
```jsonc
// For format details, see https://aka.ms/devcontainer.json. For config options, see the README at:
// https://github.com/microsoft/vscode-dev-containers/tree/v0.209.6/containers/ubuntu
{
	"name": "dev",
	"image": "mcr.microsoft.com/vscode/devcontainers/base:hirsute",
	// Set *default* container specific settings.json values on container create.
	"settings": {
		"terminal.integrated.defaultProfile.linux": "zsh"
	},
	// Add the IDs of extensions you want installed when the container is created.
	"extensions": [
		"TabNine.tabnine-vscode",
		"humao.rest-client",
		"redhat.vscode-xml",
		"redhat.vscode-yaml",
		// "golang.Go"
	],
	"mounts": [
		"source=dev-linux-var-lib-docker,target=/var/lib/docker,type=volume"
	],
	// Comment out connect as root instead. More info: https://aka.ms/vscode-remote/containers/non-root.
	"remoteUser": "vscode",
	"remoteEnv": {
		// "PATH": "${containerEnv:PATH}:/usr/local/go/bin",
		// "GOPROXY": "https://goproxy.cn,direct"
	}
}
```
