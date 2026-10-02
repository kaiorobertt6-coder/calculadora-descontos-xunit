# Calculadora de Descontos — xUnit

O objetivo da atividade é implementar métodos para cálculo de descontos e elegibilidade de clientes e validar seu funcionamento por meio de **testes unitários parametrizados utilizando xUnit**.

## Métodos Implementados

A classe `DescontoService` possui três métodos:

### `ObterCategoriaCliente`

```csharp
ObterCategoriaCliente(int totalCompras)
```

Retorna a categoria do cliente de acordo com a quantidade de compras:

* Menos de 5 compras → `BRONZE`
* De 5 a 10 compras → `PRATA`
* Mais de 10 compras → `OURO`

### `CalcularDescontoPorPercentual`

```csharp
CalcularDescontoPorPercentual(int valorOriginal, int percentualDesconto)
```

Calcula o valor final de uma compra após aplicar o percentual de desconto.

Exemplos:

```text
100 com 10% de desconto → 90
200 com 20% de desconto → 160
50 com 0% de desconto → 50
```

### `EValidoParaCupom`

```csharp
EValidoParaCupom(int idade, bool primeiraCompra)
```

Verifica se o cliente pode utilizar o cupom.

O retorno será `true` quando:

* O cliente tiver 18 anos ou mais; **ou**
* For a primeira compra.

Caso nenhuma dessas condições seja atendida, o retorno será `false`.

---

## Testes Parametrizados com xUnit

Os testes foram implementados na classe `DescontoServiceTests`.

Nesta atividade foi utilizado o atributo `[Theory]` juntamente com `[InlineData]`.

### Diferença entre `[Fact]` e `[Theory]`

#### `[Fact]`

O `[Fact]` é utilizado quando o teste possui **um cenário fixo**, sem necessidade de receber diferentes valores de entrada.

Exemplo:

```csharp
[Fact]
public void ExemploDeTeste()
{
    // teste com valores definidos diretamente
}
```

Cada método marcado com `[Fact]` representa um teste independente.

#### `[Theory]`

O `[Theory]` é utilizado quando o mesmo teste precisa ser executado com **diferentes conjuntos de dados**.

Os valores são fornecidos através do `[InlineData]`.

Exemplo:

```csharp
[Theory]
[InlineData(2, "BRONZE")]
[InlineData(7, "PRATA")]
[InlineData(15, "OURO")]
public void ObterCategoriaCliente_DeveRetornarCategoriaCorreta(
    int totalCompras,
    string categoriaEsperada)
{
    // teste
}
```

Nesse caso, o xUnit executa o mesmo método de teste três vezes, uma para cada `[InlineData]`.

### Resumindo

| Atributo       | Utilização                                          |
| -------------- | --------------------------------------------------- |
| `[Fact]`       | Teste com cenário/valores fixos                     |
| `[Theory]`     | Teste que recebe diferentes conjuntos de dados      |
| `[InlineData]` | Fornece os valores para cada execução do `[Theory]` |

Nesta atividade, os testes foram parametrizados para evitar a duplicação de métodos de teste e permitir a validação de diferentes cenários.

## Cobertura dos Testes

Foram utilizados três métodos de teste com `[Theory]`, cada um contendo três `[InlineData]`.

### Categorias de cliente

```csharp
[InlineData(2, "BRONZE")]
[InlineData(7, "PRATA")]
[InlineData(15, "OURO")]
```

### Cálculo de desconto

```csharp
[InlineData(100, 10, 90)]
[InlineData(200, 20, 160)]
[InlineData(50, 0, 50)]
```

### Elegibilidade para cupom

```csharp
[InlineData(20, false, true)]
[InlineData(16, true, true)]
[InlineData(17, false, false)]
```

Ao todo, são **9 casos de teste executados pelo xUnit**.

## Como Executar os Testes

Abra o terminal na pasta raiz da solução e execute:

```bash
dotnet test
```

O comando irá compilar os projetos e executar automaticamente todos os testes unitários.

Como existem 3 métodos com 3 `[InlineData]` cada, serão executados **9 casos de teste**.

O resultado esperado é:

```text
Total: 9
Aprovados: 9
Falhos: 0
```
## Autor

**Kaio Moreira**

Projeto acadêmico desenvolvido para a disciplina de **Garantia e Qualidade de Software**.
