# Roadmap Golang: Marshalling e Unmarshalling JSON

Vou pular a parte de explicação do JSON. haha! Vamos para o que interessa.

Marshalling é o processo de transformar um objeto ou estrutura de dados em um formato que possa ser facilmente armazenado ou transmitido. No caso do JSON, marshalling é transformar uma estrutura em Go (struct) para uma string JSON.

Unmarshalling é o processo inverso: transformar uma string JSON em um objeto ou estrutura de dados. Em Go, isso significa pegar uma string JSON e preencher uma struct com esses dados.

## Golang e JSON

Golang tem um suporte nativo bem robusto para trabalhar com JSON através do pacote `encoding/json`. Vamos ver como funciona na prática.

## Estrutura Básica

Primeiro, vamos definir uma estrutura (struct) em Go. Imagine que você quer representar uma pessoa:

```go
package main

import (
    "encoding/json"
    "fmt"
)

type Pessoa struct {
    Nome  string `json:"nome"`
    Idade int    `json:"idade"`
    Email string `json:"email"`
}
```

A struct `Pessoa` tem três campos: `Nome`, `Idade` e `Email`. Note que usamos tags JSON para mapear os campos da struct para os campos do JSON.

## Marshalling

Vamos transformar essa struct em uma string JSON:

```go
func main() {
    pessoa := Pessoa{
        Nome:  "João",
        Idade: 30,
        Email: "joao@example.com",
    }

    jsonData, err := json.Marshal(pessoa)
    if err != nil {
        fmt.Println(err)
        return
    }

    fmt.Println(string(jsonData))
}
```

Saída:

```json
{"nome":"João","idade":30,"email":"joao@example.com"}
```

Aqui usamos `json.Marshal` para converter a struct `Pessoa` em uma string JSON. Se houver algum erro durante o processo, ele será capturado e impresso.

## Unmarshalling

Agora, vamos pegar uma string JSON e convertê-la de volta para uma struct:

```go
func main() {
    jsonData := []byte(`{"nome":"João","idade":30,"email":"joao@example.com"}`)

    var pessoa Pessoa
    err := json.Unmarshal(jsonData, &pessoa)
    if err != nil {
        fmt.Println(err)
        return
    }

    fmt.Printf("%+v
", pessoa)
}
```

Saída:

```go
{Nome:João Idade:30 Email:joao@example.com}
```

Aqui usamos `json.Unmarshal` para converter a string JSON de volta para a struct `Pessoa`. Note que precisamos passar um ponteiro para a struct.

## Exemplos Mais Complexos

Vamos complicar um pouco as coisas. Imagine que você tem um JSON com uma lista de pessoas:

```json
[
    {
        "nome": "João",
        "idade": 30,
        "email": "joao@example.com"
    },
    {
        "nome": "Maria",
        "idade": 25,
        "email": "maria@example.com"
    }
]
```

Podemos representar isso em Go como um slice de `Pessoa`:

```go
func main() {
    jsonData := []byte(`[
        {"nome":"João","idade":30,"email":"joao@example.com"},
        {"nome":"Maria","idade":25,"email":"maria@example.com"}
    ]`)

    var pessoas []Pessoa
    err := json.Unmarshal(jsonData, &pessoas)
    if err != nil {
        fmt.Println(err)
        return
    }

    for _, pessoa := range pessoas {
        fmt.Printf("%+v
", pessoa)
    }
}
```

Saída:

```go
{Nome:João Idade:30 Email:joao@example.com}
{Nome:Maria Idade:25 Email:maria@example.com}
```

Aqui, deserializamos um slice de `Pessoa` a partir de um JSON.

## Trabalhando com Campos Opcionais

Às vezes, os campos do JSON podem ser opcionais. Por exemplo:

```json
{
    "nome": "João",
    "idade": 30
}
```

Aqui, o campo `email` está faltando. Podemos lidar com isso usando ponteiros ou o tipo `omitempty` nas tags JSON:

```go
type Pessoa struct {
    Nome  string  `json:"nome"`
    Idade int     `json:"idade"`
    Email *string `json:"email,omitempty"`
}
```

## Marshalling e Unmarshalling com Mapas

Também podemos usar mapas em vez de structs. Isso é útil quando não conhecemos a estrutura do JSON de antemão:

```go
func main() {
    jsonData := []byte(`{"nome":"João","idade":30,"email":"joao@example.com"}`)

    var pessoa map[string]interface{}
    err := json.Unmarshal(jsonData, &pessoa)
    if err != nil {
        fmt.Println(err)
        return
    }

    fmt.Printf("%+v
", pessoa)
}
```

Saída:

```go
map[email:joao@example.com idade:30 nome:João]
```

## Customizando a Serialização e Desserialização

Às vezes, você precisa de mais controle sobre como os dados são serializados e desserializados. Para isso, você pode implementar as interfaces `json.Marshaler` e `json.Unmarshaler`.

Por exemplo, suponha que você quer que o campo `Idade` seja sempre serializado como uma string:

```go
type Pessoa struct {
    Nome  string `json:"nome"`
    Idade int    `json:"idade,string"`
    Email string `json:"email"`
}
```

Ou, você pode implementar métodos customizados:

```go
func (p Pessoa) MarshalJSON() ([]byte, error) {
    type Alias Pessoa
    return json.Marshal(&struct {
        Idade string `json:"idade"`
        *Alias
    }{
        Idade: fmt.Sprintf("%d anos", p.Idade),
        Alias: (*Alias)(&p),
    })
}

func main() {
    pessoa := Pessoa{
        Nome:  "João",
        Idade: 30,
        Email: "joao@example.com",
    }

    jsonData, err := json.Marshal(pessoa)
    if (err != nil) {
        fmt.Println(err)
        return
    }

    fmt.Println(string(jsonData))
}
```

Saída:

```json
{"nome":"João","idade":"30 anos","email":"joao@example.com"}
```

## Lidando com Erros

Sempre que trabalhamos com JSON, é importante lidar com possíveis erros de forma adequada. Veja como podemos fazer isso:

```go
func main() {
    jsonData := []byte(`{"nome":"João","idade":"trinta","email":"joao@example.com"}`)

    var pessoa Pessoa
    err := json.Unmarshal(jsonData, &pessoa)
    if err != nil {
        fmt.Println("Erro ao desserializar JSON:", err)
        return
    }

    fmt.Printf("%+v
", pessoa)
}
```

Saída:

```go
Erro ao desserializar JSON: json: cannot unmarshal string into Go struct field Pessoa.idade of type int
```

Entender Marshalling e Unmarshalling é fundamental para manipular dados.

Lembre-se de sempre lidar com erros e validar seus dados. E, claro, continue praticando e experimentando com diferentes tipos de dados e estruturas. Boa codificação!
