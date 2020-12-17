# Tree Traversals (Inorder, Preorder and Postorder)

> 1 ~ 7까지 있는 이진트리를 순회해보자

## Preorder | 전위순회

```python
def preOrder(n):
    if n >7:
        return
    else:
        print(n, end=' ')
        preOrder(2*n)
        preOrder(2*n+1)
```

- 전위순회: 내 일 먼저 => Left => Right
- 결과: `1 2 4 5 3 6 7 `



## Inorder | 중위순회

```python
def inOrder(n):
    if n>7:
        return
    else:
        inOrder(2*n)
        print(n, end=' ')
        inOrder(2*n+1)
```

- 중위순회: Left => 내 일 => Right
- 결과: `4 2 5 1 6 3 7 `



## Postorder | 후위순회

```python
def postOrder(n):
    if n>7:
        return
    else:
        postOrder(2*n)
        postOrder(2*n+1)
        print(n, end=' ')
```

- 후위순회: Left => Right => 내 일
- 결과: `4 5 2 6 7 3 1`