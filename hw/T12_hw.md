# HW 6 — MLE로 모수 추정하기

**확률통계 · Topic 12** | 배점 25점 | 개인 과제

---

## 문제 1. Exponential의 MLE 유도와 검증 (10점)

$X_1, \ldots, X_n \sim \text{Exp}(\lambda)$ 일 때 $\lambda$ 의 MLE를 구한다.

- **(a)** log-likelihood $\ell(\lambda)$ 를 쓰고, 미분해서 $\hat\lambda_{\text{MLE}}$ 를 **유도**한다
  (과정을 마크다운에 적을 것)
- **(b)** $\lambda = 0.4$ 로 데이터 500개를 생성하고 (a)의 공식으로 추정한다
- **(c)** **격자 탐색**과 **`scipy.optimize`** 로도 구해 세 값이 일치하는지 확인한다
- **(d)** $n$ 을 10, 100, 1000, 10000 으로 바꿔가며 각각 200번 반복해
  $\hat\lambda$ 의 **평균과 표준편차**를 표로 정리한다. 일치성이 보이는가?

> 💡 $\hat\lambda_{\text{MLE}} = 1/\bar{X}$ 가 나온다. 그런데 이것은 **불편이 아니다.**
> (d)에서 $n$ 이 작을 때 평균이 0.4보다 큰지 확인해볼 것.

## 문제 2. 손으로 못 푸는 MLE (8점)

**Beta 분포**의 모수 $(\alpha, \beta)$ 는 해석적으로 풀리지 않는다.

- **(a)** `rng.beta(2, 5, size=300)` 으로 데이터를 만든다
- **(b)** `scipy.optimize.minimize` 로 **음의 log-likelihood를 최소화**해
  $(\hat\alpha, \hat\beta)$ 를 구한다 (`stats.beta.logpdf` 사용)
- **(c)** 추정된 모수로 그린 PDF를 데이터 히스토그램에 겹쳐 그린다
- **(d)** `stats.beta.fit(data, floc=0, fscale=1)` 의 결과와 비교한다 (SciPy도 MLE를 쓴다)

## 문제 3. 손실함수의 정체 (7점)

- **(a)** $y_i = f(x_i) + \varepsilon_i$, $\varepsilon_i \sim N(0, \sigma^2)$ 를 가정하면
  NLL을 최소화하는 것이 **제곱오차를 최소화하는 것과 같음**을 3~5줄로 보인다
- **(b)** 오차를 Gaussian 대신 **Laplace 분포**로 가정하면 어떤 손실함수가 나오는가?
  (Topic 7 Laplace PDF를 참고. 결과만 맞으면 된다)
- **(c)** (b)의 손실함수가 **이상치에 더 강한 이유**를 2문장으로 설명한다

---

## 제출

| 항목 | 내용 |
|---|---|
| 파일 | `HW_학번_T12.ipynb` |
| 제출처 | Google Classroom |
| 기한 | ⚠️ **PLATO · Google Classroom 공지 확인** |
| 필수 | 문제 1(a)·3(a)의 유도 과정, 1(d)의 표, 2(c)의 그래프 |

## 채점 루브릭

| 항목 | 배점 | 상 | 중 | 하 |
|---|:-:|---|---|---|
| 문제 1 | 10 | 유도 정확 + 세 방법 일치 + 일치성 확인 | 공식은 맞으나 검증 부족 | 유도 오류 |
| 문제 2 | 8 | 수치 최적화 성공 + SciPy와 일치 | 최적화는 되나 그래프 없음 | 수렴 실패 방치 |
| 문제 3 | 7 | (a) 유도 + (b)(c) 정확 | (a)만 | 개념 혼동 |

**감점** — 한글 폰트 깨짐 −1 / 출력 미포함 −2 / 시드 미지정 −1

---

## 자주 하는 실수

- **최대화와 최소화를 헷갈린다.** `scipy.optimize` 는 **최소화**만 하므로 **음의** log-likelihood를 넣는다
- $\log(0)$ 이 나와 `-inf` 가 되는 경우 → 모수 범위를 `bounds` 로 제한한다
- 문제 2에서 초기값이 나쁘면 수렴하지 않는다 → `x0=[1, 1]` 정도에서 시작
- `np.var(x)` 와 `np.var(x, ddof=1)` 을 구분할 것 (랩 Part 3)

<span class="ref">Chan §8.1–8.2</span>
