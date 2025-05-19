# spike-pr-template
### 🌲 PR TEMPLATE
#### PR TEMPLATE 작성, 아래 조건 확인
1. main이 아닌 다른 branch에 존재하는 경우
  - workflow는 main이 아닌 다른 브랜치에 존재해도 생김
  - issue template은 main에 존재해야만 활성화 됨
2. 다중 PR template이 제대로 작동하는지
  - 다중 PR template이 가능하긴 하지만 PR을 눌렀을 때 뜨지 않고 link뒤에 메뉴얼하게 경로를 붙여야 한다는 글 뿐
    - link뒤에 PR-TEMPLATE 경로 작성
3. 2가 가능할 때 단일 PR-TEMPLATE과 다중 PR-TEMPLATE이 공존 할 때 어떻게 되는지
  - 순서 확인 (단일 생성 후 다중 생성한 경우, 다중 생성 후 단일 생성한 경우 모두 확인)
---
### ✅ 목적
- PR-TEMPLATE 설정 시 어떻게 작성하면 되는지 테스트
---
### 🔎 주요 내용 요약
#### ❌ main이 아닌 다른 branch에 존재하는 경우 활성화되지 않음
#### ❌ Multiple 템플릿을 사용하는 경우 UI에서 템플릿을 선택할 수 있은 창이 나오지 않음
- ⚠️ `[https://github.com/can019/spike-pr-template/compare/.../...muttiple-1](https://github.com/{owner}/{repo}/compare/{base_branch}...{compare_branch}?expand=1&template={TEMPLATE_FILE_NAME}
)` 과 같이 마지막에 쿼리 파라미터로 파일을 지정해줘야 template 변경 가능
#### ✅ Multiple template과 Single template이 모두 있을 때 사용 가능
#### ✅ Multiple과 Single template 생성 순서에 상관 없음
- Multiple 생성 -> Single 생성 test ✔️
- Single 생성 -> Multiple 생성 test ✔️
- 템플릿 생성 시 간혹 생성 순서에 따라 작동하지 않는 솔루션들이 있어 테스트해보았음
