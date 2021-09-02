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
answer = answer.filter("abcdefghijklmnopqrstuvwxyz-_.1234567890".contains)
```
>나는 이런식으로 풀었는데 swift 함수에 isLetter isNumber 가 있었다는걸 알았다.
>
>종종 쓸 곳이 많아보인다 다음 코딩테스트때 써보도록 해야지

3.숫자 문자열과 영단어
```
//다른사람코드
func solution(_ s:String) -> Int {


    var s = s
        var answer = s.replacingOccurrences(of: "zero", with: "0")
            .replacingOccurrences(of: "one", with: "1")
            .replacingOccurrences(of: "two", with: "2")
            .replacingOccurrences(of: "three", with: "3")
            .replacingOccurrences(of: "four", with: "4")
            .replacingOccurrences(of: "five", with: "5")
            .replacingOccurrences(of: "six", with: "6")
            .replacingOccurrences(of: "seven", with: "7")
            .replacingOccurrences(of: "eight", with: "8")
            .replacingOccurrences(of: "nine", with: "9")

    return Int(answer)!
}

```
>내 코드는 비효율적인데 이렇게 풀어도 되는구나 라는 생각이 들었다.
>
>replacingOccurrences를 이렇게 여러번 써도 되는구나라는 점을 깨달았다~
>
>다음번에는 진짜 꼭 써봐야지~


4.키패드... 너무 어려워서 거의 코드를 해석하는 수준으로 해버렸다 반성~
```
//다른사람 코드

func countKeypad(_ start: Int , _ dest: Int) -> Int {
    // [ 1, 2,  3]
    // [ 4, 5,  6]
    // [ 7, 8,  9]
    // [-1, 0, -2]
    let keypad = [[1, 2, 3], [4, 5, 6], [7, 8, 9], [-1, 0, -2]]
    var startPos = [0, 0]
    var destPos = [0, 0]

    for i in 0..<4 {
        for j in 0..<3 {
            if keypad[i][j] == start {
                startPos[0] = i
                startPos[1] = j
                //print("startPos\(startPos)")
            }
            if keypad[i][j] == dest {
                destPos[0] = i
                destPos[1] = j
                //print("destPos\(destPos)")
            }
        }
    }

    var count = 0
    for i in 0...1 {
        
        if(startPos[i] > destPos[i]){
             count += startPos[i] - destPos[i]
        }else{
           count += destPos[i] - startPos[i]
        }
    }

    return count
}

func solution(_ numbers:[Int], _ hand:String) -> String {
    var LH = -1
    var RH = -2
    var result = ""

    for n in numbers {
        switch n {
        case 1, 4, 7:
            LH = n
            result.append("L")
            break

        case 3, 6, 9:
            RH = n
            result.append("R")
            break

        default:
            let countLH = countKeypad(LH, n)
            let countRH = countKeypad(RH, n)
            print("countLH\(countLH)")
            print("countRH\(countRH)")
            // 같은거리면 왼손잡이 오른손잡이로 누름
            if countLH == countRH {
                if hand == "left" {
                    LH = n
                    result += "L"
                } else {
                    RH = n
                    result += "R"
                }
                break
            }

            // 가까운 손으로 누름
            if countLH < countRH {
                LH = n
                result += "L"
            } else {
                RH = n
                result += "R"
            }
            break
        }
    }

    return result
}
```
>이 부분에서 배운 부분이 굉장히 많았다.
>
>그리고 혼자 풀어보려 하다가 도저히 못풀겠어서 다른사람 풀이를 봤는데
>
>굉장히 자존심 하락...

|1|2|3| 
|:---|:---:|---:| 
|4|5|6| 
|7|8|9| 
|*|0|#| 

>세로의 차이가 3이라는것은 깨달아놓고 응용을 하지 못한것에 충격
>
>하지만 좌표화로 생각해서 풀면 금방 풀리는 것이였는데 좌표화 할 생각을 하지 못했다.
>
>[다른사람코드](https://codinglearn.tistory.com/28)를 보니 엄청 신박한 방법이 많았다.
>
>더 열심히 공부해야겠다...ㅠ

