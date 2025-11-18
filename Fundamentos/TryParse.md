A seguir está uma explicação completa, clara e prática sobre **TryParse**, adequada para quem está estudando C#, validação de dados e controle de fluxo.

---

# **Explicação Completa: TryParse em C#**

`TryParse` é um método presente nos tipos numéricos e em outros tipos estruturados (como `int`, `double`, `decimal`, `DateTime`, `Guid`, entre outros).  
Ele serve para **tentar converter** uma string para um tipo específico **de forma segura**, evitando exceções.

---

## **1. Por que TryParse existe?**

Métodos como `int.Parse()` ou `decimal.Parse()` lançam exceção se o usuário digitar algo inválido:

```csharp
int valor = int.Parse("abc");   // ERRO: FormatException
```

Para aplicações que recebem entrada do usuário (console, API, formulários), depender de exceções é ruim.

Por isso existe o **TryParse**, que NÃO lança exceção; ele retorna um **bool**:

- `true` → conversão bem-sucedida
    
- `false` → conversão inválida
    

---

## **2. Forma geral do TryParse**

```csharp
Tipo.TryParse(string entrada, out Tipo valorConvertido);
```

Exemplos:

```csharp
int.TryParse("10", out int numero);
decimal.TryParse("100.50", out decimal preco);
DateTime.TryParse("2025-01-01", out DateTime data);
```

---

## **3. Como TryParse funciona internamente?**

1. Recebe uma string.
    
2. Valida formato, cultura, caracteres e faixa numérica.
    
3. Se válido:
    
    - Retorna **true**
        
    - Atribui o valor convertido ao `out`.
        
4. Se inválido:
    
    - Retorna **false**
        
    - O `out` recebe **0**, `DateTime.MinValue`, ou um valor padrão.
        

---

## **4. Exemplo prático: entrada do usuário**

```csharp
Console.Write("Digite um número: ");
var entrada = Console.ReadLine();

if (int.TryParse(entrada, out int numero))
{
    Console.WriteLine($"Número válido: {numero}");
}
else
{
    Console.WriteLine("Número inválido.");
}
```

---

## **5. TryParse evita exceções**

Este código **nunca** quebra execução:

```csharp
int.TryParse("abc", out int n);  // Retorna false, n = 0
```

Já este pode quebrar:

```csharp
int n = int.Parse("abc");       // FormatException
```

---

## **6. TryParse com validação de nulo/vazio**

Recomendado para programas reais:

```csharp
if (!string.IsNullOrWhiteSpace(entrada) &&
    decimal.TryParse(entrada, out decimal salario))
{
    // OK
}
else
{
    // entrada inválida
}
```

---

## **7. Por que usar decimal.TryParse para dinheiro?**

Porque `decimal` é o tipo mais preciso para valores monetários.

---

## **8. TryParse com cultura (opcional para controlar vírgula/ponto)**

```csharp
decimal.TryParse(
    entrada, 
    NumberStyles.Number, 
    CultureInfo.InvariantCulture, 
    out decimal valor
);
```

Útil em casos onde o formato precisa ser sempre com ponto como separador.

---

## **9. Resumo direto**

- **TryParse = conversão segura + retorno booleano**.
    
- Evita exceções.
    
- Ideal para entradas do usuário.
    
- Usa parâmetro `out` para entregar o valor convertido.
    
- Sempre escolha `decimal` para valores monetários.
    

---

Se quiser, posso criar um **PDF resumido** sobre TryParse ou gerar **exercícios** para treinar.