
[urfave/cli][1] and [kong][2] are the 2 more frequently recommended and well
viewed libraries in the Go community.

[spf13/cobra][3] and [spf13/viper][4] are also well regarded but more complex and
maintainance has fallen off for a while now. 

## urfave/cli

**Philosophy:** Imperative, command‑and‑flag centric API built on Go’s standard library only. 

**Core features:**
- Commands & subcommands with alias/prefix matching 
- Flexible, permissive help system 
- Dynamic shell completion (bash, zsh, fish, PowerShell) 
- Flag parsing for simple types, slices, durations, time 
- Input lookups via ENV, text files, structured sources via cli-altsrc 

## kong (alecthomas/kong)

**Philosophy:** Declarative CLI defined by Go structs and struct tags, with minimal boilerplate. 

**Core features:**
- Deeply nested commands via nested structs 
- Positional arguments alongside flags, with rich tag metadata (help, name, type) 
- Configuration file loaders (JSON, YAML, TOML, HCL) via kong.Configuration(...) 
- Resolvers for environment variables using the env tag 
- Custom mappers for complex types 
- Optional shell completion support through third‑party kongplete 

## Examples

### urfave/cli

```go
package main

import (
  "os"
  "github.com/urfave/cli/v3"
)

func main() {
  app := &cli.App{
    Name:  "greet",
    Usage: "say a greeting",
    Commands: []*cli.Command{
      {
        Name:    "hello",
        Usage:   "print hello",
        Flags: []cli.Flag{
          &cli.StringFlag{Name: "name", Aliases: []string{"n"}, Usage: "Name to greet"},
        },
        Action: func(c *cli.Context) error {
          name := c.String("name")
          if name == "" {
            name = "World"
          }
          println("Hello", name)
          return nil
        },
      },
    },
  }
  app.Run(os.Args)
}
```

### Kong

```go
package main

import (
  "fmt"
  "github.com/alecthomas/kong"
)

var CLI struct {
  Hello struct {
    Name string `arg:"" name:"name" help:"Name to greet"`
  } `cmd:"" help:"Print a greeting"`
}

func main() {
  ctx := kong.Parse(&CLI)
  switch ctx.Command() {
  case "hello <name>":
    fmt.Printf("Hello %s\n", CLI.Hello.Name)
  }
}
```

### Feature Comparison


| Feature                    | urfave/cli                                            | kong |
| -------------------------- | ----------------------------------------------------- | --- |
| **Commands & Subcommands** | Imperative list under `app.Commands`                  | Nested Go structs with `cmd` tags|
| **Flags & Arguments**      | `cli.Flag` types per command; args via `c.Args()`     | Flags and positional args via struct tags; argument usage supported |
| **Help & Usage**           | Flexible help output; man/Markdown via docs module    | Customizable via `ConfigureHelp`/`HelpFunc` |
| **Shell Completion**       | Built‑in dynamic completion                           | Available via \[kongplete] plugin |
| **Config & ENV**           | ENV, files, formats via `cli-altsrc`                  | `env` tag resolvers; JSON/TOML/HCL/YAML loaders |
| **Extensibility**          | Hooks, Before/After actions; add modules              | Mappers, Bind/Provide for DI; plugin architecture |
| **Dependencies**           | None (only Go std lib)                                | Uses reflection; one external module |
