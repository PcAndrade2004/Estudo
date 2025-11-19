
Para validar um salário informado pelo usuário em C#, é necessário garantir dois pontos fundamentais:

1. **A entrada não pode ser nula ou vazia**.
    
2. **O valor deve ser numérico válido**, ou seja, capaz de ser convertido para um tipo numérico (ex.: `decimal`).
    

A combinação ideal é:

- Verificar se a string não é nula/ vazia (`string.IsNullOrWhiteSpace`).
    
- Em seguida usar `decimal.TryParse` para validar e converter a entrada.
    

### Padrão recomendado

```csharp
var entrada = Console.ReadLine();

if (!string.IsNullOrWhiteSpace(entrada) &&
    decimal.TryParse(entrada, out decimal salario))
{
    Console.WriteLine($"Salário válido: {salario}");
}
else
{
    Console.WriteLine("Entrada inválida. Digite um salário numérico.");
}
```

### Por que este padrão é o ideal?

- Evita exceções em tempo de execução.
    
- Garante que valores nulos, vazios ou apenas espaços sejam descartados antes da conversão.
    
- `TryParse` impede quebra do programa ao lidar com caracteres inválidos.
    
- `decimal` é o tipo mais apropriado para valores monetários.
    
.