# C++ 단기간 코테 통과 프로젝트

## 공부할 것

* stl

  * vector
  * map
  * set
  * lower_bound
  * upper_bound
  * next_permutation
  * sort
  * cciterator

* 입출력 관련

  BOJ

  * 11718
  * 11719
  * 11720
  * 11721

## stl

### vector

* 자동으로 메모리가 할당되는 배열

#### 기본 method

```c++
// vector 헤더 추가
#include <vector>

// vector 선언
std::vector<type T> vec;

// std::를 반복해서 쓰면 가독성이 떨어지므로 using namespace std;를 추가
// type T는 템플릿이기 때문에 int, char, float 등을 넣어서 씀

// 종합
# include <vector>
using namespace std;
vector<int> vec;

vector<int> v(5);
// 기본값(0)으로 초기화 된 5개의 원소를 가지는 vector v를 생성

vector<int> v(5, 2);
// 2로 초기화 된 5개의 원소를 가지는 vector v를 생성

vector<int> v2(v1);
// v1 vecotr를 복사해서 v2 생성

v.assign(5, 2);
// 2로 5개의 원소 할당

v.at(idx);
// idx번째 원소를 참조
// v[idx] 보다 속도는 느리지만, 범위를 점검함

v[idx];
// idx 번째 원소 참조

v.front();
// 첫번째 원소 참조

v.back();
// 마지막 원소 참조

v.clear();
// 모든 원소 제거

v.begin();
// 첫번째 원소

v.end();
// 마지막의 '다음'을 가리킨다.

v.rbegin();
// 거꾸로 해서 첫번째 원소

v.rend();
// 거꾸로 해서 마지막의 다음

v.reserve(n);
// n개의 원소를 저장할 위치 예약

v.resize(n);
// 크기를 n으로 변경 더 커졌을 경우 0으로 초기화

v.resize(n, 3);
// 크기를 n으로 변경 더 커졌을 경우 3으로 초기화

v.size();
// 원소의 개수 return

v.capacity();
// 할당된 공간의 크기 return

v2.swap(v1);
// v1과 v2의 원소와 capacity swqp

v.insert(2, 3, 4);
// 2번째 위치에 3개의 4값을 삽입(뒤 원소는 뒤로 밀림)

v.insert(2, 3);
// 2번째 위치에 3을 삽입
// 삽입한 곳의 iterator를 반환

v.erase(iter);
// iter가 가리키는 원소를 제거
// size만 줄어들고 capacity는 그대로 남음

v.empty();
// vector가 비었으면 return true
```

* vector == array
* vector의 타입은 사용자가 정할 수 있다

#### 데이터 조작

```c++
vector<int> iVec;
int tmp = 10;
iVec.push_back(tmp);
// push_back()이라는 함수를 통해 값을 삽입한다.

int SIZE = 5;
vector<int> iVec(SIZE);
for(int i=0; i < SIZE; i++){
    iVec[i] = i * 10;
}
// push_back()을 쓰지 않고도 배열 상태로 값을 삽입 가능

 iVec.pop_back();
// 맨 마지막에 들어갔던 값을 pop

iVec.insert(2, 20);
// 삽입하려는 위치, 삽입할 값

iVec.erace(iVec.begin() + 5);
// iVec.begin()이 0인 경우 index가 5인 value를 지운다.

iVec.erase(iVec.begin(), iVec.begin() + 3);
// 0 ~ 3번째 value를 지운다.

// begin()은 vector에 저장되어 있는 값 중 가장 첫번째 인덱스를 return

iVec.swap(vec_temp);
// iVec vector와 vec_temp vector를 swqp
```

#### size와 capacity의 관계

* v.size()

  원소의 갯수를 return

* v.capacity()

  할당된 공간의 크기를 return

원소가 들어올 때마다 공간을 할당하면 비효율적이므로 원소의 개수가 공간을 초과할 때마다 $2^n$만큼 공간 할당

#### 멤버 형식

* iterator - 반복자 형식
* reverse_iterator - 역 반복자 형식
* value_type - 원소의 형식
* size_type - 원소의 개수의 형식

### 

### map

* key value 페어로 저장함

```c++
#include <map>
#include <string>
using namespace std;
map<string, int> m;

m.insert(make_pair(key, value));
m.insert(pair<string, int>('hi', 10));
m[key] = value; // 로도 가능한 듯?
// 맵에 원소를 pair 형태로 추가

m.erase(key);
// 맵에서 key에 해당하는 원소 삭제

m.clear();
// 맵의 원소들 모두 삭제

m.find(key);
// key에 해당하는 iterator를 반환

m.count(key);
// key에 해당하는 원소들의 개수 반환

m.empty();
// 맵이 비어있으면 true 아니면 false

m.size();
// 맵 원소들의 수 반환
```



### set

* 연관 컨테이너(associative container)
* key라 불리는 원소들의 집합으로 이루어진 컨테이너 (원소 = key)

```c++
#include <set>
using namespace std;
set<int> s;
set<pair<int, string>> s2;

set<int>::iterator iter; // 이걸로 iterator 표현 가능 위에도 마찬가지인 듯

s.begin();
// 첫 번째 원소를 가리키는 반복자 return

s.end();
// 맨 마지막 원소(의 다음)를 가리킴 원소의 끝부분을 알 때 사용함

s.rbegin();
s.rend();
// begin과 end의 반대로 작동
// 역으로 출력할 때 사용하면 좋음

for(iter = s.rbegin(); iter != s.rend(); iter++){
    cout << * iter << endl;
}

s.clear();
// 모든 원소 제거

s.count(k);
// 원소 k의 갯수를 return
// set에서는 0, 1임

s.empty();

s.insert(k);
// 원소 k 삽입
// 정렬된 위치에 삽입 됨
// return 값 : pair<iterator, bool>
// pair.first는 삽입한 원소를 가리키는 iterator pair.second는 성공 실패 나타냄

s.erase(iter);
// iter가 가리키는 원소 제거 다음 원소 iterator return

s.erase(start, end);
// start ~ end 원소 제거

s.find(k);
// 원소 k를 가리키는 반복자 return
// 없으면 s.end() return

s2.swap(s1);
// s1과 s2를 swap

s.upper_bound(k);
// 원소 k가 끝나는 구간의 iterator

s.lower_bound(k);
// 원소 k가 시작하는 구간의 iterator

s.equal_range(k);
// 원소 k가 시작하는 구간과 끝나는 구간의 반복자 pair 객체 반환

s.value_comp();
s.key_comp();
// 정렬 기준 조건자 반환

s.size();
// 사이즈(원소의 개수) 반환

s.max_size();
// 최대 사이즈(남은 메모리 크기)를 반환
```



### lower_bound

```

```

### upper_bound

### next_permutation

### sort

### iterator