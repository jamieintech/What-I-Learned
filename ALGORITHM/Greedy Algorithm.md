# Greedy Algorithm

A **greedy algorithm** is an approach for solving a problem by selecting the **best option** available at the moment, without worrying about the future result it would bring.

In other words, the *locally best choices* aim at producing globally best results.

> This algorithm my not be the best option for all the problems. It may produce wrong results in some cases.

The greedy algorithm is a **top-down** approach.



## Feasible Solution

A feasible solution is the one that provides the **optimal solution** to the problem.



## Greedy Algorithm

1. Prepare and empty solution set / list.
2. At each step, an item is added into the solution set.
3. If the solution set is feasible, the current item is kept.
4. Else, the item is rejected and never considered again.



## Example [BOJ 2839]

상근이는 요즘 설탕공장에서 설탕을 배달하고 있다. 상근이는 지금 사탕가게에 설탕을 정확하게 N킬로그램을 배달해야 한다. 설탕공장에서 만드는 설탕은 봉지에 담겨져 있다. 봉지는 3킬로그램 봉지와 5킬로그램 봉지가 있다.

상근이는 귀찮기 때문에, 최대한 적은 봉지를 들고 가려고 한다. 예를 들어, 18킬로그램 설탕을 배달해야 할 때, 3킬로그램 봉지 6개를 가져가도 되지만, 5킬로그램 3개와 3킬로그램 1개를 배달하면, 더 적은 개수의 봉지를 배달할 수 있다.

상근이가 설탕을 정확하게 N킬로그램 배달해야 할 때, 봉지 몇 개를 가져가면 되는지 그 수를 구하는 프로그램을 작성하시오.

```python
import sys

N = int(sys.stdin.readline())

# 일단 5키로 봉지에 최대로 담아본다
fives = N//5

# 5키로 봉지에 꽉 채워서 담고 남은 거
left = N%5

# 전체 봉지의 합을 구할 cnt
cnt = 0

# 5키로 봉지를 아예 안쓰는 경우가 있을 때까지 돌려본다
while fives != -1:
    
    # 남은 설탕이 3의 배수면 끝
    if left%3 == 0:
        cnt = fives + left//3
        break
    
    # 남은 설탕이 3의 배수가 아니라면
    else:
        fives -= 1  #5키로 봉지 한개를 빼고
        left += 5   #5키로 만큼 남은 양에 추가해준다

# 중간에 break없이 끝났다 
# = 3키로 봉지로도 딱 채워서 못만든다
# = 딱 떨어지는 경우가 없다
if fives == -1:
    cnt = -1    # 안 되는 경우는 -1 리턴해야함

# 위의 if문에서 걸리지 않았다면 최종 cnt를 출력한다
print(cnt)
```

