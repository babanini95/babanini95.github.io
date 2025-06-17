+++
title = 'PokedexCLI'
date = 2025-06-16T10:46:31+08:00
draft = true
+++
## Introduction

[PokedexCLI](https://github.com/babanini95/pokedexcli) is a Go-based REPL (Read-Eval-Print-Loop) command-line interface that allows you to interact with Pokemon data and play with it. It is a guided project from [boot.dev course](https://www.boot.dev/courses/build-pokedex-cli-golang). To build the same application you can enter the course or follow along with me through this article!.

With PokedexCLI, you can explore Pokemon data, catch it, and manage you Pokemon collection. All the data was fetched from [PokeAPI](https://pokeapi.co).

Through this project, I learn how to:

- Learn how to parse JSON in Go
- Practice making HTTP requests in Go
- Learn how to build a CLI tool that makes interacting with a back-end server easier
- Get hands-on practice with local Go development and tooling
- Learn about caching and how to use it to improve performance

## The Making Journey

The idea of PokedexCLI is just to replicate a [Pokedex](https://bulbapedia.bulbagarden.net/wiki/Pok%C3%A9dex) using CLI. The core functions of PokedexCLI are:

- List location areas in the Pokemon World
- Explore all Pokemons in a specific area
- Catch a Pokemon
- List all Pokemons we have caught
- Inspect the Pokemon stats

### Tools and Technologies

- **Go**. One of *Go* benefit is we don't have to confuse about importing libraries since it provides a lot of robust standard libraries. In fact this application only use standard libraries. It is also easy to learn, compile binary really fast, and run on any system without requiring any existing libraries, runtimes, or dependencies.
- **Poke API**. It is a website that provide tons of data related to Pokemon. You can consume the data using [RESTful API](https://www.redhat.com/en/topics/api/what-is-a-rest-api)

### Resources

- [Go documentation](https://go.dev/doc/), especially for [standard library](https://pkg.go.dev/std) since we use it a lot
- [Poke API documentation](https://pokeapi.co/docs/v2)

### Development

**Attention!!!**

- I recommend you to learn a little bit of Go before following along. The [boot.dev go course](https://www.boot.dev/courses/learn-golang) is a good start.
- All the command here is using `bash`. If you use windows, follow accordingly.

#### Project Setup

Before we dive into the development process, we need to install [Go toolchain](https://go.dev/doc/install) first. You can follow along the instruction from the doc or any other resources. For my case, I follow the [installation steps for WSL](https://www.jetbrains.com/help/go/how-to-use-wsl-development-environment-in-product.html#wsl-general) from JetBrain since I use WSL. After complete the installation, check your `go version`.

```bash
go version
```

Create a project folder named `pokedexcli` or whatever name you like and [create a go module](https://go.dev/doc/tutorial/create-module) in the root of the project.

```bash
mkdir pokedexcli
cd pokedexcli
go mod init MODULE_NAME
```

We can naming our module with any name we like, but it is recommended to naming it by our remote Git repository. For my case, I store the repo in GitHub, so my `MODULE_NAME` would be `github.com/babanini95/pokedexcli`.

```bash
go mod init github.com/babanini95/pokedexcli
```

Create a `main.go` file in the root of the project.

```go
package main

func main() {

}
```

This will be the script where users interact with.

#### REPL Core Loop

REPL (read-eval-print-loop) is a simple interactive program that takes user inputs, evaluate them, and print the result. In our case, we will create a REPL that allows users to interact with the Pokemon data.

To create a REPL, we can create a for loop that reads user input, evaluates it, and prints the result.

To read user's input, we can use the [`bufio.NewScanner`](https://pkg.go.dev/bufio#NewScanner) to block the code and wait for user input. Once the user press enter, the code continues and the input is available in the `bufio.Scanner` object. We can then use the [`.Scan()`](https://pkg.go.dev/bufio#Scanner.Scan) and [`.Text()`](https://pkg.go.dev/bufio#Scanner.Text) method to get the input as a string.

```go
package main

import (
	"bufio"
    "os"
	"fmt"
    "strings"
)
func main() {
	scanner := bufio.NewScanner(os.Stdin)

	for {
		fmt.Print("Pokedex > ")
		scanner.Scan()
		cleanedInput := cleanInput(scanner.Text())

		if len(cleanedInput) == 0 {
			continue
		}

		userCommand := cleanedInput[0]
		args := []string{}
		if len(cleanedInput) > 1 {
			args = cleanedInput[1:]
		}

		fmt.Printf("command input: %s\narguments: %s\n", userCommand, args)
	}
}

func cleanInput(text string) []string {
	cleanText := strings.Fields(strings.ToLower(text))
	return cleanText
}
```

This code will create a simple REPL that waits for user input and prints the input back to the user. The `cleanInput` function is used to clean the `string` input by converting it to lowercase and splitting it into `[]string`. The first element of the `[]string` is the user command, and the rest are the arguments.

We can run the code using the `go run` command.

```bash
go run .
```

You should see the prompt `Pokedex >` and you can type your command. For example, if you type `catch pikachu`, the output will be:

```bash
Pokedex > catch pikachu
command input: catch
arguments: [pikachu]
```

This shows that the REPL is working and we can now start implementing the commands.

#### Commands

To implement the commands, we can create a `cliCommand` struct that contains the command name, description, and a function to execute the command. We can then create a map of commands and register them in the `main` function. For me, I separate the commands logic into a new file called `commands.go` and create a `cliCommand` struct in it.

For now, we will create two commands: `help` and `exit`. The `help` command will display a help message, and the `exit` command will exit the Pokedex. We can implement these commands in the `commands.go` file.

```go
package main

import (
	"fmt"
	"os"
)

type cliCommand struct {
	name        string
	description string
	callback    func([]string) error
}

var commands map[string]cliCommand

func generateCommand() map[string]cliCommand {
	return map[string]cliCommand{
		"help": {
			name:        "help",
			description: "Displays a help message",
			callback:    commandHelp,
		},
		"exit": {
			name:        "exit",
			description: "Exit the Pokedex",
			callback:    commandExit,
		},
	}
}

func commandExit(args []string) error {
	fmt.Println("Closing the Pokedex... Goodbye!")
	os.Exit(0)
	return nil
}

func commandHelp(args []string) error {
	output := "Welcome to the Pokedex!\nUsage:\n"

	for _, command := range commands {
		output += fmt.Sprintf("\n%s: %s", command.name, command.description)
	}

	fmt.Println(output)
	return nil
}
```

One of the benefits of using a struct is that we can easily add more fields in the future, such as aliases or flags. The `commands` map is used to store the commands and their corresponding `cliCommand` struct. The `generateCommand` function initializes the commands map with the available commands.

In the `main.go` file, we can initialize the commands map and call the command's callback function when the user input matches a command.

```go
package main

import (
	"bufio"
	"fmt"
	"os"
	"time"
)

func main() {
	commands = generateCommand()
	scanner := bufio.NewScanner(os.Stdin)

	for {
		fmt.Print("Pokedex > ")
		scanner.Scan()
		cleanedInput := cleanInput(scanner.Text())

		if len(cleanedInput) == 0 {
			continue
		}

		userCommand := cleanedInput[0]
		args := []string{}
		if len(cleanedInput) > 1 {
			args = cleanedInput[1:]
		}

		if cmd, ok := commands[userCommand]; !ok {
			fmt.Println("Unknown command")
		} else {
			err := cmd.callback(args)
			if err != nil {
				fmt.Println(err)
			}
		}
	}
}
```

Now, when you run the PokedexCLI and type `help`, it will display the help message with the available commands. If you type `exit`, it will close the Pokedex.

```bash
Pokedex > help
Welcome to the Pokedex!
Usage:
help: Displays a help message
exit: Exit the Pokedex
Pokedex > exit
Closing the Pokedex... Goodbye!
```
