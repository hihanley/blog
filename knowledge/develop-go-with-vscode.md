# Develop go with VSCode

## Print stderr or stdout in test and disable test cache

To print to stderr or stdout, you need to add-v to the go test command. Add test flag to the settings:  
```json
{
"go.testFlags": ["-v", "-count=1"]
}
```

## Build for linux/amd64 on linxu/arm64 with CGO_ENABLE=1
OS: ubuntu server 20.04

`sudo apt install gcc-x86-64-linux-gnu`

`GOOS=linux GOARCH=amd64 CC=x86_64-linux-gnu-gcc go build`