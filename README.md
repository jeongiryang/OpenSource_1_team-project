## 오픈소스 1팀 프로젝트 보고서


###  _실행 시 주의사항:_

- **visual studio code 환경에서 main.py 실행시 인코딩 문제가 발생할 수 있습니다.**
 **인코딩 오류 발생 시 아래 명령어를 Git bash 터미널로 전환 후 콘솔에 입력해주세요!**

  - **main.py가 있는 폴더에서 Git Bash 터미널을 실행시켜야 합니다!**
    
    > " python -X utf8 main.py "


## 1. 프로젝트 정보

- **과제명:** Git 협업을 통한 파이썬 기반 텍스트 터미널 TRPG 게임 구현
- **제출팀:** 오픈소스소프트웨어 1조
- **팀원명:** 안선효, 박지환, 정이량, 송지한
- **제출일:** 2025년 6월 23일

[GitHub 저장소 바로가기](https://github.com/jeongiryang/OpenSource_1_team-project.git)




## 2. 프로젝트 개요

**TRPG 게임**
- 본 프로젝트는 각 팀원이 독립적인 파이썬 기반 게임 기능(플레이어, 전투, 몬스터, 상점 등)을 구현한 후, GitHub 협업을 통해 텍스트 기반 TRPG 시스템으로 통합하는 것을 목표.

- '게임'이라는 주제의 특성상 각 기능은 파이썬 모듈 간의 명확한 의존성을 가지므로, GitHub 을 활용한 체계적인 브랜치 관리와 Merge 과정을 활용해보고 실질적인 협업 능력을 학습하기에 최적이라 판단하여 선정.

- **목표:**
  1. Git 브랜치 전략 및 commit, Pull Request, conflict 기반의 협업 구조 실습
  2. 개별 기능 구현이 아닌 협업을 통한 통합 구조 구성 경험(파이썬의 모듈화 호출로 실행)
  3. 팀워크 기반의 실전 오픈소스 프로젝트 유사 경험

---

## 3. 폴더 구조 및 전체 흐름

```
OpenSource_TeamProject_1_team/ ← 루트 디렉토리
├── README.md                  ← 보고서 (본 문서)
├         
├── feature/director/          ← 팀원 1. 안선효(게임의 총괄 및 실행)
│   └── main.py
│   └──game_manager.py
├── feature/monster/           ← 팀원 2. 송지한(몬스터 데이터 기능 구현)
│   └── monster_data.py
|   └── coin.py
├── feature/player/            ← 팀원 3. 정이량(플레이어와 상점 기능 구현)
│   └── shop.py
|   └── player.py
├── feature/combat/            ← 팀원 4. 박지환(전투, 던전 기능 구현)
│   └── dungeon.py
|   └── combat.py
```

- **`main.py` 및 구조 통합 방식 체택**

  - **본 프로젝트의 코드 실행점은 `main.py`로, 전체 게임을 실행하는 메인 루프를 담당한다.**

---

**실행 시 플레이어는 다음 중 하나를 선택할 수 있다**

- 던전에 입장하여 몬스터와 전투
- 상점에서 아이템(장비,물약) 구매 또는 능력치 구매
- 상점에서 회복 기능
- 레벨업 시스템 
- 게임 종료

---

**선택 메뉴는 터미널 기반 인터페이스로 구성되어 있으며, 
각 기능은 다음과 같이 모듈별 함수 호출 방식으로 실행**


- `dungeon.enter_dungeon(player)` → 전투 진행

- `shop.enter_shop(player)` → 상점 기능 실행

- `combat.start_combat(player, monster)` → 전투 시스템
---

**각 기능은 독립적인 `.py` 파일로 분리되어 있으며 모든 핵심 로직은 `main.py`와 `game_manager.py`를 통해 통합됨.**

 이 구조는 모듈화를 기반으로 Git 협업을 효율화하기 위한 것으로,
모든 팀원이 각자의 `.py` 모듈을 별도 브랜치에서 개발 후 병합하여
`main.py`를 통해 단일 실행 체계로 연동되도록 설계되었다.

---

## 4. 주요 기능 및 역할 분담

| 팀원  | 폴더 | 주요 기능 개요 | 스크린샷 |
|:---:|:---:|:---:|:---:|
|안선효| `feature/director` | 전체 게임의 메인 루프 관리 및 메뉴 진입 인터페이스 | ![안선효１](https://github.com/user-attachments/assets/cef1ba3e-0462-4df5-9939-fa427c7bb141)|
|송지한| `feature/monster` |몬스터 데이터 정의 및 랜덤 생성, 난이도 조정 기능 |![image](https://github.com/user-attachments/assets/c03a74bc-ca96-4963-bdd9-cb76b1c52004)|
|정이량| `feature/player`  |	플레이어 상태 관리 및 상점 로직 구현 | ![image](https://github.com/user-attachments/assets/4b78cf0a-8c2d-4c54-b5db-61eeefdd9830)|
|박지환| `feature/combat`  | 전투 진행, 던전 탐색 흐름 및 결과 처리 |![image](https://github.com/user-attachments/assets/ed4f4a3f-98c7-40fc-b937-3cf8721e232d)|

***각 기능은 독립적이며, `main.py`에서 통합 후 호출하여 실행***

---

## 5. Git 협업 전략 및 구조

### 5.1 GitHub 원격 저장소와 로컬 환경(_VisualStudioCode_) 연결:

#### 1단계: 원격 조장소에 호스트가 `main` 브랜치 최초 생성

* 호스트가 최초로 README.md 파일을 `main` branch에 push하여 생성
 ![git 연결 및 등록 후 main branch 생성](https://github.com/user-attachments/assets/47c6f7cd-7707-4a70-853d-577e926d132b)



---

#### 2단계: 각 조원 원격 조장소와 연결 진행:

* 조원1 clone 복제 후, Git hub의 원격 저장소와 연결*
![image](https://github.com/user-attachments/assets/02c6c525-7577-4cde-968f-103efe9f6fd5)


* 조원2 clone 복제 후, Git hub의 원격 저장소와 연결*
![image](https://github.com/user-attachments/assets/502a755c-639c-4014-aaff-d3bd5b430780)


* 조원3 clone 복제 후, Git hub의 원격 저장소와 연결*
![image](https://github.com/user-attachments/assets/e34a5ff7-9c1e-42a7-b94b-718d768513f1)



---

### 5.2 브랜치 전략

 모든 팀원은 `main` 브랜치에 직접 작업하지 않고, 개인 기능은 각 조원 별로 브랜치에 구현후 `main`에 `merge`하여 진행

--- 
  - 팀원 각각 작업별 브랜치 등록
![모든 사람 최초로 각 기능별 파일 push 완료](https://github.com/user-attachments/assets/6fc5bec8-3257-422e-b75e-9938361132a9)

---

* 1차적으로 모든 팀원 코드 작성 완료
![모든 조원 1차 코드 작성 완료](https://github.com/user-attachments/assets/46551f16-d445-469d-8047-1d1c1945f694)


* merge 직전 각 작업 브랜치별 기능 완성
![branch 분기 많은거](https://github.com/user-attachments/assets/9a0d0ea4-f4d6-4698-a89f-069563949641)

---

* 각 조원들 브랜치 목록
![각 조원들 가지 목록(역할)](https://github.com/user-attachments/assets/dc95cad4-962a-40aa-a2f4-edd5ef645686)



```
feature/director   → 게임 디렉터리 및 흐름 제어 (안선효)
feature/monster    → 몬스터 시스템 (송지환)
feature/combat     → 전투 시스템 (박지환)
feature/player     → 플레이어 및 상점 시스템 (정이량)
```

---

**기능 구현이 완료된 후 각자의 브랜치에서 `main` 브랜치로 직접 `Pull Request`를 생성하여 병합**

---

### 5.3 `Pull Request` & 병합 방식

각자 할당된 브랜치에서 기능 개발을 완료한 후,
GitHub 상에서 `main` 브랜치로 `Pull Request(PR)`를 생성하여 병합을 요청.
PR에는 다음과 같은 내용을 포함하였다:
- 주요 변경 사항 설명
- 코드 리뷰 및 충돌 여부 확인

---


![pull request 4 최종본](https://github.com/user-attachments/assets/6afeeaaa-a4d7-4ec9-b57e-11a2a7f734a0)

**충돌이 발생할 가능성의 사전 대비책으로서, 로컬에서 사전 병합 테스트를 진행한 뒤
main 브랜치에 반영함으로써 안정적인 통합을 추구했다.**

---

- 첫번째 PR 요청
![1](https://github.com/user-attachments/assets/bd8d9b48-1a27-4ffb-9369-e1ee58b3e806)


---
- 두번째 PR 요청
![2](https://github.com/user-attachments/assets/e1ed5dee-33f1-4061-b610-f7132729a6fa)


---

- 세번째 PR 요청
![3](https://github.com/user-attachments/assets/89f049ed-2f6d-4d0b-8dc5-63e322a740dc)


- `merge` 후 최종 결과

![9 최종 merge 결과물 확인](https://github.com/user-attachments/assets/40bddff5-6c9c-4229-b307-c88f2457ffaf)

3개의 branch(*feature/director, feature/monster, feature/player*)는 main과 merge가 정상적으로 진행되었으나, 

**`feature/combat`을 merge 하는 과정에서 충돌 발생 !!**

---

### 5.4 마지막 `Merge` 진행중 충돌 발생

**`feature/combat` 브랜치가 마지막에 conflict 충돌 유발**
![5 merge conflict](https://github.com/user-attachments/assets/043a8494-0cb5-43fa-9642-2dfc33065b5d)


---

#### 충돌 원인:
![image](https://github.com/user-attachments/assets/3fd843fe-9b0f-47bc-b6c1-9445847efaf4)

1. 최종 `merge`를 대비해 사전에 로컬 환경에서 `practice` 브랜치를 만들어서 병합을 시도해보았음

2. 이 과정에서 실수로 **`feature/combat` 브랜치에 `pracitce` 브랜치를 `merge`하고 `push`**를 해버려서 원격 저장소까지 영향을 미침

3. 결정적으로 confilct 충돌이 난 원인은 `feature/combat` **브랜치의 2개의 파일(`dungeon.py`, `combat.py`)은 다른 파일들(main에 있는 몇개의 파일)을 `import`해서 사용하는 형태로 구현했지만**,

4. **이 2개의 파일만 있는 `feature/combat` 브랜치**에서 `pull request를 보내면`, **해당 파일들은 다른 파일들 없이는 당연히 실행이 불가능 하기에 Git이 이를 오류로 인식**

5. **`Pull request` 실패로 귀결**

---

### 해결 방법:

![image](https://github.com/user-attachments/assets/9594eb62-8288-470c-8d89-69f7d7fd0c96)


1. 우선 PR검사를 통과한 **`merge`된 6개의 `main` 브랜치의 파일들을 *`feature/combat`* 브랜치로 가져옴**
2. 그 후 *`feature/combat`* 브랜치를 **github에 `Push`**
3. 그러면 *`feature/combat`* 브랜치는 **github의 `Pull Request`검사를 통과**
4. 원래의 *`feature/combat`* 브랜치의 2개의 파일들을 포함한 총 8개의 파일들을 `main` 브랜치로 `merge`하여 해결

 **_즉, `main`의 파일 6개를 `feature/combat`로 이동 -> `feature/combat`에서 PR검사 통과 -> `feature/combat`와 `main`을 `merge`_**

---

**Pull Request를 통과한 *`feature/combat`* 브랜치에서, 2개의 (`dungeon.py`, `combat.py`) 파일들을 로컬로 `pull`하였음.**

![image](https://github.com/user-attachments/assets/44e1a184-431b-4585-99f7-f2ac09089eed)

---

![11](https://github.com/user-attachments/assets/c6f24fc0-192c-4f53-9ea1-41ae3d63f06d)

---

**성공**
![10](https://github.com/user-attachments/assets/c42d4b2c-0240-44da-a900-33aaa9f45049)

---

**완성 후 최종 실행**
![image](https://github.com/user-attachments/assets/d9d85e7c-8955-4e63-a504-8c00c39dbd08)


---

## 6. 구현 상세 (각 조원 별)

**팀원 1 (안선효) - 게임 총괄(디렉터 담당)**

- **기능 요약:** 게임 전체의 흐름을 제어하는 디렉터 역할을 수행하며,
  플레이어의 선택에 따라 전투, 상점, 종료 기능을 연결하는 중앙 통제 허브를 구현
- **사용 기술:** 함수 분기, 조건문, 모듈 간 호출, 게임 루프 설계, 플레이어 상태 관리
- **주요 함수:**
  `main_loop(player)`: 메인 게임 루프
  `start_game()`: **_player_**는 `import`로 클래스 이름을 인자로 받아옴, 게임 시작
  choice-handling을 통한 게임 루프 제어
- **코드 위치:** `game_manager.py`, `main.py`
- **실행 예시:**
  ```
  [1] 던전 입장
  [2] 상점 방문
  [3] 게임 종료
  선택 >> 
  ```

- 특이사항:
  - `main.py`에서 `player` 객체를 생성 후 `main_loop(player)`로 흐름 진입

  - 모든 기능은 독립 모듈에 위임되어 있으며, 중앙에서 호출만 담당

---
**팀원 2 (송지한) - 몬스터 데이터 구현**

- **기능 요약:** 다양한 난이도의 몬스터 정보를 정의하고 관리하며,
  전투에서 사용할 수 있도록 몬스터 목록을 클래스 기반 객체로 구조화함
- **사용 기술:** 속성 할당, 랜덤 선택, 데이터 구조화, 함수 리턴
- **주요 함수:**
  `Monster`: 몬스터의 체력, 공격력 등 기본 속성을 가짐
  `get_monster_list()`: 몬스터 객체 리스트 반환
  `get_random_monster()`: 전투에 사용할 랜덤 몬스터 선택
- **코드 위치:** `monster_data.py`,`coin.py`
- **실행 예시:**
  ```
   monsters = get_monster_list()
   print(monsters[0].name, monsters[0].attack)
  ```
- 특이사항:

  - `combat.py`에서 전투 시작 시 `get_random_monster()`를 사용

  - 다양한 난이도와 타입의 몬스터 확장 가능성을 고려한 설계

---
**팀원 3 (정이량) - 플레이어 및 상점 구현**

- **기능 요약:** 플레이어의 상태(체력, 공격력, 골드 등)를 관리하며,
  상점 시스템을 통해 아이템 구매 구현함.
  전투와 게임 전반의 진행에 핵심이 되는 플레이어 객체 구조 및 경제 시스템을 담당
- **사용 기술:** 리스트 및 딕셔너리 조작, 조건 분기, 상호작용 메뉴, 데이터 구조화
- **주요 함수:**
  `Player`: 플레이어의 능력치, 인벤토리, 상태 관리 클래스
  `display_shop(player)`: 상점 진입 및 상품 목록 출력
  `buy_item(player, item)`: 골드 차감 후 아이템 구매
  `sell_item(player, item)`: 아이템 판매 및 골드 획득
- **코드 위치:** `player.py`, `shop.py`
- **실행 예시:**
  ```
  [상점 입장]
  1. 체력 회복 포션 - 30G
  2. 능력치 상승 - 20G
  3. 나가기
  선택 >>
  ```

- 특이사항:

  - player 인스턴스는 `main.py`에서 생성

  - 다른 모든 기능(전투, 상점 등)에서 상태가 공유됨

  - 상점에서는 플레이어의 소지 골드에 따라 구매 제한 조건이 적용됨

---
**팀원 4 (박지환)** - 던전 및 전투 구현

- **기능 요약:**  플레이어가 던전에 진입하여 몬스터와 전투를 진행하는 핵심 전투 시스템을 구현.

  공격, 회복, 도망 등 다양한 선택지를 통해 게임의 재미와 전략성을 강화하며,

  실제 게임 진행의 중심이 되는 전투 로직과 승패 판정 흐름을 담당.
- **사용 기술:** 클래스 상호작용, 랜덤 처리, 조건문 및 반복문, 전투 시나리오 흐름, 상태 업데이트
- **주요 함수:**
  `enter_dungeon(player)`: 던전 입장 및 몬스터 생성
  `combat(player, monster)`: 전투 루프 시작
  `attack(player, monster)`: 플레이어의 공격 처리
  `monster_attack(player, monster)`: 몬스터의 공격
- **코드 위치:** `dungeon.py`, `combat.py`
- **실행 예시:**

  ```
   [던전 입장]
  몬스터가 나타났다! (고블린 / 체력 50 / 공격력 10)
  1. 공격
  2. 회복
  3. 도망
  선택 >> 
  ```

- 특이사항:

  - 전투 중에는 플레이어와 몬스터의 상태를 실시간으로 출력

  - 전투 승리 시 보상 지급, 패배 시 게임 종료 등의 흐름 제어 포함

  - 전투 알고리즘은 단순하지만 전략 선택이 가능하도록 설계



## 7. 회고


### 7.1 Git 협업을 통해 얻은 점:

- 개인 작업을 각각의 브랜치로 분리하고 PR(Pull Request) 기반으로 병합하는 과정을 통해, 실제 오픈소스 개발처럼 버전 관리의 흐름을 체득할 수 있었음.

- `merge` 후 conflict 문제를 직접 겪고 해결하면서 단순 명령어 암기가 아닌 문제 상황에 맞는 Git 전략 사용법을 실전처럼 학습함.

- 기능 구현을 협업 구조와 모듈화 전략을 통해 고려하면서, 전체 시스템의 일관성과 재사용성을 우선하는 개발 습관을 기를 수 있었음.

- 파이썬의 모듈화 방식을 Github의 협업 능력과 연관하여 파이썬 언어의 작동 로직 이해와 Git의 사용 방법을 습득함.

- 팀원 간 커뮤니케이션을 통해 작업 흐름 조율, 기능 인터페이스 통일, 중복 방지 전략을 실현하며 실질적인 협업 감각을 익히고 그 중요성을 몸소 깨달았음. 
---

### 7.2 아쉬운 점 및 개선 아이디어

- 프로젝트 초기에는 역할 분담과 브랜치 전략에 대한 명확한 가이드가 부족해 브랜치 생성 위치나 병합 타이밍에서 충돌이 발생함. 초기 설계 단계에서 작업 흐름에 대한 구체적인 합의(파일명, 브랜치명 등의 통일)가 필요했음.



- 초기에 주제를 선정할 때 공학용 계산기로 선정하려 했으나 주제의 독창성과 창의성이 부족하다고 판단되어 다른 주제를 정하느라 시간 소요가 많았음. 향후 주제 선정 시 여러 주제들을 후보로 선정하고, 각 주제들별로 간단하게 프로그래밍 해보며 방향성을 정하면서 개발해야 한다고 느낌


- 각 기능이 독립적이다 보니 통합 시 데이터 공유 방식을 고려하지 못해 중복된 정보 관리나 상태 동기화에 어려움을 겪음. 기능별로 상호관계를 명확하고 구체적으로 계획해야 한다고 깨달음.


- 실행 구조를 설계할 때 각 파일에서 서로 복잡하게 호출하는 방식으로 구현하여 conflict 문제를 해결하는데 어려움을 겪었음. 처음부터 `main.py` 진입 지점에서 기능을 명확히 호출하고 출력 흐름을 통제하는 방식으로 설계했다면 병합 시 혼란을 줄일 수 있었을 것.


- `merge` 시 **_conflict_** 문제를 해결하는데 상당한 시간이 소요되었음. **시간 소요의 대부분은 충돌원인을 찾지 못하는 것이었으며, 충돌 후에 복구하는 방법 등 대처하는데도 어려움을 겪었음**(사실 이번 프로젝트의 가장 큰 고비였습니다). 그러나 이번 프로젝트를 통해 conflict문제를 해결하는 경험을 함으로써 향후 git 활용 시 보다 능숙하게 대처할 것이라고 확신함.
 
---

## 9. 참고 자료

- [Markdown 문법](https://www.markdownguide.org/)


