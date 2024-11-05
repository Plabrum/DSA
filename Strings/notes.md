13. **Rabin-Karp Algorithm (String Matching)**:  
    A string searching algorithm that uses hashing to find any occurrence of a pattern in a text. It calculates hash values for the pattern and substrings of the text, allowing quick comparisons.

### 13. Rabin-Karp Algorithm (String Matching)

```python
def rabin_karp(pattern, text, prime=101):
    d, p_len, t_len = 256, len(pattern), len(text)
    p_hash = t_hash = 0
    h = 1

    for i in range(p_len-1):
        h = (h * d) % prime

    for i in range(p_len):
        p_hash = (d * p_hash + ord(pattern[i])) % prime
        t_hash = (d * t_hash + ord(text[i])) % prime

    for i in range(t_len - p_len + 1):
        if p_hash == t_hash and pattern == text[i:i+p_len]:
            return i
        if i < t_len - p_len:
            t_hash = (d * (t_hash - ord(text[i]) * h) + ord(text[i + p_len])) % prime
            if t_hash < 0:
                t_hash += prime

    return -1
```

9. **Knuth-Morris-Pratt Algorithm (String Matching)**:  
   A string searching algorithm that searches for occurrences of a "pattern" within a "text" by preprocessing the pattern to create a partial match table, allowing the search to skip sections of the text for faster matching.

### 9. Knuth-Morris-Pratt Algorithm (String Matching)

```python
def kmp(pattern, text):
    def compute_lps(pattern):
        lps = [0] * len(pattern)
        length, i = 0, 1

        while i < len(pattern):
            if pattern[i] == pattern[length]:
                length += 1
                lps[i] = length
                i += 1
            elif length > 0:
                length = lps[length - 1]
            else:
                lps[i] = 0
                i += 1
        return lps

    lps = compute_lps(pattern)
    i = j = 0

    while i < len(text):
        if pattern[j] == text[i]:
            i += 1
            j += 1

        if j == len(pattern):
            return i - j
        elif i < len(text) and pattern[j] != text[i]:
            if j != 0:
                j = lps[j - 1]
            else:
                i += 1
    return -1
```
