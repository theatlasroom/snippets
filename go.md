# Go

## Match multiple cases in switch statement

```go
switch repoHost {
case "gitlab", "gitlab.com":
  fmt.Println("🦊")
case "github", "github.com":
  fmt.Println("🐙")
default: 
  log.Fatal("Probably bitbucket 🙄")
}
```
