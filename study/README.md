# 프로그래머스 풀이 정리 LV1

1.로또의 최고 순위와 최저 순위
```
//다른사람풀이
import Foundation

func solution(_ lottos:[Int], _ win_nums:[Int]) -> [Int] {

    let zeroCount = lottos.filter { $0 == 0}.count
    let winCount: Int = win_nums.filter { lottos.contains($0) }.count


    return [min(7-winCount-zeroCount,6), min(7-winCount,6)]
}

```
>filter 를 생각하지 못했다. filter 를 쓰지 않아서 for문을 엄청 돌렸는데 반성타임...
>
>다음에는 filter를 써서 간결하고 깔끔한 코드 짜기로 마음 먹어야겠다 아자자!
>
>[고차함수 공부를 위해 참고한 링크](https://shark-sea.kr/entry/Swift-%EA%B3%A0%EC%B0%A8%ED%95%A8%EC%88%98-Map-Filter-Reduce-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0)

2.신규 아이디 추천
```

```
3.숫자 문자열과 영단어
```

```
4.키패드... 너무 어려워서 거의 코드를 해석하는 수준으로 해버렸다 반성~
```

```


