# Roadmap Golang: Sintaxe

Olá a todos! Quero compartilhar com vocês um pouco da sintaxe Golang neste conteúdo. Vamos aprender?

## Declaração de Variáveis

As variáveis podem ser declaradas usando a palavra-chave `var` ou o operador de declaração curta `:=`.

### Usando `var`

```go
var nome string
var idade int
var salario float64
```

Aqui, declaramos três variáveis de diferentes tipos: `string`, `int` e `float64`. As variáveis em Go são tipadas estaticamente, o que significa que o tipo da variável deve ser conhecido em tempo de compilação. Bem importante isso!

### Usando `:=`

```go
nome := "João"
idade := 30
salario := 4500.50
```

Neste caso, usamos o operador `:=` para declarar e inicializar variáveis. Go infere o tipo da variável a partir do valor atribuído.

## Estruturas de Controle

A linguagem oferece várias estruturas de controle para gerenciar o fluxo do programa: `if`, `for`, `switch`, entre outras.

### Estrutura `if`

```go
if idade >= 18 {
    fmt.Println("Você é maior de idade.")
} else {
    fmt.Println("Você é menor de idade.")
}
```

O `if` em Go é similar a outras linguagens, mas não requer parênteses ao redor da condição.

### Estrutura `for`

No Go tem apenas uma estrutura de loop: o `for`. Ele pode ser usado de várias formas.

#### Loop Tradicional

```go
for i := 0; i < 10; i++ {
    fmt.Println(i)
}
```

#### Loop `while`

```go
i := 0
for i < 10 {
    fmt.Println(i)
    i++
}
```

#### Loop Infinito

```go
for {
    fmt.Println("Loop infinito")
}
```

### Estrutura `switch`

Vamos ver a estrutura `switch`:

```go
dia := "segunda"
switch dia {
case "segunda":
    fmt.Println("Início da semana")
case "sexta":
    fmt.Println("Quase fim de semana")
default:
    fmt.Println("Meio da semana")
}
```

Ao contrário de outras linguagens, o `switch` em Go não precisa de `break` para evitar a queda para o próximo caso.

## Funções

Funções em Go são declaradas usando a palavra-chave `func`. Elas podem retornar múltiplos valores, o que é uma característica poderosa da linguagem.

### Função Simples

```go
func saudacao(nome string) string {
    return "Olá, " + nome
}
```

### Função com Múltiplos Retornos

```go
func dividir(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("divisão por zero")
    }
    return a / b, nil
}
```

### Função Anônima

```go
anonima := func(a, b int) int {
    return a + b
}
fmt.Println(anonima(2, 3))
```

## Estruturas de Dados

Go fornece várias estruturas de dados integradas, como arrays, slices, mapas e structs.

### Arrays

Arrays têm tamanho fixo.

```go
var numeros [5]int
numeros[0] = 1
```

### Slices

Slices são mais flexíveis que arrays, pois podem mudar de tamanho.

```go
numeros := []int{1, 2, 3, 4, 5}
numeros = append(numeros, 6)
```

### Mapas

Mapas são coleções de pares chave-valor.

```go
idades := make(map[string]int)
idades["João"] = 30
idades["Maria"] = 25
fmt.Println(idades)
```

### Structs

Structs permitem criar tipos de dados compostos.

```go
type Pessoa struct {
    Nome string
    Idade int
}

joao := Pessoa{Nome: "João", Idade: 30}
fmt.Println(joao)
```

## Concor­rência

A concor­rência é uma das características mais destacadas de Go, implementada através de goroutines e canais.

### Goroutines

Goroutines são funções que são executadas em paralelo.

```go
go func() {
    fmt.Println("Olá de uma goroutine")
}()
```

### Canais

Canais são usados para comunicação entre goroutines.

```go
mensagens := make(chan string)

go func() {
    mensagens <- "Olá"
}()

msg := <-mensagens
fmt.Println(msg)
```

## Tratamento de Erros

No Go, o tratamento de erros é feito explicitamente, retornando erros como valores.

```go
file, err := os.Open("arquivo.txt")
if err != nil {
    log.Fatal(err)
}
defer file.Close()
```

## Ponteiros

Go suporta ponteiros, permitindo manipulação direta de endereços de memória.

```go
var x int = 10
var p *int = &x
fmt.Println(*p)  // Desreferenciação do ponteiro
```

## Interfaces

Interfaces são tipos que especificam um conjunto de métodos.

```go
type Desenhavel interface {
    Desenhar()
}

type Circulo struct{}

func (c Circulo) Desenhar() {
    fmt.Println("Desenhar círculo")
}

var d Desenhavel = Circulo{}
d.Desenhar()
```

## Pacotes

O Go organiza código em pacotes, e cada programa Go começa no pacote `main`.

### Criando um Pacote

Vamos criar um arquivo com seu código com a declaração do pacote.

```go
package minhaBiblioteca

func Saudacao() string {
    return "Olá do meu pacote"
}
```

### Usando um Pacote

```go
package main

import (
    "fmt"
    "minhaBiblioteca"
)

func main() {
    fmt.Println(minhaBiblioteca.Saudacao())
}
```
