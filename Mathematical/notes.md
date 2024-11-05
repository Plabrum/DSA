12. **Sieve of Eratosthenes (Prime Numbers)**:  
     An efficient algorithm to find all prime numbers up to a specified limit by iteratively marking the multiples of each prime starting from 2, leaving only primes unmarked.

### 12. Sieve of Eratosthenes (Prime Numbers)

```python
def sieve_of_eratosthenes(n):
    sieve = [True] * (n+1)
    sieve[0] = sieve[1] = False

    for i in range(2, int(n**0.5) + 1):
        if sieve[i]:
            for j in range(i*i, n+1, i):
                sieve[j] = False

    return [i for i in range(n+1) if sieve[i]]
```
