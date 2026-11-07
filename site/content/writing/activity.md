---
title: "대표 활동"
date: 2026-10-01
summary: "JAVA로 구현한 딱정벌레 이동"
tags: ["JAVA", "학습"]
---

## JAVA로 구현한 딱정벌레 이동

저는 특기할만한 대표적인 활동이 아직 없습니다. 따라서 객체지향프로그래밍(JAVA) 수업에서 10월 1일 개인 수행으로 구현 완료한, 한번 방문한 곳으로 다시 방문하지 않는 딱정벌레의 이동을 활동으로 적고자 합니다.

딱정벌레는 총 10회 이동하며 11x11 크기의 맵 내에서 이동합니다. 이는 콘솔창에서 볼 수 있는 문자열로 구현되었습니다.

Enter를 누를 때마다 딱정벌레의 이동 경로가 # 기호로 나타나는 JAVA 코드입니다. 이 코드는 강의자료에서 제시된 원본으로 이 코드를 수정하여 딱정벌레가 한번 방문한 곳은 다시 방문하지 않도록 해야합니다.

```JAVA
import java.util.Scanner;

public class RandomWalk {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        int x = 5, y = 5;
        boolean[][] tile = new boolean[11][11];
        int steps;
        tile[y][x] = true;

        for (steps = 0; steps < 10; steps++) {
            int direction = (int) (Math.random() * 4);

            if (direction == 0 && x > 0) // go left
                x--;
            else if (direction == 1 && x < 10) // go right
                x++;
            else if (direction == 2 && y > 0) // go up
                y--;
            else if (direction == 3 && y < 10) // go down
                y++;

            tile[y][x] = true;

            System.out.print("Enter.");
            input.nextLine();

            System.out.println("------------ " + (steps + 1) + " --------------");
            for (int i = 0; i < 11; i++) {
                for (int j = 0; j < 11; j++) {
                    if (tile[i][j] == true)
                        System.out.print("# ");
                    else
                        System.out.print(". ");
                }
                System.out.println();
            }
            System.out.println("-----------------------------");
        }
    }
}
```

## 1단계. 이미 방문한 칸으로 이동하지 못하도록 합니다.

for문 내부의 if-else문에서 조건을 하나 더 추가합니다. tile은 2차원 배열이고 각 요소의 값은 boolean입니다. for 반복문의 마지막에서 이동한 곳의 값을 true로 바꾸기 때문에 각 방향으로 이동할 때 해당 요소의 값이 false라는 것은 이동하지 않은 곳이라는 뜻이므로 조건식을 추가하여 이동하지 않은 곳으로만 이동하게끔 합니다.

```JAVA
    if (direction == 0 && x > 0 && tile[y][x-1] == false)
        x--;
    else if (direction == 1 && x < 10 && tile[y][x+1] == false)
        x++;
    else if (direction == 2 && y > 0 && tile[y-1][x] == false)
        y--;
    else if (direction == 3 && y < 10 && tile[y+1][x] == false)
        y++;
```

## 2단계. 총 10회 이동 규칙을 지킵니다.

총 10회 이동해야 하고 실패한 경우에는 이동하지 않은 것이므로 steps 변수의 값을 증가시키지 않아야 합니다. 따라서 if-else 반복문 아래에 else 구문을 추가하여 steps를 감소시키고 continue로 코드를 계속 진행시킵니다.

```JAVA
    if (direction == 0 && x > 0 && !tile[y][x-1])
        x--;
    else if (direction == 1 && x < 10 && !tile[y][x+1])
        x++;
    else if (direction == 2 && y > 0 && !tile[y-1][x])
        y--;
    else if (direction == 3 && y < 10 && !tile[y+1][x])
        y++;
    else {
        steps--;
        continue;
    }
```

## 최종 완성 코드와 구현된 실제 스크린샷

'구현'의 방식을 이용하였으며 딱정벌레가 한번 이동한 곳에 다시 이동하지 않으려면 그러한 기능을 구현하는 일 외에는 방법이 없기 때문에 선택했습니다.

```JAVA
import java.util.Scanner;

public class RandomWalk {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        int x = 5, y = 5;
        boolean[][] tile = new boolean[11][11];
        int steps;
        tile[y][x] = true;

        for (steps = 0; steps < 10; steps++) {
            int direction = (int) (Math.random() * 4);

            if (direction == 0 && x > 0 && !tile[y][x-1])
                x--;
            else if (direction == 1 && x < 10 && !tile[y][x+1])
                x++;
            else if (direction == 2 && y > 0 && !tile[y-1][x])
                y--;
            else if (direction == 3 && y < 10 && !tile[y+1][x])
                y++;
            else {
                steps--;
                continue;
            }

            tile[y][x] = true;

            System.out.print("Enter.");
            input.nextLine();

            System.out.println("------------ " + (steps + 1) + " --------------");
            for (int i = 0; i < 11; i++) {
                for (int j = 0; j < 11; j++) {
                    if (tile[i][j] == true)
                        System.out.print("# ");
                    else
                        System.out.print(". ");
                }
                System.out.println();
            }
            System.out.println("-----------------------------");
        }
    }
}
```

![ChatGPT 사용 사례](/portfolio.assignment/images/randomwalk.png)

## 학습 결과와 개선 방향

2차원 배열에 접근하는 방법을 알게 되었고 조금 더 창의적인 알고리즘은 없을까하는 생각이 들었습니다. 기존에 알고 있던 배열은 단순한 1차원 배열이었는데 2차원은 조금 난해하게 느껴졌습니다. 딱정벌레 이동 예제를 직접 고쳐보면서 2차원 배열에 대해 자세히 이해하였고 최종적으로 완성한 코드는 직접 실행해보니 발견한 문제점은 딱정벌레가 사방이 막혀있다면 이동하지 않는데도 반복문이 종료되지 않는다는 것입니다. 이를 해결하면 객체지향프로그래밍 수업에서 배운 예제를 완벽히 이해하는 좋은 결과를 얻을 수 있다고 생각합니다.