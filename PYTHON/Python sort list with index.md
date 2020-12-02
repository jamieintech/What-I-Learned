# Python: sort list with index

> a quick how-to on sorting values of a list with while keeping the original index numbers

```python
# given list that I want to sort with the original index kept
scores = [75, 93, 89, 99, 72, 86, 96, 69, 86, 86]

# using enumerate to create a new list with (score, index)
result = [(score, idx+1) for idx, score in enumerate(scores)]
print(result)

# sort the result list based on the score values
result.sort(reverse=True)
print(result)
```

```bash
[(75, 1), (93, 2), (89, 3), (99, 4), (72, 5), (86, 6), (96, 7), (69, 8), (86, 9), (86, 10)]
[(99, 4), (96, 7), (93, 2), (89, 3), (86, 10), (86, 9), (86, 6), (75, 1), (72, 5), (69, 8)]
```

