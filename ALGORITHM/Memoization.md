# Memoization

Memoization is a technique used in computing to speed up programs. This is done by caching the outputs of a function for future use (=memorizing the calculation results of function calls)

> What is Caching?
>
> In computing, a cache is a high-speed data storage layer which stores a subset of data, typically transient in nature, so that future requests for that data are served up faster than is possible by accessing the data’s primary storage location. Caching allows you to efficiently reuse previously retrieved or computed data.
>
> [AWS Caching Overview](https://aws.amazon.com/caching/?nc1=h_ls)

If the same input of a function call with the same parameters is used, the previously stroed results can be used again an unnecssary calculations are avoided.

<br>

## Example (factorial)

```python
factorial_memo = {}

def factorial(n):
    if n<2:
        return 1
    if n not in factorial_memo:
        factorial_memo[n] = n * factorial(n-1)
    return factorial_memo[n]

n = 5
print(factorial(n))
```

### How it works

![Factorial Memoization](https://user-images.githubusercontent.com/53888115/97662447-7a1ea500-1aba-11eb-960a-ccf73d25c9a7.gif)
