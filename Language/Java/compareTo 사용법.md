#### Arrays.sort, Collection.sort 라는 메서드를 많이 써봤음
#### 다만 그냥 실수 범주 안에있는 것만 정렬해봤음
#### 근데 알고리즘 문제 풀다 보니까 클래스 끼리 비교하면 어떨까라는 생각을 해봄
#### 찾아보니까 다음과같이 쓰면 되더라

``` java
private static class Score implements Comparable<Score>{  

	public String name;  
	public int korean, english, math;  
	
	public Score(String name, int korean, int english, int math) {  
	this.name = name;  
	this.korean = korean;  
	this.english = english;  
	this.math = math;  
	}  
	  
	//내가 target 보다 앞인 경우 음수  
	//내가 target 보다 뒤인 경우 양수  
	//(정렬 후를 기준으로) 나를 기준으로 해서 내 인덱스에서 저놈의 인덱스를 뺀 값이다  
	//그래도 생각하기 어렵다면 내 위치가 저놈보다 앞이면 음수 뒤면 양수로 외워라 

	@Override  
	public int compareTo(Score target) {  
		// 국어 점수 내림차순 (크면 앞이다)  
		// 내 국어 점수가 target의 국어 점수보다 낮은 경우 (내가 뒤에 온다)  
		if(this.korean < target.korean){  
			return 1;  
		}  
		// 내 국어 점수가 target의 국어 점수보다 큰 경우 (내가 앞에 온다)  
		else if (this.korean > target.korean) {  
			return -1;  
		}  
	  
		// 영어 점수 오름차순 (작으면 앞이다)  
		// 내 영어 점수가 target의 영어 점수보다 낮은경우 (내가 앞에 온다)  
		if(this.english < target.english){  
			return -1;  
		}  
		// 내 영어 점수가 target의 영어 점수보다 큰 경우 (내가 뒤에 온다)  
		else if (this.english > target.english) {  
			return 1;  
		}  
	  
		// 수학 점수 내림차순 (크면 앞이다)  
		// 내 수학 점수가 target의 수학 점수보다 작은 경우 (내가 뒤에 온다)  
		if(this.math < target.math){  
			return 1;  
		}  
		//내 수학 점수가 target의 수학 점수보다 큰 경우 (내가 앞에 온다)  
		else if (this.math > target.math) {  
			return -1;  
		}  
	  
		// 이름 사전순 오름차순  
		// 내 이름이 사전순으로 target의 이름보다 작을 경우 (내가 앞에 온다)  
		if(this.name.compareTo(target.name) < 0) {  
			return -1;  
		}  
		// 내 이름이 사전순으로 target의 이름보다 클 경우 (내가 뒤에 온다)  
		else if (this.name.compareTo(target.name) > 0) {  
			return 1;  
		}  
		//같은 경우  
		else return 0;  
	}  
}
```

#### 사용법
- 내가 target 보다 앞인 경우 음수
- 내가 target 보다 뒤인 경우 양수
- 같으면 0을 리턴하는 메서드이다
- 따라서 숫자값이면 오름차순 정렬의 경우 (문자하나(char) 일때도 동일 (아스키 코드))
	- 내가 대상보다 큰 경우 뒤에 와야 하므로 this.number - target.number 식으로 리턴을 하며
	- 내가 대상보다 작은경우 앞에 와야 하므로 target.number - this.number 식으로 리턴을 한다.
- 문자열인경우
	- 대소문자 구별이냐 아니냐에 다라서 String의 compareTo를 선택하며
	- String의 compareTo는 아스키코드 값에 따라서 사전식으로 분류가 되므로
	- 오름차순이면 그대로 리턴을 하며
	- 내림차순이면 부호 전환하여 리턴한다.