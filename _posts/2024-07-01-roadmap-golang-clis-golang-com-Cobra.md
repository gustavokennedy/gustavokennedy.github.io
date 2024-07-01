
# Roadmap Golang: CLIs em Golang com Cobra

Interfaces de Linha de Comando (CLIs) são ferramentas indispensáveis ​​no mundo da programação e administração de sistemas. Eles permitem que usuários e desenvolvedores interajam com aplicações através do terminal, proporcionando uma forma rápida e eficaz de executar comandos, automatizar tarefas e configurar sistemas. No ecossistema Go, uma das bibliotecas mais populares para a construção de CLIs poderosas e escaláveis ​​é a Cobra.
## O que é Cobra?

A maneira mais fácil de criar aplicativos CLI em Go é usando o Cobra. Uma equipe do [spf13](https://github.com/spf13) o desenvolveu e está sendo consumido por vários projetos conhecidos como Kubernetes, Hugo e etcd. Cobra tem uma provisão para definir comandos, subcomandos, sinalizadores e argumentos, além de suportar geração automática de documentação e preenchimento automático de shell.
## Estrutura Básica de um Projeto Cobra

Um projeto típico usando Cobra tem uma estrutura bem definida. Aqui está um exemplo de como pode ser organizado:

```
mycli/
├── cmd/
│   ├── root.go
│   ├── serve.go
│   └── version.go
├── main.go
├── go.mod
└── go.sum
```

- `cmd/`: Diretório que contém os arquivos de comandos.
- `main.go`: O ponto de entrada da aplicação.
- `go.mod` e `go.sum`: Arquivos de gerenciamento de dependências.

## Instalando Cobra

Para começar a usar Cobra, primeiro você precisa instalar a biblioteca. Execute o seguinte comando:

```sh
go get -u github.com/spf13/cobra/cobra
```

## Criando a Estrutura do Projeto

Para inicializar um novo projeto Cobra, você pode usar a ferramenta de CLI do próprio Cobra:

```sh
cobra init --pkg-name mycli
```

## Implementação de Comandos Básicos

Vamos criar um exemplo simples com dois comandos: `serve` e `version`.

### Arquivo `main.go`

```go
package main

import "mycli/cmd"

func main() {
    cmd.Execute()
}
```

### Arquivo `cmd/root.go`

```go
package cmd

import (
    "fmt"
    "os"

    "github.com/spf13/cobra"
)

var rootCmd = &cobra.Command{
    Use:   "mycli",
    Short: "MyCLI is a simple CLI application",
    Long:  `MyCLI is a longer description of this simple CLI application`,
}

func Execute() {
    if err := rootCmd.Execute(); err != nil {
        fmt.Println(err)
        os.Exit(1)
    }
}

func init() {
    cobra.OnInitialize(initConfig)
}

func initConfig() {
    // Configurações iniciais, como leitura de arquivos de configuração
}
```

### Arquivo `cmd/serve.go`

```go
package cmd

import (
    "fmt"
    "github.com/spf13/cobra"
)

var serveCmd = &cobra.Command{
    Use:   "serve",
    Short: "Starts the server",
    Long:  `Serve command starts the HTTP server for MyCLI application`,
    Run: func(cmd *cobra.Command, args []string) {
        fmt.Println("Server started on port 8080")
    },
}

func init() {
    rootCmd.AddCommand(serveCmd)
}
```

### Arquivo `cmd/version.go`

```go
package cmd

import (
    "fmt"
    "github.com/spf13/cobra"
)

var versionCmd = &cobra.Command{
    Use:   "version",
    Short: "Prints the version number",
    Long:  `Version command prints the current version of MyCLI application`,
    Run: func(cmd *cobra.Command, args []string) {
        fmt.Println("MyCLI v0.1")
    },
}

func init() {
    rootCmd.AddCommand(versionCmd)
}
```

## Flags e Argumentos

Flags e argumentos são componentes cruciais de qualquer CLI. Com Cobra, é fácil adicionar e gerenciar esses componentes.

### Adicionando Flags

Você pode adicionar flags aos comandos usando os métodos `Flags().XxxVarP`.

```go
func init() {
    serveCmd.Flags().StringP("port", "p", "8080", "Port to run the server on")
}
```

### Utilizando Flags

Para acessar o valor das flags dentro do comando, utilize `cmd.Flags().GetXxx`.

```go
Run: func(cmd *cobra.Command, args []string) {
    port, _ := cmd.Flags().GetString("port")
    fmt.Printf("Server started on port %s
", port)
}
```

## Geração Automática de Documentação e Autocompletar

Cobra facilita a geração de documentação e autocompletar para shells. Para gerar a documentação:

```sh
cobra doc --output docs/
```

Para gerar scripts de autocompletar:

```go
func init() {
    // para bash
    rootCmd.PersistentFlags().StringVar(&cfgFile, "config", "", "config file (default is $HOME/.cobra.yaml)")
    cobra.OnInitialize(initConfig)
    rootCmd.AddCommand(serveCmd, versionCmd)
    rootCmd.CompletionOptions.DisableDefaultCmd = true
}

func initConfig() {
    // configurações
}

func generateBashCompletionScript() {
    err := rootCmd.GenBashCompletionFile("mycli_completion.sh")
    if err != nil {
        fmt.Println("Error generating bash completion script:", err)
    }
}
```

## Conclusão

Cobra é uma ferramenta poderosa para criar CLIs em Go. Oferece uma estrutura organizada e extensível que facilita o desenvolvimento de aplicações complexas. Cobra se torna uma escolha natural para desenvolvedores Go que desejam construir interfaces de linha de comando eficientes e fáceis de usar quando oferece suporte a comandos, subcomandos, sinalizadores e geração de documentação. 

Tendo passado pelos exemplos e conceitos que discutimos até agora, agora você está bom o suficiente para começar a trabalhar.
