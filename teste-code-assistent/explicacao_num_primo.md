# Algoritmo de Verificação de Números Primos

## Introdução
Um número primo é um número inteiro maior que 1 que possui apenas dois divisores positivos: 1 e ele mesmo. Por exemplo, 2, 3, 5, 7, 11 são primos. O algoritmo implementado em `pratica1.py` verifica se um número dado é primo de forma eficiente.

## Algoritmo Básico
A versão básica do algoritmo verifica se o número `n` é divisível por qualquer inteiro de 2 até `n-1`. Se encontrar um divisor, retorna `False`; caso contrário, `True`. No entanto, essa abordagem é ineficiente para números grandes, com complexidade de tempo O(n).

## Algoritmo Otimizado
A versão otimizada inclui as seguintes melhorias:
- Trata casos especiais: números ≤ 1 não são primos, 2 é primo, números pares > 2 não são primos.
- Verifica divisibilidade apenas por números ímpares de 3 até a raiz quadrada de `n` (inclusive).

### Código da Função Otimizada
```python
def is_prime_optimized(n):
    if n <= 1:
        return False
    if n == 2:
        return True
    if n % 2 == 0:
        return False
    for i in range(3, int(n**0.5) + 1, 2):
        if n % i == 0:
            return False
    return True
```

## Por que Verificar Apenas Até a Raiz Quadrada?
A otimização principal vem da verificação de divisores apenas até √n. Isso é possível devido a uma propriedade matemática fundamental:

- Se um número `n` não é primo, ele pode ser expresso como `n = d * d'`, onde `d` e `d'` são inteiros > 1.
- Pelo menos um dos fatores (`d` ou `d'`) deve ser ≤ √n.
- Se `n` tem um divisor `d` > √n, então o outro divisor `d'` = `n / d` deve ser < √n (já que `d * d'` = n e d > √n implica d' < √n).
- Portanto, verificando apenas até √n, cobrimos todos os possíveis divisores.

Essa abordagem reduz drasticamente o número de verificações. Para um número grande `n`, em vez de verificar até `n-1` (O(n)), verificamos apenas até √n (O(√n)), o que é uma melhoria exponencial na eficiência.

Por exemplo:
- Para n = 10^6, a versão básica faria ~10^6 verificações.
- A otimizada faz apenas ~10^3 verificações (√10^6 = 10^3).

Isso torna o algoritmo viável para números muito grandes, mantendo a corretude.