
# Roadmap Golang: Váriaveis no Go

O Golang, ou simplesmente Go, é uma linguagem de programação criada pelo Google em 2007. Foi projetada para ser simples, eficiente e altamente concorrente. Neste artigo, quero explicar e entender melhor as variáveis.

## Instalando o Golang

Antes de começar, é necessário instalar o Golang em seu sistema. Você pode baixar o instalador oficial no site [golang.org](https://golang.org/dl/). Após a instalação, verifique se tudo está funcionando corretamente executando o comando:

```bash
go version
```

Se tudo estiver correto, você verá a versão instalada do Go.

## Primeiro Programa em Go

Vamos começar com um simples programa "Hello, World!" para garantir que nosso ambiente está configurado corretamente.

Crie um arquivo chamado `main.go` e adicione o seguinte código:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

Para executar o programa, use o comando:

```bash
go run main.go
```

Você deve ver a mensagem "Hello, World!" no terminal.

## Variáveis em Go

Variáveis são essenciais em qualquer linguagem de programação, e Go oferece diversas formas de declarar e inicializar variáveis. Vamos ver algumas dessas formas.

### Declaração de Variáveis

A forma mais básica de declarar uma variável em Go é utilizando a palavra-chave `var`. Aqui está um exemplo:

```go
package main

import "fmt"

func main() {
    var nome string
    nome = "Alícia"
    fmt.Println(nome)
}
```

Neste exemplo, declaramos uma variável `nome` do tipo `string` e a inicializamos com o valor "Alícia".

### Declaração e Inicialização

Podemos simplificar a declaração e inicialização em uma única linha:

```go
package main

import "fmt"

func main() {
    var idade int = 25
    fmt.Println(idade)
}
```

### Inferência de Tipo

Go possui um recurso chamado inferência de tipo, onde o compilador deduz o tipo da variável com base no valor atribuído. Para isso, usamos o operador curto `:=`:

```go
package main

import "fmt"

func main() {
    altura := 1.75
    fmt.Println(altura)
}
```

Aqui, a variável `altura` é declarada e inicializada com o valor `1.75`, e o compilador infere que seu tipo é `float64`.

### Variáveis Múltiplas

Go permite declarar e inicializar múltiplas variáveis em uma única linha:

```go
package main

import "fmt"

func main() {
    var x, y, z int = 1, 2, 3
    fmt.Println(x, y, z)
}
```

Ou usando inferência de tipo:

```go
package main

import "fmt"

func main() {
    a, b, c := 4, 5.5, "hello"
    fmt.Println(a, b, c)
}
```

### Zero Values

Em Go, variáveis declaradas sem uma inicialização explícita recebem um valor padrão, chamado de "zero value". Estes valores são `0` para números, `false` para booleanos, e `""` (string vazia) para strings.

```go
package main

import "fmt"

func main() {
    var numero int
    var texto string
    var booleano bool

    fmt.Println(numero)   // 0
    fmt.Println(texto)    // ""
    fmt.Println(booleano) // false
}
```

## Tipos de Dados

Go suporta diversos tipos de dados, incluindo:

- **int**: números inteiros
- **float64**: números de ponto flutuante
- **string**: sequências de caracteres
- **bool**: valores booleanos (true/false)

### Exemplo Prático

Vamos criar um programa que utiliza diferentes tipos de variáveis e realiza operações básicas:

```go
package main

import "fmt"

func main() {
    var a int = 10
    var b float64 = 25.5
    var c string = "Go"
    var d bool = true

    fmt.Println("a:", a)
    fmt.Println("b:", b)
    fmt.Println("c:", c)
    fmt.Println("d:", d)

    // Operações básicas
    soma := a + int(b) // Convertendo b para int
    fmt.Println("Soma:", soma)
}
```

## Recaptulando

## Tipos de Variáveis

Go é uma linguagem estaticamente tipada, o que significa que cada variável deve ter um tipo definido em tempo de compilação. Aqui estão alguns dos tipos básicos:

1. **Tipos Numéricos**:
   - Inteiros: `int`, `int8`, `int16`, `int32`, `int64`
   - Flutuantes: `float32`, `float64`
   - Números complexos: `complex64`, `complex128`
   ```go
   var x int = 10
   var y float64 = 3.14
   ```

2. **Strings**:
   - Cadeias de caracteres são declaradas usando o tipo `string`.
   ```go
   var saudacao string = "Olá, mundo!"
   ```

3. **Booleanos**:
   - Variáveis booleanas podem ser `true` ou `false`.
   ```go
   var ativo bool = true
   ```

## Variáveis Compostas

1. **Arrays**:
   - Um array tem tamanho fixo e elementos do mesmo tipo.
   ```go
   var numeros [5]int
   numeros[0] = 10
   numeros[1] = 20
   ```

2. **Slices**:
   - Um slice é uma sequência dinâmica de elementos de um mesmo tipo.
   ```go
   var nomes []string
   nomes = append(nomes, "Carlos")
   nomes = append(nomes, "Ana")
   ```

3. **Maps**:
   - Um map é uma coleção de pares chave/valor.
   ```go
   var idadePorNome map[string]int
   idadePorNome = make(map[string]int)
   idadePorNome["Carlos"] = 30
   idadePorNome["Ana"] = 25
   ```

## Constantes

Além das variáveis, Go permite a definição de constantes que não podem ser alteradas após a inicialização.
```go
const pi = 3.14159
const nome = "Golang"
```

## Exemplos Práticos

Vamos ver um exemplo prático que utiliza diversos tipos de variáveis e suas operações:
```go
package main

import "fmt"

func main() {
    // Declaração de variáveis
    var a int = 10
    var b float64 = 3.14
    var c string = "Go"
    var d bool = true

    // Declaração curta
    e := 42

    // Arrays
    var arr [3]int
    arr[0] = 1
    arr[1] = 2
    arr[2] = 3

    // Slices
    slc := []string{"apple", "banana"}
    slc = append(slc, "cherry")

    // Maps
    idadePorNome := make(map[string]int)
    idadePorNome["Alice"] = 28
    idadePorNome["Bob"] = 34

    // Constantes
    const pi = 3.14159

    // Saída
    fmt.Println(a, b, c, d, e)
    fmt.Println(arr)
    fmt.Println(slc)
    fmt.Println(idadePorNome)
    fmt.Println("O valor de pi é", pi)
}
```

## Boas Práticas

1. **Use nomes descritivos**: Nomes de variáveis devem ser claros e descrever seu propósito.
2. **Evite variáveis globais**: Prefira variáveis locais e passe-as como parâmetros para funções sempre que possível.
3. **Considere a imutabilidade**: Sempre que possível, use constantes para valores que não devem mudar.
