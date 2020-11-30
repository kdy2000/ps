> own thinking 
> 문제가 존재하지 않거나, 테케를 만들어서 테스트 해보지 않았기 때문에, 정확성은 담보하지 못합니다.
> 그냥 개인적인 잡생각이라고 보시면 될 것 같습니다. 본문에 대한 의견이 있으시다면, 얘기해주시면 감사하겠습니다.

## disjoint-set subgroup problem
말 그대로이다. 그래프가 있다고 해보자. 이 그래프들의 connectivity에 따라서 노드들을 분할할 수 있겠다. 이렇게 분할된 그룹들 (disjoint-set) 이 있다면, 이 group을 포함하는 상위 group을 어떻게 proper하다고 판별할 수 있을까? 라는 생각에서 출발하였다.

```
ex.
set group G1
set A = {1, 2, 3}
set B = {4, 5, 6}
set C = {7, 8, 9}
    
set group G2
set A = {1, 2, 3, 4, 5, 6}
set B = {7, 8, 9}    

G1은 G2의 subgraph라고 할 수 있겠다.
(비교되는 그룹들은, 동일한 original set을 분할했다고 가정한다.)
```
### solution 1
가장 처음에 한 생각은 union-find로 해결해야겠다는 것이었다. 그리고 생각을 발전시킨 것에 대한 결과물을 소개한다. 1 ~ n 에 대해서, G1, G2 각각 parent array 를 적절히 만들어서, disjoint-set을 구현한다. 그리고 그 다음 아래처럼 동작한다.
```
/* 
G1 이 G2의 subgraph인지 판단하는 것이다.
첫번째 반복문에서는, G1에서 i번 node가 G2와 동일한 set에 속하도록 만들어주는 것이다. 만약 subgraph가 아니라면, 이미 지나온 1 ~ i-1 까지의 parent가 적절하게 유지되지 않을것이다. 
두번째 반복문에서는, 수정된 G1과 G2가 동일한지 파악한다. 동일하면, G1은 subgraph였던 것이다.

for(int i = 1; i <= n; i++){
    int r1 = findG1(i);
    int r2 = findG2(i);
    mergeG1(i, r2);
}

int ans = true;
for(int i = 1; i <= n; i++){
    if(findG1(i) != findG2(i)){
        ans = false;
    }
}
if(ans) printf("G1 is subgroup of G2\n");
else printf("G1 is not subgroup of G2\n");

```

### solution 2
사실 이게 정답인거 같다. subgraph 의 수학적 정의가 무엇인지 생각해보았었다. 정의 = 솔루션 이었다.
$$
G1 is subgroup of G2 := G1 에서 같은 set에 분류되어 있는 노드들은, G2에서도 같다. 
$$
정말 이게 다다. 이 글자를 보지 말고, 머릿속으로, subgroup 관계 에 있는 두개의 group을 생각해보라. 딱 이게 답이다. 이렇게 되면 구현도 정말 간단하다. g1[N], g2[N]이 각각 disjoint-set 을 나타낸다고 해보자. ( g1[i] = j <-> G1에서 i 번째 node는 j 라는 set에 속한다.)
```
int ans = true;
int direct[N] = {0, };
for(int i = 1; i <= n; i++){
        if(direct[g1[i]] == 0){
            direct[g1[i]] = g2[i];
        }
        else if(direct[g1[i]] != g2[i]){
            ans = false;
        }
 }
 return ans;
 ```

> c. f. 여기서 작성한 코드는 확인해보지 않은 코드입니다. 




