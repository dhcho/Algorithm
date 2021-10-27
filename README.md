# 시간 복잡도란?


아래에 1부터 N까지 자연수의 합을 구하는 두 개의 코드가 있습니다.

```
int sum = 0;
for(int i=1; i<=N; i++)
    sum += i;
```


```
int sum = (N+1)*N/2;
```


첫번째 코드는 1부터 N까지 반복문을 돌면서 합을 직접 계산하고, 두번째 코드는 등차수열의 합 공식을 통해 합을 계산합니다.

두 코드 중 어느 코드가 더 시간적인 측면에서 효율적일까요?
…

당연히 두번째 코드가 훨씬 더 시간적인 측면에서 효율적입니다.

그렇다면, 왜 아래의 코드가 위의 코드보다 효율적이라고 말할 수 있을까요?

코드가 짧아서? 반복문이 없어서?

이러한 의문을 해결해 주는 것이 바로 시간 복잡도입니다.

시간 복잡도는 기본적인 연산을 수행하는데에 어떤 고정된 시간이 걸릴 때, 알고리즘에 의해서 수행되는 기본 연산의 개수를 세어 예측할 수 있다. 그러므로 걸리는 시간의 총량과 알고리즘에 의해 수행되
는 기본적인 연산의 개수는 최대 상수 인자만큼 다르다. 

##### -위키피디아, 시간 복잡도 정의 中


즉, 시간 복잡도는 연산의 개수를 세어 얼마만큼의 연산이 수행되는가를 통해 로직의 효율을 분석하는데 사용됩니다.

위의 코드를 다시 봅시다.

```
int sum = 0;
for(int i=1; i<=N; i++)
    sum += i;
```


```
int sum = (N+1)*N/2;
```

첫번째 코드는 반복문 안에서만 세어도 N 번의 계산이 필요한 반면, 두번째 코드는 네 번의 계산만으로 1부터 N까지의 합을 구합니다. (어디까지나 대략적인 수치입니다.)

두번째 코드가 첫번째 코드보다 연산의 개수가 적으므로(N≥5), 두번째 코드는 첫번째 코드보다 더 작은 시간 복잡도를 가집니다. 때문에 두번째 코드가 첫번째 코드보다 시간적인 측면에서 효율적이라고 말 할 수 있습니다.

시간 복잡도의 계산은 복잡하게 하려면 얼마든지 복잡하게 할 수 있고, 간단하게 하려면 얼마든지 간단하게 할 수 있습니다.

위의 예시처럼 코드의 모든 연산의 개수를 세어 계산하는 방법과 비교를 통해 계산하는 방법이 있는데, 보통은 비교를 통해 시간 복잡도를 계산합니다.


## 시간 복잡도의 종류

시간 복잡도는 크게 O(Big-O), Ω(Omega), Θ(Theta) 라고 불리는 3가지의 표기법을 가지고 있습니다.

입력의 크기 n이 주어질 때, n에 따른 연산의 개수를 f(n), 비교의 기준이 되는 함수를 g(n)이라고 정의합니다.

Big-O 표기법은 점근적 상한(Asymptotic Upper Bound)를 의미합니다.

f(n)이 n0보다 크거나 같은 모든 n에서 0 이상이고 cg(n) 이하이면,
O(g(n)) = f(n) 입니다.
ex) 3n+1 = O(n), n0 ≥1, c =4에서 0 ≤ 3n+1 ≤ 4n 이다.

Ω 표기법은 점근적 하한(Asymptotic Lower Bound)를 의미합니다.
f(n)이 n0보다 크거나 같은 모든 n에서 0 이상이고 cg(n) 이상이면,
Ω(g(n)) = f(n) 입니다.
ex) 3n²-4n+1 = Ω(n²), n0 ≥2, c =2에서 0 ≤ 2n² ≤ 3n²-4n+1 이다.

Θ 표기법은 점근적 상한과 하한의 교집합(Asymptotically Tight Bound)를 의미합니다. (쉽게 생각하면 평균)
f(n)이 n0보다 크거나 같은 모든 n에서 0 이상이고 c1g(n) 이상 c2g(n) 이하이면, Θ(g(n)) = f(n) 입니다.
ex) 1/2n²-3n = Θ(n²), n0≥7, c1=1/14, c2=1/2에서
0≤1/14n²≤1/2n²-3n≤1/2n² 이다.

<img src="https://github.com/dhcho/Algorithm/blob/main/images/%231.jpg"/>      

​                                                  <3가지 표기법의 함수 모양>

Θ 표기법을 계산하여 사용하는 것이 가장 이상적이지만, 계산이 복잡하기 때문에 보통은 Big-O 표기법을 사용하여 시간 복잡도를 나타냅니다.
Big-O 표기법은 최대 차항만 계수 없이 표기하면 되기 때문에 사용하기 간편하고, 알고리즘의 최악의 경우를 의미해서 평균과 가까운 결과를 예측 할 수 있기 때문입니다.


## 시간 복잡도 계산

이제 위의 내용들을 토대로 여러가지 코드의 시간 복잡도를 계산해봅시다.
먼저, 아까부터 예시로 사용했던 코드들에 적용해봅니다.

```
int sum = 0;
for(int i=1; i<=N; i++)
    sum += i;
```


```
int sum = (N+1)*N/2;
```

먼저, 첫번째 코드는 sum=0이 한 번, int i=1이 한 번, i++이 N번, sum+=i가 N번 합쳐서 총 2N+2 번의 연산이 수행되었습니다.
Big-O 표기법으로 표현하면 2N+2 = O(N) 이므로, 첫번째 코드의 시간 복잡도는 O(N) 입니다.
다음으로, 두번째 코드는 (N+1)이 한 번, *N이 한 번, /2가 한 번, 대입 연산이 한 번 합쳐서 총 4번의 연산이 수행되었습니다.
Big-O 표기법으로 표현하면 4 = O(1) 이므로, 두번째 코드의 시간 복잡도는 O(1) 입니다.
O(N) > O(1) 이므로, 두번째 코드가 첫번째 코드보다 시간적인 측면에서 효율적입니다.
아래는 두번째 예시입니다.

```
int sum = 0;
for(int i=0; i<N; i++)
    for(int j=0; j<i; j++)
        sum += j;
```


```
int sum = 0;
for(int i=N; i>0; i/=2)
    for(int j=0; j<i; j++)
        sum += j;
```

반복문 안에 반복문이 들어가있습니다.
연산의 개수를 직접 세기는 힘드니까 이제부터는 대략적인 식을 사용하여 시간 복잡도를 계산합니다.
먼저, 첫번째 코드는 바깥쪽 반복문과 안쪽 반복문 총 두 개의 반복문으로 이루어져 있습니다. 바깥쪽 반복문은 N번 반복하고, 안쪽 반복문은 i의 값에 따라 반복 횟수가 다릅니다.
i는 0부터 N-1까지 변하며, 안쪽 반복문은 해당하는 i만큼 반복하므로, 0+1+2+…+(N-1) = N*(N-1)/2 번 반복합니다.
Big-O 표기법은 최대 차항만 계수 없이 표기하면 되기 때문에 결과적으로
N*(N-1)/2 = O(N²) 입니다.

다음으로, 두번째 코드는 바깥쪽 반복문이 lg N번 반복하고, 안쪽 반복문은 i의 값에 따라 반복 횟수가 다릅니다.
i는 N부터 1까지 변하며, 안쪽 반복문은 해당하는 i만큼 반복하므로, N + N/2 + N/4 + … + 1 = 2N 번 반복하고, Big-O로 표기하면 2N = O(N) 입니다.
