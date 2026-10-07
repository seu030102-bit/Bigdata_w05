# Observations · Week 5

## Task 1

In the broken version a dead end's rank leaves the graph and is gone. I send it back as a uniform teleport (treat the empty column as `1/n` everywhere) — the other defensible choice is to leak and renormalise after each step. The same teleport repairs both failures because it injects a positive probability of leaving *any* set, so mass cannot drain to zero and cannot stay trapped. `beta` is the chance the surfer follows a link; with probability `1 - beta` they jump to a page chosen uniformly.

고장 버전에서 dead end의 랭크는 그래프 밖으로 빠져 사라진다. 나는 그 질량을 모든 노드에 `1/n`으로 되돌렸다(빈 열을 균등 텔레포트로 본다). 매 스텝 후 재정규화도 가능한 선택이다. 같은 텔레포트가 두 고장을 고치는 이유는 어떤 집합에서든 나갈 확률이 생기기 때문이다. `beta`는 링크를 따라갈 확률이고, `1-beta`는 균등 점프다.

## Task 2

As beta → 1, iterations rose 14 → 24: the second eigenvalue is `beta`, so mixing slows when teleport shrinks. A4: **iteration count barely moved** with n (20 vs 21); **wall time did** (0.023 s → 0.66 s). Iterations are spectral; time is edges per iteration. A6: the top 10 first changed at **beta 0.7** (`p00000`/`p00004` swap). A published ranking is not independent of the 0.85 convention.

beta가 1에 가까워지면 반복이 14→24로 늘었다. 둘째 고유값이 beta라 텔레포트가 줄면 섞임이 느려진다. A4: **반복 수는 n과 거의 무관**(20 vs 21)이고 **시간만** 커졌다(0.023초 → 0.66초). A6: top 10은 **beta 0.7에서 처음** 바뀌었다. 공개 순위는 0.85 관례에 의존한다.

## Task 3

I store two rank vectors, **2n floats**, and walk the adjacency list already in `graph` — not M (n²). Teleport is `(1-beta)/n` added to every entry of the new vector; that is n additions, not an n×n multiply. Dead-end leak is the same shape: one scalar `beta * leaked / n` added everywhere. Worst per-node diff **1.18e-15**, not zero, from summation order — not a different algorithm. Harness: 76× faster, 600× less memory → strong.

저장하는 것은 랭크 벡터 두 개(**2n floats**)와 이미 있는 인접 리스트다. M(n²)은 만들지 않는다. 텔레포트는 새 벡터의 각 칸에 `(1-beta)/n`을 더하는 것뿐이라 n번 덧셈이지 밀집 곱이 아니다. dead-end 재분배도 스칼라 하나다. 노드당 최대 오차 **1.18e-15**는 합산 순서 때문이고, 벤치는 76배 빠르고 메모리 600배 절약 → strong.
