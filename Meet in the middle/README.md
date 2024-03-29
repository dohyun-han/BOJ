# ※ Meet in the middle(중간에서 만나기)

Meet in the middle 알고리즘은 전체 크기를 반으로 나눠 계산의 양을 줄이는 방식의 알고리즘입니다.<br><br>
* 탐색의 크기를 반으로 나눕니다.
* 한 쪽에서 탐색을 진행합니다.
* 반대쪽에서 탐색을 진행합니다.
* 양쪽에서 나온 결과를 합하여 결과를 도출합니다.

![2021-11-02-14-19-32](https://user-images.githubusercontent.com/63232876/139878741-5d18e9a0-eb85-414d-af56-979b68a489b7.png)

* 예를 들어 크기가 10인 배열이 있고, 이 배열 전체를 탐색하는데 2<sup>10</sup>이 드는 문제가 있다고 가정합니다.<br>
만약 이 알고리즘을 사용한다면, 탐색의 범위가 각각 반으로 줄어들어 2<sup>5</sup> X 2의 시간이 소요되어 계산 양이 줄어들게 됩니다. 그림에서는 배열을 10으로 가정했지만 2<sup>40</sup>만 되어도 수는 급격하게 늘어나게 됩니다.<br> 나눠진 부분을 합하여 결과를 도출하는데 추가적인 계산이 들 수도 있지만, 대체로 탐색 연산보다는 적은 시간이 소요됩니다.<br> 
알고리즘 자체는 간단하지만 구현하는 과정이 조금 까다로울 수 있고 탐색 범위가 적당히 클 때 사용할 수 있습니다.
<br><br><br>

## 1208번: 부분 수열의 합 2
https://www.acmicpc.net/problem/1208
![2021-11-02-14-41-08](https://user-images.githubusercontent.com/63232876/139878783-15c400b4-347c-48bb-80f3-058426136754.png)

* 부분 수열의 합이 S가 되는 수열의 수를 구하는 문제입니다. <br>
모든 부분 수열의 합을 계산한다고 생각해 볼 수 있습니다. 하지만 모든 부분수열의 개수는 2<sup>N</sup>이고 최대 2<sup>40</sup>이 되어 하나씩 구할 경우 시간 초과가 납니다. 만약 탐색 범위를 반으로 줄인다면 2<sup>20</sup>이 되어 계산의 양을 줄일 수 있습니다. 해당 방법을 이용하여 문제를 풀 수 있습니다.<br>

    * DFS로 0 ~ N/2 - 1 인덱스까지의 각 부분 수열의 합(sum)을 계산하고 그 합을 인덱스로 하여 lsum[sum]의 개수를 증가시킨다. 이때 합이 음수가 될 수 있으므로 2000000을 더하여 양수로 만들어 준다. (left())
    * DFS로 N/2 ~ N-1 인덱스까지의 각 부분수열의 합(sum)을 구하고 lsum[S - sum + 2000000]을 결과값에 더한다. (right())
    * S가 0일 경우 부분 수열의 크기는 0인 경우가 포함되어 있으므로 결과값에서 1을 빼준다.

### 코드
https://github.com/dohyeon-han/BOJ/blob/main/Meet%20in%20the%20middle/1208.cpp
<br><br><br>

## 1450번: 냅색문제
https://www.acmicpc.net/problem/1450
![2021-11-02-14-42-35](https://user-images.githubusercontent.com/63232876/139878814-899f90a7-9e8c-45c4-8d57-d73bfd094f62.png)

* 위의 문제와 유사한 문제입니다. 모든 부분 수열의 합은 최대 2<sup>30</sup>으로 약 10억번의 계산이 필요합니다.<br> 만약 n을 반으로 줄인다면 2<sup>15</sup>가 되어 충분히 빠르게 계산할 만한 값이 됩니다. 다음과 같은 방법으로 탐색 범위를 반으로 줄일 수 있습니다.<br>

    * 배열을 반으로 나눠 왼쪽 배열에서 모든 부분수열의 합을 계산한다. (leftWei[])
    * 합을 오름차순으로 정렬한다.
    * 나머지 오른쪽 배열에서 모든 부분수열의 합을 계산한다. (rightWei[])
    * (최대무게 - rightWei[i])를 upper bound를 통해 leftWei에서 찾으면 그 인덱스의 값이 넣을 수 있는 무게의 수가 되고 구한 무게 수의 총 합이 가방에 넣을 수 있는 방법의 수가 된다.


### 코드
https://github.com/dohyeon-han/BOJ/blob/main/Meet%20in%20the%20middle/1450.cpp
<br><br><br>

## 22882번: 시험 문제 출제
https://www.acmicpc.net/problem/22882
![2021-11-02-14-45-32](https://user-images.githubusercontent.com/63232876/139878837-ac075d76-c1b4-412d-9eb1-6baafc1fed94.png)

* (1,1)에서 (N,N)까지의 경로를 수열로하여 최대 부분합이 K인 수열의 개수를 구하는 문제입니다.<br>
(1,1)에서 (20,20)까지의 경로 수는 오른쪽으로 이동하는 횟수 19번, 아래로 이동하는 횟수 19번 총 <sub>38</sub>C<sub>19</sub>로 매우 큰 수가 됩니다.<br>
2차원 배열의 칸을 (x,y)라 할때, (1,1), (N,N)에서 x + y = N + 1을 만족하는 대각선까지의 경로는 트리 형태이므로 그 개수는 약 2*2<sup>19</sup>이 되어 계산할 수 있는 수가 됩니다.

![2021-11-02-18-35-44](https://user-images.githubusercontent.com/63232876/139878867-4818cc9f-8863-4835-8352-2a1b2810383b.png)

* 경로를 지나면서 최대 부분합을 구해야 하는데, 이전 부분 합을 pre, 최대 부분 합을 mx라 할 때, max 계산을 통해 각 수열을 지나면서 최대 부분합을 구할 수 있습니다.

``` C++
pre = max(pre+arr[y][x], pre);
mx = max(mx,pre);
```

* 두 수열를 합친 최대 부분합은 max(mx<sub>1</sub>,mx<sub>2</sub>,pre<sub>1</sub>+pre<sub>2</sub>)이 됩니다.

* 두 수열이 만나는 지점에서 mx<sub>1</sub><=k인 pre<sub>1</sub>과 mx<sub>2</sub><=k인 pre<sub>2</sub>를 이용해
최대 부분합이 k이하인 수열의 개수를 구할 수 있는데 이를 f(k)라 한다면
f(k)-f(k-1)로 최대 부분합이 k인 수열을 구할 수 있습니다.<br>
f(n)에서 pre<sub>1</sub>, pre<sub>2</sub>의 값을 각각 배열로 만들어 정렬한다면 투 포인터를 이용해 구할 수 있습니다.<br>
* f(n)를 구하기 위해 다음과 같은 pre<sub>1</sub>, pre<sub>2</sub>배열이 있다고 한다면,

![2021-11-03-00-05-05](https://user-images.githubusercontent.com/63232876/139878919-b113cd5a-be73-4237-84c6-790b8eb0521a.png)

* 양 끝에 포인트를 둬서 인덱스 값의 합이 k보다 크면 e-=1<br>
k이하이면 e+1만큼의 최대 부분합이 k보다 작으므로 결과 값에 더해준 후 s+=1을 해줍니다.

![2021-11-03-00-05-43](https://user-images.githubusercontent.com/63232876/139878949-7312b095-d3e6-43c3-9a41-d4ee9e719af9.png)

* 10+(-2)<=15 이므로 결과값에 4를 더해준후 s+=1을 해줍니다.

![2021-11-03-00-06-27](https://user-images.githubusercontent.com/63232876/139878999-627d77e4-d33d-44e0-b795-ecec6a39581e.png)

* 10+0<=15 이므로 결과값에 4를 더해준후 s+=1을 해줍니다.
* 이런 방식으로 계산한 후 s또는 e가 각 배열을 벗어나게 되면 함수는 return됩니다.

* 이 계산을 만나는 지점인 (1,N), (2,N-1), ... , (N-1,2), (N,1)에서 각각 해주고 그 값을 모두 합하면 최대 부분합이 K인 수열을 만드는 서로 다른 방법의 수가 됩니다.<br>

### 코드
https://github.com/dohyeon-han/BOJ/blob/main/Meet%20in%20the%20middle/22882.cpp
