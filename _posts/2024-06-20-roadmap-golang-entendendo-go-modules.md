
# Roadmap Golang: Go Modules

Primeiro, precisamos entender que o Go Modules é um sistema de gerenciamento de dependências introduzido na linguagem de programação Go a partir da versão 1.11. Ele permite que desenvolvedores gerenciem versões de pacotes de maneira mais eficiente, além de proporcionar um ambiente de desenvolvimento mais consistente.

### Configurando o Go Modules

Antes de começar a usar os módulos, é necessário garantir que seu projeto esteja configurado para utilizá-los. Para isso, verifique se a variável de ambiente `GO111MODULE` está definida como `on`. A partir da versão 1.16, essa configuração é o padrão.

Você pode inicializar um novo módulo utilizando o comando:

```sh
go mod init nome-do-modulo
```

Isso criará um arquivo `go.mod` na raiz do seu projeto, que será utilizado para gerenciar as dependências.

## Estrutura do Arquivo go.mod

Um arquivo `go.mod` típico se parece com isso:

```go
module github.com/usuario/projeto

go 1.16

require (
    github.com/gin-gonic/gin v1.7.2
    github.com/jinzhu/gorm v1.9.16
)
```

- `module`: Especifica o nome do módulo.
- `go`: Define a versão do Go que está sendo usada.
- `require`: Lista as dependências do projeto e suas versões.

## Adicionando Dependências

Para adicionar uma nova dependência ao seu projeto, use o comando `go get`:

```sh
go get github.com/sirupsen/logrus@v1.8.1
```

Isso atualizará o arquivo `go.mod` e criará ou atualizará o arquivo `go.sum`, que contém hashes de verificação das dependências para garantir a integridade.

## Exemplo Complexo

Vamos criar um exemplo mais complexo que utiliza múltiplos pacotes externos e módulos internos. Nosso projeto será uma API RESTful que se comunica com um banco de dados.

### Estrutura do Projeto

```
myapp/
|-- go.mod
|-- go.sum
|-- main.go
|-- handlers/
|   |-- user.go
|-- models/
    |-- user.go
```

### Arquivo go.mod

```go
module github.com/usuario/myapp

go 1.16

require (
    github.com/gin-gonic/gin v1.7.2
    github.com/jinzhu/gorm v1.9.16
    github.com/sirupsen/logrus v1.8.1
)
```

### Arquivo main.go

```go
package main

import (
    "github.com/gin-gonic/gin"
    "github.com/jinzhu/gorm"
    _ "github.com/jinzhu/gorm/dialects/sqlite"
    "github.com/sirupsen/logrus"
    "github.com/usuario/myapp/handlers"
)

func main() {
    r := gin.Default()

    db, err := gorm.Open("sqlite3", "test.db")
    if err != nil {
        logrus.Fatal("failed to connect database")
    }
    defer db.Close()

    db.AutoMigrate(&handlers.User{})

    r.GET("/users", handlers.GetUsers(db))
    r.POST("/users", handlers.CreateUser(db))

    r.Run()
}
```

### Arquivo handlers/user.go

```go
package handlers

import (
    "net/http"

    "github.com/gin-gonic/gin"
    "github.com/jinzhu/gorm"
    "github.com/usuario/myapp/models"
)

type User struct {
    gorm.Model
    Name  string `json:"name"`
    Email string `json:"email"`
}

func GetUsers(db *gorm.DB) gin.HandlerFunc {
    return func(c *gin.Context) {
        var users []User
        db.Find(&users)
        c.JSON(http.StatusOK, users)
    }
}

func CreateUser(db *gorm.DB) gin.HandlerFunc {
    return func(c *gin.Context) {
        var user User
        if err := c.ShouldBindJSON(&user); err != nil {
            c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
            return
        }
        db.Create(&user)
        c.JSON(http.StatusOK, user)
    }
}
```

### Arquivo models/user.go

```go
package models

import "github.com/jinzhu/gorm"

type User struct {
    gorm.Model
    Name  string
    Email string
}
```

## Trabalhando com Versões

Você pode especificar versões de dependências no seu `go.mod` usando sintaxes como `@latest`, `@v1.2.3`, ou até mesmo commit hashes. Por exemplo:

```sh
go get github.com/gin-gonic/gin@latest
go get github.com/jinzhu/gorm@v1.9.16
go get github.com/sirupsen/logrus@v1.8.1
```

## Atualizando Dependências

Para atualizar todas as dependências para suas últimas versões compatíveis, você pode usar:

```sh
go get -u ./...
```

Para atualizar uma dependência específica:

```sh
go get -u github.com/gin-gonic/gin
```

## Gerenciando Submódulos

No Go, você pode ter submódulos dentro do seu repositório. Isso é útil para dividir grandes projetos em partes menores e mais gerenciáveis. Cada submódulo terá seu próprio arquivo `go.mod`.

### Criando um Submódulo

1. Navegue até o diretório onde deseja criar o submódulo.
2. Execute `go mod init caminho/do/submodulo`.

