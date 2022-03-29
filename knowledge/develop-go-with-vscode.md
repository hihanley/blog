# Develop go with VSCode

## Print stderr or stdout in test and disable test cache

To print to stderr or stdout, you need to add-v to the go test command. Add test flag to the settings:  
```json
{
"go.testFlags": ["-v", "-count=1"]
}
```
