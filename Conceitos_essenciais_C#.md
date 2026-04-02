# 📘 Guia Rápido — Conceitos Essenciais de C#

---

# 🧠 TIPOS (Value vs Reference)

## 🔹 Value Types

```csharp
int a = 10;
int b = a;
b = 20;

Console.WriteLine(a); // 10
```

## 🔹 Reference Types

```csharp
class Pessoa { public string Nome { get; set; } }

var p1 = new Pessoa { Nome = "Edu" };
var p2 = p1;
p2.Nome = "Outro";

Console.WriteLine(p1.Nome); // Outro
```

---

# 🧠 PROPRIEDADES

## 🔹 get / set

```csharp
public string Nome { get; set; }
```

## 🔹 private set

```csharp
public string Nome { get; private set; }
```

## 🔹 init (imutável após criação)

```csharp
public string Nome { get; init; }
```

---

# 🧠 CONSTRUTORES

```csharp
public class Produto
{
    public string Nome { get; }

    public Produto(string nome)
    {
        Nome = nome;
    }
}
```

---

# 🧠 NULL SAFETY

## 🔹 null check

```csharp
if (obj is null) throw new Exception();
```

## 🔹 null conditional

```csharp
var tamanho = texto?.Length;
```

## 🔹 null coalescing

```csharp
var nome = input ?? "default";
```

---

# 🧠 LISTAS E LINQ

## 🔹 Criar lista

```csharp
var lista = new List<int> { 1, 2, 3 };
```

## 🔹 Where

```csharp
var maiores = lista.Where(x => x > 1);
```

## 🔹 Select

```csharp
var dobrado = lista.Select(x => x * 2);
```

## 🔹 Sum

```csharp
var total = lista.Sum();
```

---

# 🧠 EXPRESSÕES LAMBDA

```csharp
x => x * 2
(x, y) => x + y
```

---

# 🧠 MÉTODOS

## 🔹 Método simples

```csharp
public int Somar(int a, int b)
{
    return a + b;
}
```

## 🔹 Expression body

```csharp
public int Somar(int a, int b) => a + b;
```

---

# 🧠 CLASSES vs RECORDS

## 🔹 Class

```csharp
public class Pessoa
{
    public string Nome { get; set; }
}
```

## 🔹 Record

```csharp
public record Pessoa(string Nome);
```

---

# 🧠 ENUM

```csharp
public enum StatusPedido
{
    Pendente,
    Pago,
    Cancelado
}
```

---

# 🧠 TRY / CATCH

```csharp
try
{
    var x = 10 / 0;
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
```

---

# 🧠 ASYNC / AWAIT

```csharp
public async Task<string> Buscar()
{
    await Task.Delay(1000);
    return "ok";
}
```

---

# 🧠 INTERFACES

```csharp
public interface IRepositorio
{
    void Salvar();
}
```

```csharp
public class Repositorio : IRepositorio
{
    public void Salvar() { }
}
```

---

# 🧠 INJEÇÃO DE DEPENDÊNCIA

```csharp
public class Service
{
    private readonly IRepositorio _repo;

    public Service(IRepositorio repo)
    {
        _repo = repo;
    }
}
```

---

# 🧠 CHECKLIST

## 🔹 Você precisa saber

* Tipos (value/reference)
* LINQ
* null safety
* async/await
* interfaces
* DI

---

# 💡 FRASE PRA LEMBRAR

"Estou lidando com valor ou referência?"

---

# 🧠 DELEGATES E EVENTS

## 🔹 Delegate (função como variável)

```csharp
public delegate int Operacao(int a, int b);

Operacao soma = (a, b) => a + b;
var resultado = soma(2, 3); // 5
```

## 🔹 Usando Func / Action (mais comum)

```csharp
Func<int, int, int> soma = (a, b) => a + b;
Action<string> log = msg => Console.WriteLine(msg);
```

## 🔹 Event (notificação)

```csharp
public class Pedido
{
    public event Action<string> AoFinalizar;

    public void Finalizar()
    {
        AoFinalizar?.Invoke("Pedido finalizado");
    }
}

var pedido = new Pedido();
pedido.AoFinalizar += msg => Console.WriteLine(msg);
pedido.Finalizar();
```

---

# 🧠 IEnumerable vs IQueryable

## 🔹 IEnumerable (memória)

```csharp
var lista = new List<int> {1,2,3,4};
var resultado = lista.Where(x => x > 2); // executa em memória
```

## 🔹 IQueryable (banco)

```csharp
var resultado = db.Produtos
    .Where(p => p.Preco > 10); // vira SQL
```

## 🔹 Diferença prática

```csharp
// ruim (traz tudo e filtra depois)
var lista = db.Produtos.ToList().Where(p => p.Preco > 10);

// bom (filtra no banco)
var lista = db.Produtos.Where(p => p.Preco > 10).ToList();
```

---

# 🧠 EXTENSION METHODS

## 🔹 Criando

```csharp
public static class StringExtensions
{
    public static bool EhValido(this string texto)
    {
        return !string.IsNullOrWhiteSpace(texto);
    }
}
```

## 🔹 Usando

```csharp
string nome = "Edu";
var valido = nome.EhValido();
```

---

# 🧠 PATTERN MATCHING AVANÇADO

## 🔹 Property Pattern

```csharp
if (produto is { Preco: > 100 })
{
    Console.WriteLine("Caro");
}
```

## 🔹 Relational Pattern

```csharp
if (numero is > 0 and < 10)
{
    Console.WriteLine("Entre 1 e 9");
}
```

## 🔹 Switch avançado

```csharp
var resultado = valor switch
{
    int i when i > 0 => "Positivo",
    int i when i < 0 => "Negativo",
    0 => "Zero",
    _ => "Outro"
};
```

---

# 🧠 DATAS E STRINGS (VIDA REAL)

## 🔹 Data atual

```csharp
var agora = DateTime.Now;
var utc = DateTime.UtcNow;
```

## 🔹 Formatação

```csharp
var data = DateTime.Now;
var texto = data.ToString("dd/MM/yyyy");
```

## 🔹 Parse

```csharp
var data = DateTime.Parse("2024-01-01");
```

## 🔹 TryParse (seguro)

```csharp
if (DateTime.TryParse(input, out var data))
{
    Console.WriteLine(data);
}
```

## 🔹 String

```csharp
var nome = "Edu";

nome.ToUpper();
nome.ToLower();
nome.Trim();
nome.Contains("du");
```

## 🔹 Interpolação

```csharp
var idade = 20;
var texto = $"Idade: {idade}";
```

---

# 🔥 DICA FINAL

Sempre pense:

* Isso roda em memória ou no banco?
* Isso pode quebrar com null?
* Isso pode ser reaproveitado?
