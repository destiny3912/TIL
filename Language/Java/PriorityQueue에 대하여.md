### 우선 큐다 큐
### 그런데 큐에 집어넣으면 정렬을 해준다
### 선언 방식 - 기본 타입 (Wrapper Type)

``` java
// 낮은 숫자가 우선 순위인 (앞으로 오는)
PriorityQueue<Integer> pQueue = new PriorityQueue<>();
// 큰 숫자가 우선 순위인 (앞으로 오는)
PriorityQueue<Integer> pQueue = new PriorityQueue<>(Collections.reverseOrder());
```

### 선언 방식 - 사용자 정의 클래스

``` java
// 예시 클래스
private static class Lecture implements Comparable<Lecture> {  
	int S, T;  
  
	public Lecture(int s, int t) {  
		S = s;  
		T = t;  
	}  
	  
	//내가 쟤보다 앞이면 음수  
	//내가 쟤보다 뒤이면 양수  
	@Override  
	public int compareTo(Lecture target) {  
		return this.S - target.S;  
	}  
}

// 위 클래스를 우선순위 큐에 사용 할라면 그냥 다음과 같이 하자
// 정방향 정렬 (정렬 가장 앞이 가장 앞에 있는)
PriorityQueue<Lecture> pQueue = new PriorityQueue<>();
// 역방향 정렬 (정렬 가장 뒤가 가장 앞에 있는)
PriorityQueue<Lecture> pQueue = new PriorityQueue<>(Collections.reverseOrder());
```
#### 다만 여기서 주의할 점은 대상 클래스를 구현할 때 Comparable 인터페이스를 구현해야 한다 -> CompareTo 메서드 Override 해야함
#### 해당 메서드로 정렬을 함

### 우선순위 큐의 사용

- 그냥 별게 없다 일반적인 큐를 사용하는 것과 같다
- peak을 하면 가장 앞을 보는 것
- poll을 하면 가장 앞을 가져오고 제거함
- 등등 Collections 프레임워크를 따르는 자료구조에 불과함