Por exemplo, se quisermos criar um submódulo em `handlers`:

```sh
cd handlers
go mod init github.com/usuario/myapp/handlers
```

### Importando um Submódulo

No arquivo `main.go`, você importaria o submódulo da seguinte forma:

```go
import "github.com/usuario/myapp/handlers"
```

## Conclusão

Go Modules é uma ferramenta poderosa para gerenciamento de dependências em projetos Go. Ele facilita a manutenção de versões consistentes e a modularização de grandes projetos. Com os exemplos fornecidos, você deve estar pronto para começar a utilizar Go Modules em seus próprios projetos.

## Dependências Transitivas

Quando você adiciona uma dependência ao seu projeto, ela pode ter suas próprias dependências, chamadas de dependências transitivas. O Go Modules gerencia isso automaticamente.

### Exemplo

Vamos adicionar a biblioteca `gorm` que depende de `jinzhu/inflection`.

#### Arquivo go.mod

```go
module github.com/usuario/projeto

go 1.16

require (
    github.com/jinzhu/gorm v1.9.16
)
```

#### Arquivo go.sum

O arquivo `go.sum` incluirá todas as dependências transitivas:

```sh
github.com/jinzhu/gorm v1.9.16 h1:xxxxx
github.com/jinzhu/gorm v1.9.16/go.mod h1:xxxxx
github.com/jinzhu/inflection v1.0.0 h1:xxxxx
github.com/jinzhu/inflection v1.0.0/go.mod h1:xxxxx
```

## Versão Mínima Compatível

A funcionalidade de versão mínima compatível (`minimal version selection`) garante que o Go Modules sempre use a menor versão compatível com as restrições especificadas.

### Exemplo

Se você adicionar uma dependência com uma versão mínima e depois atualizar para uma versão mais recente, o Go usará a menor versão que satisfaz ambas as restrições.

#### Inicialmente

```sh
go get github.com/gin-gonic/gin@v1.5.0
```

```go
require github.com/gin-gonic/gin v1.5.0
```

#### Atualizando

```sh
go get github.com/gin-gonic/gin@v1.6.0
```

```go
require github.com/gin-gonic/gin v1.6.0
```

Se outra dependência exigir `gin-gonic/gin` com versão `>=v1.4.0`, o Go Modules resolverá para `v1.6.0`.

## Projeto com Múltiplos Módulos

Vamos criar um exemplo com múltiplos módulos que se inter-relacionam. Teremos três módulos: `auth`, `user`, e `main`.

### Estrutura do Projeto

```
multi-module-app/
|-- main/
|   |-- go.mod
|   |-- main.go
|-- auth/
|   |-- go.mod
|   |-- auth.go
|-- user/
    |-- go.mod
    |-- user.go
```

### Módulo `auth`

#### Arquivo go.mod

```go
module github.com/usuario/multi-module-app/auth

go 1.16
```

#### Arquivo auth.go

```go
package auth

import "fmt"

func Authenticate(username, password string) bool {
    fmt.Println("Authenticating user:", username)
    return username == "admin" && password == "admin"
}
```

### Módulo `user`

#### Arquivo go.mod

```go
module github.com/usuario/multi-module-app/user

go 1.16
```

#### Arquivo user.go

```go
package user

import "fmt"

type User struct {
    ID    int
    Name  string
    Email string
}

func GetUser(id int) User {
    fmt.Println("Fetching user with ID:", id)
    return User{ID: id, Name: "John Doe", Email: "john.doe@example.com"}
}
```

### Módulo `main`

#### Arquivo go.mod

```go
module github.com/usuario/multi-module-app/main

go 1.16

require (
    github.com/usuario/multi-module-app/auth v0.0.0
    github.com/usuario/multi-module-app/user v0.0.0
)
```

#### Arquivo main.go

```go
package main

import (
    "fmt"
    "github.com/usuario/multi-module-app/auth"
    "github.com/usuario/multi-module-app/user"
)

func main() {
    if auth.Authenticate("admin", "admin") {
        u := user.GetUser(1)
        fmt.Println("User:", u)
    } else {
        fmt.Println("Authentication failed")
    }
}
```

### Como Criar e Rodar

1. **Inicialize cada módulo individualmente:**

    ```sh
    cd auth
    go mod init github.com/usuario/multi-module-app/auth
    cd ../user
    go mod init github.com/usuario/multi-module-app/user
    cd ../main
    go mod init github.com/usuario/multi-module-app/main
    ```

2. **No diretório `main`, obtenha as dependências:**

    ```sh
    go get github.com/usuario/multi-module-app/auth
    go get github.com/usuario/multi-module-app/user
    ```

3. **Execute o programa principal:**

    ```sh
    go run main.go
    ```

Precisamos entender que o Modules facilita o gerenciamento de dependências, mesmo em projetos complexos com múltiplos módulos. Com o Go Modules, é possível manter um controle rigoroso sobre as versões das dependências e garantir a integridade do projeto.
