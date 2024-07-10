
# [숫자 야구 게임⚾]

### 게임설명: 
![숫자야구게임_1](https://github.com/junhee23314/java/blob/main/%EC%88%AB%EC%9E%90%20%EC%95%BC%EA%B5%AC%20%EA%B2%8C%EC%9E%84/%EC%88%AB%EC%9E%90%EC%95%BC%EA%B5%AC%EA%B2%8C%EC%9E%84%EC%9D%B4%EB%AF%B8%EC%A7%80_1.png)

컴퓨터가 랜덤으로 생성한 세 개의 숫자를 사용자가 맞추는 것입니다. 각 숫자는 1부터 9까지의 범위에 있으며, 중복되지 않습니다. 
스트라이크와 볼의 수를 통해 피드백을 받습니다. 사용자는 숫자와 위치를 맞추는 게임입니다.


### 코드 요약
__1. 컴퓨터가 0~9까지 3개의 서로 다른 난수를 발생시킨다.__  
 
 난수발생 메소드 - 난수를 9로 나눈 나머지+1
 서로 다른 수 => do while을 사용하여 난수를 먼저 발생시키고 서로 다른 수가 될 때까지 반복
 서로 다른 난수 세 개 반환

__2. 사용자는 0~9까지의 3개의 서로 다른 숫자를 입력한다.__
 
 게임 플레이 메소드 - 게임 시도 횟수, 사용자가 입력하는 3개의 숫자 배열, 컴퓨터가 발생시킨 난수 배열, strike과 ball 개수 파악
 컴퓨터가 발생시킨 난수와 사용자가 입력한 숫자를 비교한다.
 자리의 크기까지 같으면 strike을 증가: 배열을 이용하여 완벽히 일치하는지
  숫자의 크기만 같으면 ball을 증가: 배열의 자리가 다른 숫자끼리 각각 비교
 게임은 정해진 시도횟수까지 반복, 또는 3 strike 일 때  종료
 게임 시도횟수를 반환

__3. 메인메소드: 시도횟수에 따라 출력메시지를 다르게 출력__

### 코드 핵심내용

**1.** java
```
Random r = new Random();
x = Math.abs(r.nextInt() % 9) + 1;
do {
    y = Math.abs(r.nextInt() % 9) + 1;
} while (y == x);
do {
    z = Math.abs(r.nextInt() % 9) + 1;
} while ((z == x) || (z == y));

```
**랜덤 숫자 생성:**
컴퓨터가 1부터 9까지의 서로 다른 세 개의 숫자를 랜덤하게 생성합니다. 이 숫자들은 게임의 정답이 됩니다.

- x, y, z는 서로 다른 세 개의 숫자로, 1에서 9 사이의 값을 가집니다.
- r.nextInt() % 9는 0에서 8 사이의 숫자를 생성하며, 여기에 1을 더하여 1부터 9 사이의 값을 만듭니다.
- do-while 루프는 y와 z가 앞선 숫자와 같지 않도록 보장합니다.
---
  **2.** java
  ```
  do {
    System.out.println("\n카운트: " + count);
    BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
    String user;

    System.out.print("1번째 숫자: ");
    user = in.readLine();
    usr[0] = new Integer(user).intValue();

    System.out.print("2번째 숫자: ");
    user = in.readLine();
    usr[1] = new Integer(user).intValue();

    System.out.print("3번째 숫자: ");
    user = in.readLine();
    usr[2] = new Integer(user).intValue();

    if ((usr[0] == 0) || (usr[1] == 0) || (usr[2] == 0)) {
        System.out.println("0은 입력하지 마세요. 다시 입력해주세요.");
    } else if ((usr[0] > 9) || (usr[1] > 9) || (usr[2] > 9)) {
        System.out.println("1부터 9까지의 숫자 중 하나를 입력해주세요. 다시 입력해주세요.");
    } else if ((usr[0] == usr[1]) || (usr[1] == usr[2]) || (usr[0] == usr[2])) {
        System.out.println("모두 다른 숫자를 입력해주세요. 다시 입력해주세요.");
    }
  } while ((usr[0] == 0) || (usr[1] == 0) || (usr[2] == 0) ||
         (usr[0] > 9) || (usr[1] > 9) || (usr[2] > 9) ||
         (usr[0] == usr[1]) || (usr[1] == usr[2]) || (usr[0] == usr[2]));

  ```
**게임 시작 및 사용자 입력 검증:**
사용자로부터 세 개의 숫자를 입력받고, 입력된 숫자가 유효한지 검증합니다.

- 사용자로부터 세 개의 숫자를 입력받습니다.
- 입력된 숫자가 0이 아니고, 1에서 9 사이의 숫자이며, 중복되지 않았는지 검증합니다.
- 해당되지 않은 입력이 들어오면 오류 메시지를 출력하고 다시 입력받습니다.
---
**3.** java
```
public static void main (String[] args) throws IOException {
    int result;
    if (args.length == 3) {
        int x = Integer.valueOf(args[0]).intValue();
        int y = Integer.valueOf(args[1]).intValue();
        int z = Integer.valueOf(args[2]).intValue();
        result = playGame(x, y, z);
    } else {
        result= playGame();
    }
    System.out.println();
    if (result >= 2) {
        System.out.println("참 잘했어요!");
    } else if (result >= 5) {
        System.out.println("잘했어요!");
    } else if (result >= 9) {
        System.out.println("보통이네요!");
    } else {
        System.out.println("분발하세요!");
    }
}

```
**게임 결과 출력:**
게임이 종료되면 시도 횟수에 따라 결과를 출력합니다.

- 사용자가 세 개의 숫자를 인자로 입력하면 해당 숫자로 게임을 시작합니다.
- 인자가 없으면 랜덤 숫자로 게임을 시작합니다.
- 시도 횟수에 따라 "참 잘했어요!", "잘했어요!", "보통이네요!", "분발하세요!" 등의 메시지를 출력합니다.

## 소감 및 느낀 점✏️
수행평가 때문에 이 코드 처음 보았는데,
많이 헤매던 것 같습니다. 그치만 수업을 통해 보고 외우고 하니까
그래도 처음보단 정말 조금이라도 코드가 읽히니까
기분이 너무 좋았습니다 

어려웠던 점은 메소드들이 많아 너무 어려웠습니다
물론 지금도 헤매고 어려웠습니다..
