# 선택 HW — Topic 5 · 엔트로피로 게임 풀기 (가산점 5점)

**확률통계 · Topic 5** | **선택 과제**

> ⚠️ 이번 주는 **정식 과제가 없다.** 대신 **미니 프로젝트 1**의 팀 구성과 주제 선정을
> 이번 주 안에 마쳐야 한다. 아래는 관심 있는 학생을 위한 **가산점 과제**다.

---

## 문제. Wordle 첫 단어 고르기 (5점)

Wordle에서 **첫 번째 추측 단어**를 무엇으로 고르는 것이 유리할까?
"정보를 가장 많이 주는 단어"를 **엔트로피로** 판단해보자.

### 설정

- 5글자 단어 후보 목록은 아래 코드로 만든다 (간이 버전, 200개 내외)
- 추측 결과는 각 글자마다 🟩(정확한 위치) / 🟨(다른 위치에 있음) / ⬜(없음) 셋 중 하나
- 따라서 한 번의 추측 결과는 $3^5 = 243$ 가지 패턴 중 하나다

### 할 일

**(a)** 추측 단어 `guess` 와 정답 후보 `answer` 를 받아 **패턴을 반환**하는 함수를 만든다.
(간단히 하기 위해 중복 글자 처리는 신경 쓰지 않아도 된다)

**(b)** 어떤 추측 단어에 대해, 모든 정답 후보를 훑으며 **패턴별 후보 수**를 센다.
이 분포의 **엔트로피**를 계산한다.

$$H(\text{guess}) = -\sum_{\text{pattern}} p(\text{pattern}) \log_2 p(\text{pattern})$$

**(c)** 후보 단어 20개 이상에 대해 엔트로피를 구하고 **상위 5개**를 출력한다.

**(d)** 엔트로피가 높은 단어와 낮은 단어의 **공통점**을 각각 2문장으로 설명한다.

### 시작 코드

```python
import numpy as np
from collections import Counter

# 간이 단어 목록 (원하면 더 늘려도 좋다)
words = ["crane", "slate", "trace", "adieu", "audio", "raise", "roast",
         "stare", "least", "point", "movie", "beach", "chair", "dance",
         "fruit", "ghost", "house", "juice", "knife", "lemon", "mouse"]

def pattern(guess, answer):
    """🟩=2, 🟨=1, ⬜=0 을 5자리 튜플로 반환"""
    out = []
    for i, ch in enumerate(guess):
        if ch == answer[i]:
            out.append(2)
        elif ch in answer:
            out.append(1)
        else:
            out.append(0)
    return tuple(out)
```

> 💡 **핵심 아이디어** — 좋은 추측은 정답 후보를 **가장 고르게 쪼개는** 추측이다.
> 고르게 쪼갤수록 엔트로피가 크고, 남은 후보가 가장 많이 줄어든다.
> 슬라이드의 "스무고개" 슬라이드가 정확히 이 이야기였다.

---

## 제출

| 항목 | 내용 |
|---|---|
| 파일 | `HW_학번_T05_bonus.ipynb` |
| 기한 | PLATO · Google Classroom 공지 확인 |
| 제출처 | Google Classroom |
| 기한 | ⚠️ **PLATO · Google Classroom 공지 확인** |
| 필수 | (c)의 상위 5개 출력, (d)의 서술 |

## 채점

| 항목 | 배점 |
|---|:-:|
| (a)(b) 동작하는 엔트로피 계산 | 3 |
| (c) 순위 출력 | 1 |
| (d) 해석 | 1 |

---

## 참고

- 강의 슬라이드 Topic 5 — "스무고개로 이해하기"
- 3Blue1Brown, *Solving Wordle using information theory* (영상)
- 랩 노트북 `T05_lab.ipynb` Part 1의 `entropy()` 함수를 그대로 쓰면 된다
