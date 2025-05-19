# [Spike] PR-Template
### 🌲 PR TEMPLATE
#### PR TEMPLATE 작성, 아래 조건 확인
1. main이 아닌 다른 branch에 존재하는 경우
  - workflow는 main이 아닌 다른 브랜치에 존재해도 생김
  - issue template은 main에 존재해야만 활성화 됨
2. 다중 PR template이 제대로 작동하는지
  - 다중 PR template이 가능하긴 하지만 PR을 눌렀을 때 뜨지 않고 link 뒤에 메뉴얼하게 경로를 붙여야 한다는 글 뿐
    - link뒤에 PR-TEMPLATE 경로 작성
3. 2가 가능할 때 단일 PR-TEMPLATE과 다중 PR-TEMPLATE이 공존 할 때 어떻게 되는지
  - 순서 확인 (단일 생성 후 다중 생성한 경우, 다중 생성 후 단일 생성한 경우 모두 확인)
---
### ✅ 목적
- PR-TEMPLATE 설정 시 어떻게 작성하면 되는지 테스트
---
### 🔎 주요 내용 요약
#### ❌ main이 아닌 다른 branch에 존재하는 경우 활성화되지 않음
#### ❌ Multiple 템플릿을 사용하는 경우 템플릿을 선택할 수 있는 UI 창이 나오지 않음
- ⚠️ `[https://github.com/can019/spike-pr-template/compare/.../...?expand=1&template=multiple1.md]`과 같이 마지막에 쿼리 파라미터로 파일을 지정해줘야 template 변경 가능
- **양식:** `https://github.com/{owner}/{repo}/compare/{base_branch}...{compare_branch}?expand=1&template={TEMPLATE_FILE_NAME}
` 
#### ✅ Multiple template과 Single template이 모두 있을 때 사용 가능
#### ✅ Multiple과 Single template 생성 순서에 상관 없음
- Multiple 생성 -> Single 생성 test ✔️
- Single 생성 -> Multiple 생성 test ✔️
- 템플릿 생성 시 간혹 생성 순서에 따라 작동하지 않는 솔루션들이 있어 테스트해보았음
  
---

## 🤔 생각해 볼 것
### ❗ 관리 방식 설명 및 장단점
| 전략                  | 구현 방식                                                              | 장점                                                                                                 | 단점                                                                                                     |
|-----------------------|------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| Single template만 유지 | 모든 템플릿 내용을 하나에 넣고, 필요한 부분만 사용하고 나머지는 지움       | - 구현 간편<br>- PR 템플릿 존재 인지 쉬움<br>- 링크 없이도 바로 사용 가능<br>- 도구(JIRA 등) 연동 안정적 | - 불필요한 부분 지우는 작업 번거로움<br>- PR 제목 강제 불가 (body에 안내 가능)<br>- 템플릿 일관성 떨어질 수 있음 |
| Multiple template만 유지 | 템플릿 파일을 여러 개로 분리하고, PR 생성 시 query param으로 선택 지정     | - 파일 분리로 관리 편리<br>- 목적별로 명확히 구분 가능<br>- 자동화 및 GitHub Action과 연계 용이         | - 기본값이 빈 템플릿(blank)<br>- query param 숙지 필요 (교육 비용 발생)<br>- 누락 시 다른 PR에서 복붙 필요       |
| Single + Multiple     | 자주 사용하는 템플릿은 Single에, 나머지는 Multiple로 분리 사용            | - 전략적 템플릿 분리 가능<br>- 핵심은 Single로 유지하고 세부 분기는 Multiple로<br>- 최소한의 가이드 + 유연성 확보 | - 관리 복잡도 증가<br>- 사용자가 어떤 템플릿을 써야 하는지 혼란<br>- 장점/단점이 명확하지 않아 운영 혼선 가능        |


### ❓ 추가적인 고려사항
| 고려 항목         | 내용                                                                                       | 해당 전략 영향도                        |
|------------------|--------------------------------------------------------------------------------------------|-----------------------------------------|
| 교육 비용         | query param 사용법에 대한 사전 지식 요구                                                  | Multiple, Single+Multiple: 높음         |
| 도구 통합 영향    | 템플릿 파일이 하나인 경우 외부 도구 연동이 더 단순함 (JIRA 자동 채움 등)                  | Single: 유리                            |
| 자동화 가능성     | 템플릿마다 분기 설정 가능 → GitHub Action 조건 처리 유리                                   | Multiple, Single+Multiple: 유리         |
| 리뷰어 사용자 경험 | Single은 불필요한 섹션이 남아있을 수 있어 집중 어려움                                      | Multiple: 좋음 / Single: 나쁨           |
| 실수 방지         | 템플릿 선택을 빼먹을 수 있음 → blank PR 생성 위험                                          | Multiple: 취약                          |
| 유지보수 난이도   | 템플릿 변경 시 영향 범위가 어디까지 퍼지는지 관리 어려움                                   | Single+Multiple: 높음 / Single: 낮음    |

