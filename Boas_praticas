# 📘 Boas Práticas no .NET (Guia Rápido)

---

# 🧠 ORGANIZAÇÃO DE PROJETO

## 🔹 Estrutura básica

```
/src
  /Domain
  /Application
  /Infrastructure
  /API
```

## 🔹 Regra

* Domain não depende de ninguém
* Infrastructure depende de Domain
* API depende de tudo

---

# 🧠 NOMENCLATURA

## 🔹 Boas práticas

```csharp
// Classes
public class PedidoService {}

// Métodos
public void CriarPedido() {}

// Variáveis
var totalPedido = 10;
```

## ❌ Evitar

```csharp
var x = 10;
```

---

# 🧠 MÉTODOS

## 🔹 Pequenos e objetivos

```csharp
public void CriarPedido()
{
    Validar();
    Salvar();
}
```

## ❌ Evitar método gigante

---

# 🧠 VALIDAÇÃO

## 🔹 Sempre validar entrada

```csharp
if (string.IsNullOrWhiteSpace(nome))
    throw new ArgumentException("Nome inválido");
```

---

# 🧠 IMUTABILIDADE

## 🔹 Preferir

```csharp
public string Nome { get; private set; }
```

## 🔹 Ou

```csharp
public string Nome { get; init; }
```

---

# 🧠 EXCEÇÕES

## 🔹 Usar quando necessário

```csharp
throw new Exception("Erro");
```

## ❌ Evitar

* Usar exceção como fluxo normal

---

# 🧠 LINQ

## 🔹 Boa prática

```csharp
var ativos = lista.Where(x => x.Ativo).ToList();
```

## ❌ Evitar múltiplos ToList()

---

# 🧠 EF CORE

## 🔹 Sempre filtrar no banco

```csharp
var produtos = db.Produtos
    .Where(p => p.Preco > 10)
    .ToList();
```

## ❌ Evitar

```csharp
var produtos = db.Produtos.ToList().Where(p => p.Preco > 10);
```

---

# 🧠 DEPENDENCY INJECTION

## 🔹 Usar via construtor

```csharp
public class Service
{
    private readonly IRepo _repo;

    public Service(IRepo repo)
    {
        _repo = repo;
    }
}
```

---

# 🧠 SEPARAÇÃO DE RESPONSABILIDADE

## 🔹 Regra

* Controller → recebe requisição
* Service → regra de negócio
* Repository → acesso a dados

---

# 🧠 NULL SAFETY

## 🔹 Sempre tratar

```csharp
if (obj is null) throw new Exception();
```

---

# 🧠 LOG

## 🔹 Sempre logar erros

```csharp
_logger.LogError("Erro ao salvar");
```

---

# 🧠 ASYNC/AWAIT

## 🔹 Usar corretamente

```csharp
public async Task<List<Produto>> Buscar()
{
    return await db.Produtos.ToListAsync();
}
```

## ❌ Evitar

* .Result
* .Wait()

---

# 🧠 CÓDIGO LIMPO

## 🔹 Regras

* Nomes claros
* Métodos pequenos
* Sem código morto

---

# 🔥 REGRAS DE OURO

* Código simples > código complexo
* Clareza > esperteza
* Legível > inteligente

---

# 💡 FRASE FINAL

"Se outro dev olhar e entender rápido, está bom."
