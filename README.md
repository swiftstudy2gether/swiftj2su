# 프로그래머스 풀이 정리 LV1

1 . 로또의 최고 순위와 최저 순위
```
import Foundation

func solution(_ lottos:[Int], _ win_nums:[Int]) -> [Int] {
    var winfirst : Int = 0
    var winlast : Int = 0
    var winarray : [Int] = []
    for i in 0..<lottos.count{
        if(lottos[i] == 0){
                print(0)
                winfirst += 1
            }
        for j in 0..<win_nums.count{
            if(lottos[i] == win_nums[j]){
                print("맞음")
                winfirst += 1
                winlast += 1
            }
        }
    }

    winarray.append(countwin(win : winfirst))
    winarray.append(countwin(win : winlast))

    return winarray
}

func countwin(win : Int) -> Int {
    var winner : Int = 0
    print("win\(win)")
    switch win { 
        case 1: // todo 
        winner = 6
        break;
        case 2: // todo 
        winner = 5
        break;
        case 3 : // todo 
        winner = 4
        break;
        case 4 : // todo 
         winner = 3
        break;
        case 5 : // todo 
        winner = 2
        break;
        case 6 : // todo 
        winner = 1
        break;
        default:
         winner = 6// todo 
        break; 
    }
    return winner;

}
```
2.신규 아이디 추천
```
import Foundation

func solution(_ new_id:String) -> String {
    
    var answer : String = ""
    var answer2 : String = ""
    
    //1단계
    answer = new_id.lowercased
    
    //2단계
    answer = answer.filter("abcdefghijklmnopqrstuvwxyz-_.1234567890".contains)
    
    //3단계
    while (answer.contains("..")){
        answer = answer.replacingOccurrences(of: "..", with: ".")
    }
    
    //4단계
    answer = answer.trimmingCharacters(in: ["."])
    
    //5단계
    
    if(answer.count == 0){
        answer.append("a")
    }
   
    //6단계
    var i : Int = 0
    for s in answer {
        i+=1
        if(i<16){
        answer2.append(s)
        }
    }
    answer2 = answer2.trimmingCharacters(in: ["."])
    
    //7단계
    while(answer2.count < 3){
        answer2.append(answer2[answer2.index(before: answer2.endIndex)])
    }
    
    
    return answer2
}
```
3.숫자 문자열과 영단어
```
import Foundation

func solution(_ s:String) -> Int {
    
    var str : String = ""
    var strnum : String = ""
    var numint : Int = 0
    
    for item in s{
        print(item)
        str += String(item)
        if(str == "one" || str == "1"){
            strnum += "1"
            str=""
        }
         if(str == "two" || str == "2"){
            strnum += "2"
            str=""
        }
         if(str == "three" || str == "3"){
            strnum += "3"
            str=""
        }
         if(str == "four" || str == "4"){
            strnum += "4"
            str=""
        }
         if(str == "five" || str == "5"){
            strnum += "5"
            str=""
        }
         if(str == "six" || str == "6"){
            strnum += "6"
            str=""
        }
         if(str == "seven" || str == "7"){
            strnum += "7"
            str=""
        }
         if(str == "eight" || str == "8"){
            strnum += "8"
            str=""
        }
         if(str == "nine" || str == "9"){
            strnum += "9"
            str=""
        }
         if(str == "zero" || str == "0"){
            strnum += "0"
            str=""
        }
    }
    
    print("strnum\(strnum)")
    numint = Int(strnum)!
    
    return numint
}
```
4. 키패드... 너무 어려워서 거의 코드를 해석하는 수준으로 해버렸다 반성~
```
import Foundation

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
>dfs
