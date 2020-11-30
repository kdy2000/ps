[Olympiad](https://www.acmicpc.net/category/2) > [USA Computing Olympiad](https://www.acmicpc.net/category/106) > [2019-2020 Season](https://www.acmicpc.net/category/470) > [USACO 2020 January Contest](https://www.acmicpc.net/category/472) > [Silver](https://www.acmicpc.net/category/detail/2151) 3번

## Wormhole sort
### description
n 마리의 소가 존재한다. 각각의 소는 1~n 사이의 번호를 가지고 있다. (번호는 모두 다르다.) 

n 마리의 소가 1차원 배열에 서로 뒤섞여서 존재한다. 이들은 정렬시켜서, i 번 소가 i 번 위치에 오도록 하고 싶다.

정렬은 swap 을 통해서만 이루어진다. swap 할 수 있는 위치는 고정되어 있다. a, b, w 로써 표시된다. a 번 위치와 b번 위치에 있는 한쌍의 소를 swap할수 있다는 뜻이다. 이때 cost는 w 이다.

swap 가능한 쌍은 총 m개가 주어진다. 그리고 항상 정렬이 가능하다. 

몇번을 swap 해도 상관없다. 정렬을 시키기 위해 사용한 swap의 cost 들 중, 가장 작은 값을, 최대로 하면 된다.

### constraint
1 <= n <= 1e5
1 <= m <= 1e5
1 <= w <= 1e9

### solution
솔루션을 바로 내고도, 시간복잡도 계산을 아주 잘못생각해서 다른 솔루션을 계속 찾느라 시간을 낭비한 문제이다. (정신머리를 챙겨야 한다.)

답에 대하여 바이너리 서치를 하면된다. 사용된 가장 작은 cost 를 bound 라고 하겠다. bound 이상인 edge를 전부 사용한다고 생각하고, (**i 번 소가 현재위치한 번호**, **i 번**) 이 connect 되어 있는지 확인하면 된다. 만약 connect되어 있지 않다면, false를 return 한다.

\* i 번 소는 현재 어디있건 상관없이, i 번 position으로 가야한다. 어떻게 가든지 상관없다. 현재위치에서 목표까지 갈 수 있기만 하면 되는것이다. (cost 가 bound이상인것들만 사용해서 말이다.) 즉, i 번 소가 현재 위치한 곳과, i 번 노드가 서로 **연결** 되어 있기만 하면 된다는 것이다.

\* bound이상인 edge들을 사용해서 node들을 union시켜준뒤, 연결되어 있는지 확인하기 위해서 find를 사용해다. (union-find)

\* 근데 정해를 보니, 굳이 union-find까지 가지 않고, bound이상인 edge들만 탐색하도록 dfs를 구현했었었다. 

