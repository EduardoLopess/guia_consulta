# 📘 Guia Rápido — DDD + C# + EF Core

---

# 🧠 VALUE OBJECT (VO)

## 🔹 Conceito

* Representa um conceito sem identidade
* Comparado por valor
* Deve ser imutável

## 🔹 Quando usar

* Tem regras próprias
* Não precisa de ID
* Representa algo como: Preço, Endereço

## 🔹 Quando NÃO usar

* Precisa de identidade
* Precisa ser alterado constantemente
* Precisa ser buscado sozinho no banco

## 🔹 Exemplo padrão (com validação)

```csharp
public record Preco
{
    public decimal Valor { get; }

    public Preco(decimal valor)
    {
        if (valor < 0)
            throw new ArgumentException("Preço inválido");

        Valor = valor;
    }

    public static Preco Criar(decimal valor)
    {
        return new Preco(valor);
    }
}
```

## 🔹 VO composto

```csharp
public record Cep(string Valor)
{
    public Cep(string valor) : this()
    {
        if (valor.Length != 8)
            throw new ArgumentException("CEP inválido");
        Valor = valor;
    }
}

public record Endereco(string Rua, string Cidade, Cep Cep);
```

## 🔹 Uso na entidade

```csharp
public class Produto
{
    public int Id { get; set; }
    public Preco Preco { get; private set; }

    public void AlterarPreco(decimal novoPreco)
    {
        Preco = new Preco(novoPreco);
    }
}
```

## 🔹 EF Core

```csharp
modelBuilder.Entity<Produto>()
    .OwnsOne(p => p.Preco);
```

## 🔹 Erros comuns

* Usar get/set público
* Permitir valor inválido
* Criar VO sem regra
* Tratar VO como entidade

---

# 🧠 ENTITY

## 🔹 Conceito

* Possui identidade (ID)
* Comparado por identidade
* Pode mudar estado

## 🔹 Exemplo completo

```csharp
public class Produto
{
    public int Id { get; private set; }
    public string Nome { get; private set; }
    public Preco Preco { get; private set; }

    public Produto(string nome, decimal preco)
    {
        Nome = nome;
        Preco = new Preco(preco);
    }

    public void AlterarNome(string nome)
    {
        if (string.IsNullOrWhiteSpace(nome))
            throw new Exception("Nome inválido");

        Nome = nome;
    }
}
```

---

# 🧠 RECORD vs CLASS

## 🔹 Record

```csharp
public record Preco(decimal Valor);
```

## 🔹 Class

```csharp
public class Preco
{
    public decimal Valor { get; set; }
}
```

## 🔹 Comparação

```csharp
var p1 = new Preco(10);
var p2 = new Preco(10);

Console.WriteLine(p1 == p2); // true (record)
```

---

# 🧠 PATTERN MATCHING

## 🔹 Exemplo básico

```csharp
if (obj is string texto)
{
    Console.WriteLine(texto);
}
```

## 🔹 Com condição

```csharp
if (obj is int numero && numero > 10)
{
    Console.WriteLine("Maior que 10");
}
```

## 🔹 Switch moderno

```csharp
string resultado = obj switch
{
    int i => $"Número {i}",
    string s => $"Texto {s}",
    _ => "Outro"
};
```

---

# 🧠 EF CORE — OWNED TYPES

## 🔹 Configuração

```csharp
modelBuilder.Entity<Pedido>()
    .OwnsOne(p => p.Endereco);
```

## 🔹 Entidade exemplo

```csharp
public class Pedido
{
    public int Id { get; set; }
    public Endereco Endereco { get; set; }
}
```

---

# 🧠 AGGREGATE

## 🔹 Exemplo

```csharp
public class Pedido
{
    public int Id { get; private set; }
    private readonly List<ItemPedido> _itens = new();

    public IReadOnlyCollection<ItemPedido> Itens => _itens;

    public void AdicionarItem(string nome, decimal preco)
    {
        _itens.Add(new ItemPedido(nome, preco));
    }
}

public class ItemPedido
{
    public string Nome { get; private set; }
    public Preco Preco { get; private set; }

    public ItemPedido(string nome, decimal preco)
    {
        Nome = nome;
        Preco = new Preco(preco);
    }
}
```

---

# 🧠 DOMAIN SERVICE

## 🔹 Exemplo

```csharp
public class CalculoPedidoService
{
    public decimal CalcularTotal(Pedido pedido)
    {
        return pedido.Itens.Sum(i => i.Preco.Valor);
    }
}
```

---

# 🧠 CHECKLIST BACKEND C#

## 🔹 Sintaxe importante

```csharp
// LINQ
var total = lista.Sum(x => x.Preco);

// null check
if (obj is null) throw new Exception();

// init only
public string Nome { get; init; }
```

---

# 🔥 REGRAS DE OURO

* Se tem ID → Entity
* Se é valor → VO
* Se depende de outro → composição
* Se regra envolve vários → Domain Service

---

# 💡 FRASE PRA LEMBRAR

"Isso aqui é um valor ou uma identidade?"

Se for valor → VO
Se for identidade → Entity
