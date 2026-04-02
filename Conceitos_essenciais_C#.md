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
