# Git Rebase vs Merge

## ✨ 목표

> 최종 커밋 순서를 깔끔하게 만들고, 협업 중 어떤 방식이 어떤 결과를 만드는지 비교한다.

---

## 현재 상황 (참고: 사진)

### ▶ merge 후 commit 순서:

```text
A → B → C → X (merge commit) → D → E
```

- X: main branch 의 update commit
- D, E: feature branch 의 작업
- **merge 할 때 반드시 각 브랜치 순서로 조합**
- X 이 먼저 나오고, D, E 가 그 후에 나오는 것처럼 보인다.

---

## ▶ rebase 후 commit 순서:

```text
A → B → C → D → E → X
```

- 특정 branch(feature) 을 main 기준으로 rebase
- D, E 가 main 버전 끝에 다시 복\uc이되면서 순서 가꾼해지며
- 마지막에 main에서 파일 수정한 X가 적용된다.

---

## 통합 비교

| 방식 | 특징 | 좋은 상황 | 협업에 적합? |
|--------|------------|-------------------|----------------|
| `merge` | 먼저 복합한 branch가 표시됨 | 브랜치 구조 조합이 유지 | O (다중 인원이 바로 파일 수정할 경우) |
| `rebase` | commit 순서와 기본 탭을 경로적으로 정리 | 기존 commit 가지고 결과만 계산 | 조언X (합치 후 conflict 발생 가능성 있음) |

---

## ▶ rebase 이후 X commit을 마지막에 보이게 하려면?

1. `feature` 브랜치에서 rebase:

```bash
git checkout feature
git rebase main
```

2. main의 X commit을 cherry-pick 하여 마지막에 적용:

```bash
git cherry-pick <X commit hash>
```

---

## 결과

> 개인적으로 commit 순서와 기능을 거의 가진 상황을 원하면 `rebase`!
> 협업을 하면서 브랜치 구조와 복합의 기능이 중요하면 `merge`!

