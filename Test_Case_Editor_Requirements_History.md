v1.0.3 (2026-11-19)

* 1페이지 7·8. Test Flow (#cond) & Evaluation Criteria (#crit) 단일 통합 에디터 및 폰트 축소:

  * 7번(Test Flow)과 8번(Evaluation Criteria) 에디터를 1개의 전체 너비 에디터 창(#tcScriptInput)으로 통합하고 폰트 크기를 1px 축소(calc(0.9rem - 1pt - 1px)), 줄 간격(1.48)을 조정하여 한 화면에 더 많은 스크립트가 보이도록 개선.

  * Form View에서는 #cond1 → #crit1 → #cond2 → #crit2 순으로 통합 편집되며, PTC View 및 Excel/PTC Export에서는 기존과 동일하게 Test Flow와 Evaluation Criteria가 자동 분리됨.

  * * #cond, + #crit 버튼을 + #cond/crit 버튼 1개로 통합하여 클릭 시 다음 번호의 #condN / #critN 쌍을 한 번에 추가.

* Sidebar / Left Nav 여백 축소, 전체 삭제 배경색 강화, Utility HTML 추출 버튼 제거:

  * #sidebar 및 각 페이지 Left Nav 카드의 좌우 여백(padding)을 축소하여 공간 효율 개선.

  * Left Nav의 전체 삭제(#btnClearAllTestCases) 버튼에 고대비 Rose(#e11d48) 배경색과 흰색 텍스트 강제 적용.

  * Sidebar 하단의 Utility HTML 추출 버튼 제거.

* TC Import 시 공백 대신   /   등 & 엔티티 문자열 유입 버그 수정:

  * cleanPtcImportedRichText에서 & 이중 이스케이프(&nbsp;, &#160;)를 먼저 1차 해제한 뒤  ,  ,  ,  ,  ,  ,  ,   등 모든 공백 엔티티를 일반 공백(" ")으로 디코딩하도록 수정.
    v1.0.2 (2026-11-19)

* Auto-TA 시나리오·Trigger·Calculation 이름 규칙 통일:

  * 시나리오(Trace Analysis / Episode) <NAME>: TC\_{ID} 형식으로 자동 연동 (예: TC_2172601, ID 미입력 시 TC_AutoTA).

  * Trigger block <NAME>: TriggerBlock\[#Cond{N}\] 구문을 지원하여 각 조건 블록의 <NAME>을 #Cond1, #Cond2, ...로 출력.

  * Calculation <NAME>: 각 검증 항목의 <NAME>을 #Crit1, #Crit2, ...로 출력하며, .pkg의 TsTraceStepResult UUID는 #Crit{N} 섹션 번호와 수식 신호명으로 1:1 매칭되도록 개선.

  * Plot 이름은 기존대로 Plot\_{ID} 연동 유지, 2종 핵심 번들(ecu_test_integrity_admin.html + Test_Case_Editor_Requirements_History.md)로 패키징.
    v1.0.1 (2026-11-19)

* 릴리즈 체계 개편 (Test Case Editor 폴더 이관 및 v1.0.1 기준 버전 전환):

  * 기존 v50.96 최신 기능(Auto-TA Plot <NAME> TC ID 연동, Map/Vector \[x\]\[y\] 개별 인덱스 접근, Excel ==/#critN 보존, PTC TS 하위 Functional Test 전체 Import, 가이드 문법 규칙 1×2 그리드 등)을 기반으로 공식 버전 체계를 **v1.0.1**로 전환.

  * 배포·유지보수 번들 구성을 핵심 2종 파일(ecu_test_integrity_admin.html, Test_Case_Editor_Requirements_History.md)로 슬림화하여 Google Drive Test Case Editor 폴더 및 GitHub(yongjunpark03/Test-Case-Editor)와 일원화 관리.
    v50.96 (2026-11-19)

* Auto-TA Plot의 <NAME> 필드를 TC ID와 자동 연동:

  * extractWaitUntilAutoTaBlocks, parseTaAnalysisEpisodes, generateTaXmlContent, syncAutoTaPackagesFromTestCases, generatePkgXmlContent에서 TC ID(tc.id / tc.ptcId)가 존재할 경우 Plot의 <NAME> 필드를 Plot\_{TC_ID} (예: Plot_2172601)로 생성하도록 개선 (TC ID가 빈칸일 때는 기본값 Plot 유지).

  * *autoTaCache 캐시 키에 tcId를 포함하여 TC ID 변경 시 즉시 새 Plot 이름으로 갱신되며, Plot\[Plot*{TC_ID}\] 구문 파싱 시 이름이 신호 목록(VIRTUAL-SIGNAL / MAPPING-ITEM)으로 오인되지 않도록 처리.
    v50.95 (2026-11-17)

* 3. 가이드 (Guide) → 문법 규칙 탭 전면 정리 (누락 문법 추가 + 비침범 컨테이너 + 1x2 와이드 블록 배치):

  * 누락 문법 추가 및 ID별 전용 메타데이터 분리:

    * Map\[x\]\[y\] / Vec\[x\] 개별 인덱스 접근 (Check if {SIGNAL}\[x\]\[y\] {OP} {VALUE}, Set {SIGNAL}\[x\]\[y\] to {VALUE}) 카드 추가.

    * Ensure that {SIGNAL} {OP} {VALUE} (GRAM_ENSURE_THAT) 문법 추가.

    * #cond{N} / #crit{N} 섹션 블록 & 주석 (//, #) 레퍼런스 카드 추가.

    * 기존에 action(READ_VERIFY, MULTI_CHECK) 단위로만 묶여 동일한 예제가 중복 표시되던 Wait until {SIGNAL} {OP} {VALUE} (1 min 기본 Timeout), After trigger + {DELAY_SIGNAL} ms, From trigger for {DURATION_SIGNAL} ms, Multi-Check 3종(every test step, at least one test step, every test step at least once)을 문법 id별 전용 인자·API·예제로 각각 분리.

  * 블록 침범 방지 및 1x2 (grid-column: span 2) 와이드 카드 레이아웃 적용:

    * 모든 문법 카드(.guide-gram-card)와 내부 패턴/코드 박스(.guide-gram-pattern-box, .guide-gram-code)에 min-width: 0, max-width: 100%, overflow: hidden, word-break: break-word, overflow-wrap: anywhere를 강제하여 긴 문법 패턴이나 코드가 인접 카드를 침범하지 않도록 격리.

    * 상단 핵심 요약 카드 중 텍스트·예제가 많은 3번(Wait until & Multi-Check 3종 + within 타임아웃) 및 4번(Map/Vector \[x\]\[y\] 인덱스 & Auto-TA 트리거 문법) 카드를 1x2 와이드 블록으로 배치하고 좌(설명)·우(코드 예제) 2단 구조로 가독성 개선.

    * 하단 전체 문법 그리드(#guideFullGrammarGrid, 4열 grid-auto-flow: dense)에서도 패턴·설명·다중 라인 예제가 긴 문법(Set, Check if, Ensure that, Wait until, After/From trigger, Multi-Check 3종, Map\[x\]\[y\], #cond/#crit, If, Switch 등 17개)이 자동으로 1x2 (grid-column: span 2) 칸을 차지하도록 구현.
      v50.94 (2026-11-17)

* TC 에디터 Map (\[x\]\[y\]) 및 Vector (\[x\]) 개별 인덱스 접근(Check if {signal_map}\[0\]\[1\] == ..., Set {signal_map}\[0\]\[1\] to ... 등) 완벽 지원:

  * parseLine에서 Check if TCU_ShiftPattern_Map\[0\]\[1\] == 5, Check if $shift_map$\[0\]\[1\] == 5(Helper Signal + 인덱스), Wait until TCU_ShiftPattern_Map\[0\]\[1\] == 5, Read TCU_ShiftPattern_Map\[0\]\[1\] Into var, Signal read TCU_ShiftPattern_Map\[0\]\[1\] 및 명령어 뒤 공백이 생략된 Check if{signal_map}\[0\]\[1\] 형태까지 모두 파싱하도록 구현.

  * 인덱스가 지정된 Map/Vector 요소({signal_map}\[0\]\[1\])는 .pkg 생성 시 전체 행렬(xaMeasMatrixVariable / MAP)이 아닌 개별 스칼라 요소(ID="TCU_ShiftPattern_Map\[0\]\[1\]", LABEL="TCU_ShiftPattern_Map\[0\]\[1\]", xaMeasValueVariable, DATA-TYPE="VALUE")로 매핑·검증되며, 인덱스가 없는 Check if TCU_ShiftPattern_Map == 5는 기존대로 전체 행렬(matrixAllExpression, DATA-TYPE="MAP")로 검증.

  * Set {signal_map}\[0\]\[1\] to 5 작성 시 전체 배열(0 \~ N-1) 일괄 전개가 아닌 지정된 단일 요소(OLTCU_TCU_ShiftPattern_Map\[0\]\[1\])만 Write하도록 computeOverrideSignalNames 정밀화.

  * Auto-TA 및 5페이지 TA 에디터(normalizeTaSignalPath, resolveAswSignalName)에서도 {signal_map}\[0\]\[1\] 및 $helper_map$\[0\]\[1\] 인덱스를 보존하여 <VIRTUAL-SIGNAL> 및 <FORMULA>에 정확히 매핑.

  * 신호 자동완성(querySignalsWithWildcardAndRanking, renderSignalAutocompleteDropdown)에서 Map/Vector 신호 옆에 MAP \[30\]\[6\] / VEC \[6\] 배지를 표시하고, 신호명 뒤에 \[ 입력 시 \[0\]\[0\], \[0\]\[1\] 인덱스를 자동 추천하며 직접 입력한 \[0\]\[1\] 인덱스가 덮어써지지 않도록 개선.
    v50.93 (2026-11-17)

* Excel Export → Import 시 Evaluation Criteria == 변형 및 #critN 누락 버그 수정:

  * cleanPtcImportedRichText 내의 광범위한 정규식(/<\[^>\]+>/g)이 다중 라인에 걸친 </<= 연산자와 >/>= 연산자 사이 구간(<= ... #crit2 ... #crit3 ... >=)을 HTML 태그로 오인하여 중간 #critN 블록을 삭제하고 연산자를 단일 =로 병합하던 원인을 제거하고, 알려진 실제 HTML 태그만 안전하게 제거하도록 수정.

  * matchUnifiedPackageMapping 및 findBestWildcardRuleMatch 최상단에 비교/검증 문법(Check if, Ensure that, Wait until ... == ..., After trigger, From trigger, ==, !=, >=, <=, <, >) 보호 가드를 추가하여 와일드카드 패키지 매핑이 비교식을 변형하지 않도록 차단.

  * parseSectionGroups, combineInterleavedFlowAndCrit, splitScriptIntoFlowAndCrit, canonicalizeImportedPtcScript에서 빈 #critN 블록 및 번호별(#condN ↔ #critN) 1:1 매칭을 보존하고, 비교식 내 단일 = 입력 시 자동으로 ==로 정규화하도록 개선.

* PTC Test Suite (TS) ID Import 시 하위 모든 TC ID 조회 및 Functional Test 전체 Import 구현:

  * bridge/ptc_local_bridge.py (resolve_suite_or_tc_import) 및 스튜디오 JS(expandTestSuiteChildTestCasesViaBridge, runUtility4PtcIdImport, parsePtcRawResponseToTestCases, applyParsedPtcListToStudio) 양쪽 모두에서 TS ID 입력 시:

    1. im issues --queryDefinition=(field\[Document ID\]=<TS_ID>) --fields=ID,Category,Type --delim=\\t --batch (im issues에서 오류를 유발하던 --showRichContent 제거) 및 im viewissue <TS_ID>의 Contains 계층 트리(하위 Heading/Section 내부 Contains 재귀 포함)에서 모든 하위 TC ID를 수집.

    2. 수집된 하위 ID들을 im viewissue --showRichContent --batch로 일괄 조회한 뒤, TS 문서 자체·Heading·Comment·Non-Functional Test를 제외하고 Category == "Functional Test"인 모든 Test Case를 에디터에 일괄 Import하도록 수정.
       Test Case Editor
       v50.92 (2026-11-16) — 1페이지 Test Suite Overview \[전체 삭제\] 버튼 레이아웃 정렬 및 전 페이지 Nav 단일 화면(무스크롤) 고밀도 여백 축소

1. 1페이지 Test Suite Overview 액션 버튼(+ 추가 · 복제 · 전체 삭제) 레이아웃 정렬:

   * Test Suite Overview 제목과 3개 버튼이 한 줄에서 좁은 Nav 폭을 초과해 전체 삭제가 카드 밖으로 벗어나던 문제를 수정하여, 제목 하단 3열 균등 그리드(grid-cols-3 gap-1)로 + 추가 / 복제 / 전체 삭제 버튼을 카드 내부 폭에 맞게 깔끔하게 정렬.

2. 전 페이지 좌측 Nav 및 글로벌 사이드바(#sidebar) 세로 여백·패딩·마진 간소화 (한 화면 표시):

   * #sidebar, #leftEditorSubSidebar(1페이지), #loadedFilesManagerPanel(2페이지), #taLeftSubNav(5페이지) 등 모든 Nav의 카드 내부 패딩(0.38rem 0.48rem), 카드 간 간격(0.35rem), 버튼/입력창 세로 패딩(0.16rem\~0.2rem), 빈 파일 목록 영역(:empty { display: none }) 및 TC 리스트 높이(max-h-\[210px\])를 최적화하여 스크롤 없이 한 화면에 들어오도록 개선.
     v50.91 (2026-11-16) — 7개 페이지 각각 단일 페이지 User HTML 추출 Unit Test 전수 수행 및 발견된 3대 버그 수정

3. 단일 페이지 User HTML 추출 시 renderAll() 동적 탭 감지 (view-\${activeTab}):

   * editor가 포함되지 않은 단일 페이지 User HTML(signals, ecutest, grammars, taeditor, utility, roadmap 단독 추출)을 열었을 때 renderAll()이 무조건 editor나 utility로 강제 리다이렉트하던 로직을 수정하여, 실제 DOM에 존재하는 view-\${activeTab}을 자동 감지해 렌더링하도록 개선.

4. 3. Guide > 실험실(Lab) 역직렬화 .pkg 다운로드 함수명 수정 (#btnLabDownloadDeserTestPkg):

   * 존재하지 않던 generatePackageXmlFromTc 대신 generatePkgXmlContent(LAB_DESER_TEST_TC, 5, { includeTa: false })를 호출하도록 수정하여 LAB_2024_3_Deserialization_AllInOne.pkg (19,612 bytes)가 즉시 생성·다운로드되도록 복구.

5. 6. Utility > 3. Text/XML Split 미리보기 접힘 상태 온디맨드 복사/다운로드 연산 (#btnUtilCopySplitResult, #btnUtilDownloadSplitTxt):

   * 결과 미리보기가 접혀 있을 때도 복사 또는 .txt 다운로드 클릭 시 즉시 computeUtilityTextSplitResult()를 연산하여 빈 문자열이 복사/다운로드되지 않도록 수정.
     v50.90 (2026-11-16) — User HTML 전 페이지 조합 이벤트 중단(TypeError) 원천 차단 · 전체 버튼 전수조사 복구 · 3. Review Table 검증 테이블 기본 접기 및 좌측 Nav 정리

6. User HTML 배포 시 페이지 조합 무관 전체 이벤트 리스너 100% 등록 보장:

   * stripTaggedScriptBlocksByScope에서 UTILITY_ONLY / ADMIN_ONLY 블록을 강제 삭제하던 로직을 비활성화하여, 1. TC 에디터가 공유하는 copyPowerShellLiveBridgeToClipboard (Py 브릿지), downloadPythonBridgeLauncherBat (.py), runUtility4PtcIdImport (ID Import), applyParsedPtcListToStudio, parsePtcRawResponseToTestCases, ensureUtilityStateInitialized, renderVariantManager, renderPrePostPresets 등이 절대 누락되지 않도록 수정.

   * initEvents() 내 syncSigHelperInputState() 및 \["sigName", "sigSystem", "sigMappingType"\] 바인딩에서 2페이지(signals) 미포함 배포 시 발생하던 Cannot read properties of null 예외를 완벽히 방어하여, 이후 등록되는 모든 버튼(전체 삭제, + 추가, tcIdInput\~tcPostInput, tcScriptInput/tcCritInput 자동완성, .pkg/.xlsx Export, 3. Review Table 토글, TA Editor, 테마 전환 등)이 어떤 페이지 선택 조합에서도 100% 정상 동작하도록 전수 복구.

7. 3. Review Table 검증 테이블 접기/열기 수정 및 좌측 Nav 메뉴 정리:

   * renderActiveTestCaseEditor() 및 북마크 탭 전환 시 if (curEdTab === "REVIEW") state.showValidationTable = true;로 매번 강제 열림 처리하던 코드를 제거하여 #btnToggleValidationTable(검증 테이블 열기 / 검증 테이블 접기) 클릭 시 즉시 접기·열기가 동작하도록 수정.

   * 초기 로드 및 User HTML 배포 시 state.showValidationTable = false (기본 접기 상태)로 설정.

   * 검증 테이블이 3. Review Table 책갈피로 분리됨에 따라 1. TC 에디터 좌측 사이드바(#leftEditorSubSidebar)의 미리보기·렌더링 열기/접기에서 2) 검증 테이블 토글 버튼을 삭제하고 1) Export 미리보기, 2) TC Overview 목록으로 정리.

(ECU-TEST 2024.3 \*.pkg & PTC Integrity Studio) — 전체 요구사항 히스토리 및 명세서 (v50.19)

본 문서는 지금까지 Test Case Editor 개발 과정에서 요청하신 모든 기능 및 UI/아키텍처 요구사항을 시간순 및 기능 영역별로 정리해 보관한 통합 명세서입니다.

 1. UI 디자인, 테마 및 레이아웃 요구사항

 2. 상단 타이틀 배지 및 네비게이션 정리:

    * 상단 메인 타이틀 배지에 Halcyonic 대신 STUDIO 배지 사용.

    * 상단/사이드바 네비게이션 타이틀에서 고정된 버전 문구(v26)를 제거하고 Test Case Editor로 깔끔하게 정리.

 3. Halcyonic 테마 입체 음영 정리:

    * 모서리가 둥근 창(카드/컨테이너) 주변에 검은색 입체 그림자처럼 보이던 음영(box-shadow)을 제거하여 지저분해 보이지 않도록 개선.

 4. Helper Signal 버전 선택 버튼 시인성 개선:

    * 1. TC 에디터의 L2 / L4 버전 선택 버튼에서 현재 선택된 버튼에 고대비 배경색(#0284c7)과 굵은 테두리, 체크(✓) 표시를 넣어 시인성을 극대화.

 5. 에디션 이원화 (Admin / User) 및 내장 한/영(KO / EN) 언어 전환:

    * 배포 HTML 파일을 Admin 에디션(ecu_test_integrity_editor_admin.html)과 User 에디션(ecu_test_integrity_editor_user.html) 두 가지로만 구분하여 구성.

    * User 에디션에서는 3. 문법 규칙 및 6. To-Do & 현황 탭을 볼 수 없거나 편집할 수 없도록 숨김 처리.

    * 별도의 영문 HTML 파일을 분리하지 않고, 각 HTML 상단 헤더의 KO 한국어 / EN English 언어 선택 버튼을 통해 에디터 내부에서 실시간으로 한/영 전환이 가능하도록 통합.

 6. 패키지 번들 경량화:

    * \_halcyonic.html 파일 및 별도 외부 샘플 .xlsx 파일들을 번들에서 모두 제외하고, 에디터 내부 버튼으로 즉시 템플릿/샘플 생성이 가능하도록 경량화.

 7. 자동완성(Autocomplete) 및 신호 검색 알고리즘 요구사항

 8. 키보드 화살표 이동 시 스크롤 자동 추적:

    * 자동완성 드롭다운 목록에서 위/아래 화살표(↑ / ↓)로 이동할 때 선택된 커서 항목을 따라 스크롤이 자동으로 이동(scrollIntoView({ block: 'nearest' })).

 9. ESC 키 닫기 지원:

    * 자동완성 창이 열려 있을 때 ESC 키를 누르면 즉시 자동완성에서 빠져나올 수 있도록 처리.

10. 첫 글자 고정 매칭 + \* 와일드카드 및 다단계 랭킹 탐색 알고리즘:

    * 첫 글자가 S이면 첫 글자가 S가 아닌 신호들은 제외하도록 첫 글자 앵커링 적용(단, \*로 시작하는 와일드카드 검색 시에는 중간 문자열 매칭 허용).

    * * 와일드카드(예: S\*Typ, \*Spd) 및 대문자/언더스코어 약어(Acronym, 예: SVT $\rightarrow$ ShS_ValTyp) 퍼지 스코어링 탐색 알고리즘 적용.

11. 환경별 (SIL / HIL-ETAS / HIL-dSPACE) 데이터 사전 아키텍처

12. 플랜트 모델 및 환경별 신호 접근 분리:

    * SIL, HIL-ETAS, HIL-dSPACE 환경마다 접근 가능한 플랜트 모델 신호 및 타겟 경로(SIL Target Path, HIL-ETAS Target Path, HIL-dSPACE Target Path)를 분리 관리하는 통합 데이터 사전 구성.

13. 신호 사전(2. 신호 사전) UI 구성:

    * 상단 파일 로드 바에서 1. A2L (.a2l) 불러오기, 1-1. Helper L2 로드, 1-2. Helper L4 로드를 나란히 배치하고, 이어서 2. CAN DBC (.dbc) 불러오기, 3. Excel (.xlsx/.csv) 불러오기, 4. Override 폴더 스캔 (\*\_Override.c)을 배치.

    * 새로운 데이터 사전 구조에 맞춰 전체 신호, A2L (L2·L4 Helper), DBC 수신 (Rx), DBC 송신 (Tx), Plant Model (SIL·HIL), Override 매핑됨 아키텍처 분류 필터 탭 제공.

14. A2L 신호, Helper L2/L4 및 \*\_Override.c 기반 Override 자동 생성

15. Helper Signal L2 / L4 이원화:

    * A2L 신호의 하위 분류로 L2 Helper Signal, L4 Helper Signal, Override Signal을 지원하며, 1. TC 에디터에서 L2 / L4 버전을 즉시 전환 가능.

16. Vector / Matrix 읽기(tsRead) 기본 표현식:

    * Vector나 Matrix 신호를 tsRead할 때는 단일 원소(vectorSingleExpression) 대신 vectorAllExpression 및 matrixAllExpression을 기본 사용.

17. 폴더 자동 스캔 (webkitdirectory) 및 {component}\_Override.c 파싱 규칙:

    * 특정 폴더 또는 \*\_Override.c 파일 로드 시 내부의 매크로/함수를 자동 탐색 및 파싱:

      * 스칼라 신호: DEFINEOLVAL({SIGNALNAME}, {DATA_TYPE}, {COMPONENT_NAME}) $\rightarrow$ OL{COMPONENT_NAME}*{SIGNALNAME} 및 Swt{COMPONENT_NAME}*{SIGNALNAME} 자동 생성.

      * 배열(Vector/Matrix) 신호: DEFINEOLVALA({SIGNALNAME}, {DATA_TYPE}, {COMPONENT_NAME}, {ARRAY_SIZE}) $\rightarrow$ 원본 신호가 크기가 있는 배열(예: \[30\]\[6\], 총 크기 180)인 경우 OL{COMPONENT_NAME}*{SIGNALNAME}\[0\] \~ OL{COMPONENT_NAME}*{SIGNALNAME}\[{ARRAY_SIZE}-1\]까지 모든 방에 개별 접근 및 일괄 인가(tsWrite)가 가능하도록 전개.

18. 일괄 tsWrite 동작 및 환경 제약:

    * 배열 신호를 tsWrite할 때 OL{prefix}*{signalname}\[0\] \~ OL{prefix}*{signalname}\[size-1\]에는 사용자가 원하는 {Value}를 일괄 tsWrite하고, Swt{prefix}\_{signalname}는 Enable Switch 개념으로 배열 없이 항상 1(또는 설정된 Swt 값)로 함께 tsWrite.

    * 모든 A2L Override 신호는 MODEL-KEY = Plant Model을 사용하며 SIL 환경 전용으로 동작.

19. 5. Override 매핑 UI 경계 및 컨트롤 명칭 규칙 (2. 신호 사전 & 5. PKG 변환 공통):

    * 5. Override 매핑 영역은 고대비 컬러 테두리로 경계를 명확히 구분.

    * 컨트롤 명칭:

      * Override 매핑 적용 (구: A2L tsWrite 시 Override 적용)

      * Swt 활성화 (구: Swt{prefix}\_{signalname} 포함 (선택))

      * 불필요한 "A2L(ECU-KEY) tsWrite Signal Override 매핑 :" 문구 삭제

      * OL Tag, Swt Tag (구: OL 접두어, Swt 접두어)

    * OL Tag 및 Swt Tag 빈 값 허용: OL Tag나 Swt Tag 입력란의 값을 모두 지워 비워두더라도 OL이나 Swt가 다시 자동 복원되지 않고 빈 접두어 상태가 그대로 유지됨.

20. DBC 신호 파싱, Rx/Tx 판별, Global Mapping 및 환경별 Read 변환

21. 편집 가능한 기준 노드(Transceiver) 기반 Rx/Tx 구분:

    * DBC 파일 로드 시 사용자가 지정/편집 가능한 기준 노드(Transceiver, 예: TCU_Node)를 기준으로 수신(Rx)과 송신(Tx) 신호를 자동 판별 및 실시간 재판별.

22. Rx 신호 Override 자동 생성 및 Global Mapping 연동:

    * 모든 Rx 신호에 대해 OL\_{CanSignal} 및 Swt\_{CanSignal} 오버라이드 신호 자동 생성 (MODEL-KEY = Plant Model, SIL/HIL 공통 사용).

    * SIL Override Path (기본값): Plant model/OL\_{CanSignal}로 자동 생성.

    * HIL Override Path (Optional): 하드웨어 환경마다 경로가 상이하므로 사용자가 추후 입력하거나 Global Mapping 파일(.xam / .xlsx)로 임포트/익스포트할 수 있도록 Optional 필드로 제공.

23. DBC 신호 읽기 (tsRead / Evaluation Criteria):

    * 에디터의 사용 가능 신호 목록에는 순수 Signal Name 기준으로만 깔끔하게 등록.

    * SIL 환경: "CAN\_{CANID}*{MESSAGENAME}*{SIGNALNAME}" 양식의 경로(xaModelSignal) 사용.

    * HIL 환경 (HIL-ETAS / HIL-dSPACE): ECU-TEST의 Bus-Read (xaBusSignal, tsRead + expectation) 기능을 통해 버스에서 직접 읽도록 변환.

24. IT 테스터 대량 신호 자동 TC 생성 및 JSON 저장/복원

25. IT 테스터 대량 신호 Write/Read 엑셀 임포트 (1페이지 하단 숨김 도구):

    * 1. TC 에디터 좌측 하단의 접이식 도구에서 엑셀 임포트 시 A열(step)과 C열부터 값이 연속으로 존재하는 마지막 열까지의 모든 신호를 자동으로 읽어 각 스텝마다 일괄 tsWrite 및 tsRead하는 Test Case 자동 생성.

26. JSON 파일 저장(JSON 저장) 및 불러오기(JSON 열기):

    * 워크스페이스 JSON 파일 저장 및 로드 시 Override 매핑 설정(a2lOverrideConfig)과 전체 Override 매핑 테이블 값(signalOverrideMap), 타겟 환경(targetEnv), DBC 기준 노드(dbcTransceiverNode), Helper L2/L4 사전까지 모두 포함하여 저장 및 복원.

27. v44.1 추가 요구사항 (배지 제거, KOR/ENG 테마형 토글, 5,000+ DBC 신호 렉 최적화 및 Override 20개 페이징)

28. Admin / User 에디션 배지 삭제:

    * 상단 헤더의 ADMIN 에디션, USER 에디션 배지 완전 삭제.

29. 한/영 전환 버튼 테마 스위치 스타일(KOR / ENG) 토글 적용:

    * 상단 헤더의 테마 선택 버튼(.theme-switcher-group / .theme-switch-btn)과 동일한 알약형(Pill) 디자인으로 통일하고, 문구를 KOR, ENG로만 표시하며 클릭 시 토글 방식으로 즉시 전환.

30. 5,000개 이상 대용량 DBC 파일 로드 시 렉(Lag) 원인 분석 및 최적화 + Override 매핑 20개씩 페이징:

    * 원인 분석:

      1. 5,000개 DBC 신호 로드 시 약 4,000\~5,000개의 Rx 신호가 signalOverrideMap에 등록되면서, 페이징이 없던 renderOverrideMappingTable()이 매 렌더링마다 5,000개의 <tr> 행과 30,000개 이상의 <input> DOM 노드 및 35,000개의 개별 이벤트 리스너를 한꺼번에 생성·교체하여 심각한 브라우저 렌더링 블로킹 발생.

      2. flushSaveToStorage()에서 5,000개의 signalOverrideMap 객체가 중복 직렬화되어 동기식 localStorage.setItem에 매 500ms마다 기록되고, saveLargeSignalsToIdb()가 신호 변경이 없을 때도 매 타이핑마다 5,000개 신호를 복제·저장하던 병목 존재.

      3. 기본 한국어(KOR) 상태에서도 매 렌더링마다 applyStudioLanguageToDom()이 전체 DOM TreeWalker를 순회하던 불필요한 오버헤드 존재.

    * 최적화 및 20개 페이징 적용:

      1. 5. Override 매핑 테이블 20개씩 페이징(20개씩 기본값, 50 / 100 / 200 선택, 이전/다음/페이지 직접 이동) 및 검색/구분 필터 추가: 신호 사전 테이블과 동일하게 한 화면에 20개 행만 렌더링하고 이벤트 위임(Event Delegation)을 적용하여 DOM 노드 수를 35,000개 $\rightarrow$ 140개로 99.6% 절감 (페이지 전환 5ms 이내).

      2. 인덱스 사전 정렬 캐싱(sortedByNameAsc) 및 메타데이터 캐싱(\_metaCachedName): 5,000개 신호 정렬/탐색 시 매번 정규식 분할이나 재정렬을 수행하지 않도록 캐싱.

      3. localStorage 및 IndexedDB 저장 최적화: 신호 데이터가 실제로 변경된 경우에만 IndexedDB에 저장하도록 개선.

31. v44.2 추가 요구사항 (ENG 완전 영문화, User 에디션 탭 원천 차단, DBC 순수 신호명 자동완성 및 .xam 스키마 정합성)

32. ENG 전환 시 100% 완전 영문화:

    * HTML 정적 텍스트/속성(placeholder, title, aria-label)뿐만 아니라 동적 렌더링 테이블 셀, 배지, 기본 설명문, 입력창(#tcDescInput, ##Comment block.)까지 모두 영어로 전환되어 한글이 남지 않도록 처리.

33. User 에디션 (ecu_test_integrity_editor_user.html) 3. 문법 규칙 및 6. To-Do & 현황 선택 원천 차단:

    * 사이드바 네비게이션(#nav)에서 3. 문법 규칙 및 6. To-Do & 현황 버튼 DOM 요소를 물리적으로 제거하고, CSS 및 탭 전환 핸들러에서도 차단하여 아예 선택할 수 없도록 수정.

34. DBC Signal 자동완성 시 순수 Signal Name만 표시 및 A2L 탐색 알고리즘 동일 적용:

    * 자동완성 드롭다운에서 DBC 파일명(system) 배지가 노출되지 않고 순수 Signal Name만 표시되도록 수정하며, DBC 파싱 시 신호명 앞의 불필요한 파일명/경로 접두어를 자동 제거.

    * DBC 신호 자동완성 및 Override 검색 시에도 A2L 신호 검색과 동일한 탐색 알고리즘(querySignalsWithWildcardAndRanking: 첫 글자 고정 버킷 + \* 와일드카드 + CamelCase/언더스코어 약어 랭킹)을 동일하게 적용.

35. Global Mapping (.xam) XML 스키마 규격 반영:

    * 루트 태그: <MASTER-MAPPING xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" format-rev="1">

    * 하위 <MAPPING-ITEM format-rev="2" xsi:type="mappingItem"> 내부에 Override 신호인 경우 <CATEGORY xsi:type="string">OpenLoop</CATEGORY> 생성.

    * <XACCESS xsi:type="xaModelSignal"> 하위에 <MAPPING-ENUM xsi:type="vtabInfoEmpty"/>를 포함하고, 같은 레벨의 <VARIABLE-PATH xsi:type="string">{SIGNAL_NAME}</VARIABLE-PATH>에는 경로 접두어 없이 순수 {SIGNAL_NAME}만 기입.

36. v44.3 추가 요구사항 (5. Text PTC/Excel 산출물 반영, DBC Override \_Phy/\_Swt 및 DBC Prefix 도입, Global Mapping Swt 필수 등록, Override 10개 페이징 및 컴팩트 UI)

37. 1. TC 에디터의 5. Text 필드 PTC 산출물 및 Excel Export 반영:

    * 4. PTC 산출물 미리보기 테이블 및 CSV, Excel XML(.xml), Excel(.xlsx) 내보내기의 11개 표준 컬럼(ID, Project Variant, State, Test Case Name, Text, Pre Conditions, Test flow, Evaluation Criteria, Post Conditions, Test Case Comment, Test Environment)에 5. Text(tc.description) 항목을 완벽히 포함.

38. DBC Override 신호 명명 규칙 변경 (\_Phy / \_Swt) 및 DBC Prefix 개념 도입:

    * DBC Override 전용 규칙 (A2L Override는 기존 OL{prefix}*{sig} / Swt{prefix}*{sig} 유지):

      * 기존 OL\_{CAN_SIGNAL_NAME} $\rightarrow$ OL\_{CAN_SIGNAL_NAME}*Phy (또는 {DBC_Prefix}*{CAN_SIGNAL_NAME}\_Phy)

      * 기존 Swt\_{CAN_SIGNAL_NAME} $\rightarrow$ OL\_{CAN_SIGNAL_NAME}*Swt (또는 {DBC_Prefix}*{CAN_SIGNAL_NAME}\_Swt)

    * DBC로부터 추가되는 Override 규칙을 재정의할 수 있도록 DBC Prefix(기본값 OL, 개별 행 Prefix 재정의 가능) 설정을 도입하고, JSON 파일 저장/열기(a2lOverrideConfig.dbcPrefix, dbcPhySuffix, dbcSwtSuffix)에 포함.

39. Global Mapping (.xam) 등록 시 Swt 관련 신호 필수 추가:

    * Global Mapping (.xam) 생성 시 물리값 신호(OL\_{CAN_SIGNAL_NAME}*Phy / OL{prefix}*{sig})뿐만 아니라 스위치 신호(OL\_{CAN_SIGNAL_NAME}*Swt / Swt{prefix}*{sig})도 항상 <MAPPING-ITEM>(OpenLoop 카테고리)으로 함께 등록.

40. Override 검색/테이블 페이지당 10개 표시 및 폰트·너비 축소(좌우 스크롤 제거):

    * 5. Override 매핑 테이블의 페이지당 기본 표시 개수를 10개(10개씩)로 변경.

    * 검색창 및 테이블의 폰트 크기(0.68rem)와 입력란 너비·여백을 전체적으로 컴팩트하게 축소(table-layout: fixed; width: 100%)하여 좌우 가로 스크롤 없이 한눈에 들어오도록 개선.

41. v45.0 추가 요구사항 (타겟 SIL/HIL 2원화 및 ETAS/dSPACE HIL Path 분리 저장, User 에디션 ENG 변환 오류 수정, Signal read {Signal} 문법 추가, SIGNAL RECORDING 활성화 및 On/Off 토글)

42. 타겟 실행 환경(SIL / HIL) 2원화 및 ETAS / dSPACE HIL Path 분리 저장:

    * 타겟 실행 환경 선택기를 SIL과 HIL 2가지로만 명확히 구분하도록 단순화 (1. TC 에디터의 11. Test Environment, 2. 신호 사전 상단 타겟 바, 5. PKG 변환 타겟 선택 공통).

    * ETAS와 dSPACE는 타겟 환경이 아니라 HIL Path에서 분리하여 각각의 경로(hilEtasOverridePath / pathHilEtas, hilDspaceOverridePath / pathHilDspace)로 개별 입력 및 저장되도록 구현 (2. 신호 사전, 5. Override 매핑 테이블, Override 엑셀 템플릿/임포트, 워크스페이스 JSON 저장/복원 모두 반영).

43. User 에디션 (ecu_test_integrity_editor_user.html) ENG 변환 오류 수정:

    * User 에디션에서 3. 문법 규칙 탭 버튼 제거로 인해 renderBadges() 호출 시 발생하던 #badgeGrammarCount 참조 오류를 완벽히 방어하고, STUDIO_I18N_SORTED_PAIRS 최장 길이 우선 정렬 및 신규 문구 영문 사전 등록을 통해 User/Admin 에디션 모두에서 KOR ↔ ENG 전환이 오류 없이 즉시 동작하도록 수정.

44. Signal read {Signal} 문법 규칙 추가 (MAPPING-ITEM 전용, TEST-STEP 미생성):

    * 기본 문법 규칙에 Signal read {Signal} (ID: GRAM_SIGNAL_READ, 액션: MAPPING_ONLY) 추가.

    * 해당 문법 사용 시 지정된 {Signal}을 <MAPPING> 하위의 <MAPPING-ITEM>에만 등록하고, <TESTSTEPS> 내부에는 어떠한 <TESTSTEP>도 생성하지 않도록 구현.

45. SIGNAL RECORDING (<TRACE-RECORDING>) 기능 활성화 및 On/Off 토글 제공:

    * .pkg XML 생성 시 </MAPPING> 바로 아래, <TESTSTEPS xsi:type="testCase"> 바로 위에 <TRACE-RECORDING format-rev="4" xsi:type="recordingManager"> 블록을 생성.

    * 7개 SIGNAL-GROUPS (Plant model, TCU-XCP, A-CAN, EOP-CAN, HIL_BOB, Plant2CAN, TCM) 및 각각의 고유 UUID가 포함된 7개 RECORDING-GROUP, SYNCHRONISATION-CONFIG, TRACE-MERGE-CONFIG (MODE=0, VALUE=merged), RECORD-ALL-TEST-QUANTITIES=True 메타 정보를 원본 스펙과 100% 동일하게 구성.

    * ECU-TEST에서 Package가 열리지 않는 경우를 대비해 5. PKG 변환 상단에 SIGNAL RECORDING On/Off 토글 스위치를 제공하여 언제든 켜고 끌 수 있도록 구현.

46. PKG 생성 시 Override 매핑 (MAPPING-ITEM & TEST-STEP) 정합성 복원 및 DBC Override 상시 활성화:

    * SIL 환경 Override 판정 우선순위 수정 (getEffectiveTargetEnv):

      * PTC Test Suite 임포트 데이터나 IT 대량 신호 자동 생성 TC의 11. Test Environment(tc.environment)에 "HIL" 또는 "HIL SIL"이 포함되어 있더라도, 스튜디오의 타겟 실행 환경 / PKG 변환 타겟 (state.targetEnv: 기본값 SIL)을 최우선 기준으로 적용하여 SIL 모드에서 A2L Override가 누락되거나 원본 A2L 신호(xaMeas\*)를 직접 Write하려던 문제를 원천 해결.

      * SIL 모드에서 Set {A2lSignal} to {Value}(또는 Helper $shift_type$) 작성 시 <MAPPING-ITEM>(CATEGORY=OpenLoop, MODEL-KEY=Plant Model, OL{prefix}*{sig} / Swt{prefix}*{sig})과 <TESTSTEP name="TsWrite">가 100% 생성되도록 보장.

    * DBC Override 신호 HIL / SIL 무관 상시 Enable 및 OL\_{CanSignal}\_Swt 상시 Enable:

      * DBC(BUS) 신호에 대한 Override(OL\_{CanSignal}\_Phy)는 타겟이 HIL이든 SIL이든, 그리고 A2L Override 체크박스 상태와 무관하게 항상 활성화(Enable)되어 <MAPPING-ITEM> 및 <TESTSTEP>에 생성.

      * DBC Override 스위치 신호인 OL\_{CanSignal}\_Swt 역시 Swt 활성화 옵션 여부 및 HIL/SIL 환경에 상관없이 항상 활성화(Enable, 값 1 인가)되도록 고정.

47. 대용량 Signal 포함 TC 로드 및 렌더링 성능 최적화 (Lag Free Engine)

* 원인 분석 (8,040줄 대용량 TC & 5,000개 Signal Override 맵 기준):

  1. resolveA2lWriteOverride() 및 computeOverrideSignalNames() 내부에서 매 WRITE 라인마다 Object.keys(state.signalOverrideMap).find(...)가 수행되어 $O(N \times M)$ 선형 탐색(약 1.6억 회 문자열 비교) 발생.

  2. renderAll() 호출 시 동일 스크립트(tc.script)에 대해 parseTestCaseScript() 및 extractPtcFlowAndCriteria()가 3\~4회 중복 실행되고, 매 줄마다 matchUnifiedPackageMapping() 정규식이 재컴파일됨.

  3. 8,000줄 이상의 TC 로드 시 validationTableBody에 8,000개 <tr>(48,000개 <td>), pkgStructureTree에 10,000개 <div>, codePreviewBox에 15MB 텍스트를 동기식 DOM 생성하여 브라우저 메인 스레드 프리징 발생.

* 최적화 적용 내역:

  * O(1) Override 해시 인덱싱 및 메모이제이션 (ensureOverrideLookupCache): state.signalOverrideMap의 소문자 키 Map 인덱스 및 resolvedWriteMap 캐시를 구축하여 대용량 Signal Write/Override 판별 속도를 \$O(1)$로 단축.

  * DSL 파서 메모이제이션 및 Package Mapping 정규식 사전 컴파일: ensureCompiledGrammars()에서 Package Mapping 정규식을 사전 컴파일하고, parsedScriptMemoCache 및 tc.\_ptcExtractCache / tc.\_splitCache로 중복 파싱 제거.

  * DOM 가상화/윈도잉 렌더링 (VALIDATION_DOM_RENDER_LIMIT = 200, CODE_PREVIEW_STEP_LIMIT = 250):

    * 전체 스텝 문법 검증(100% 전수 검사) 및 에러 행 전체 표시는 유지하면서, 정상 통과 행은 상위 200행 우선 렌더링 후 \[전체 N행 펼치기\] 버튼으로 즉시 확장 가능하도록 개선.

    * 실제 파일 다운로드(\*.pkg, .py, PTC CSV/XML)는 축약 없이 100% 전체 스텝을 그대로 출력하며, 8,040줄 TC 기준 로드(5,308ms → 123ms, 43배 가속), 탭 1 렌더링(4,764ms → 5.1ms, 934배 가속), 탭 5 렌더링(27,062ms → 28.7ms, 942배 가속) 달성.
      v46.0 주요 업데이트 내역 (Major Release — v46.0)

1. 버전 관리 체계 도입 (v{major_v}.{minor_v})

* 업데이트 규모에 따라 Major 버전과 Minor 버전을 구분(v46.0)하여 Google Drive 릴리즈 폴더(v46.0)에 아카이빙하도록 표준화.

2. 로드된 파일 관리 센터 (A2L · DBC · Helper Signal · Override 파일명 표시 및 개별 교체/삭제) & A2L-Helper 완전 분리

* 파일명 표시 및 개별 교체/삭제 (#loadedFilesManagerPanel):

  * 1. A2L 파일 (.a2l), 2. CAN DBC 파일 (.dbc), 3. Helper 파일 (L2/L4), 4. Override 파일 (.c/.xlsx/.xam) 총 4개 카테고리별로 업로드된 파일명과 적재 건수를 실시간 표시.

  * 각 파일 옆의 \[교체\] 버튼으로 해당 파일 데이터만 새 파일로 즉시 교체하거나, \[삭제\] 버튼으로 해당 파일 데이터만 선택 삭제 가능.

* A2L 삭제 시 Helper Signal 동반 증발 문제 해결:

  * 기존에는 A2L 삭제 시 xaMeas\* 타입 신호 객체가 일괄 제거되면서 그에 매핑된 Helper Signal($shift_type$ 등)까지 함께 유실되던 문제를 수정.

  * A2L 개별 파일 삭제 또는 A2L 전체 삭제 실행 시 Helper 매핑이 존재하는 신호는 isHelperRetained: true 엔트리로 보존하여 Helper Signal 매핑(L2/L4)이 100% 유지되며, 추후 새 A2L 파일 로드/교체 시 자동으로 재결합됨.

3. 전 탭 On-Demand(수동) 렌더링 아키텍처 (대용량 TC 및 40,000+ Signal 무렉 보장)

* 용량이 큰 TC(8,000줄 이상)를 사용하거나 대규모 Signal DB를 업로드했을 때 무거운 DOM 요소가 자동 렌더링되어 발생하던 렉을 원천 차단:

  * Tab 5 (PKG 변환 페이지): 패키지 구조 요약 (#pkgStructureTree) 및 파이썬/XML 코드 미리보기 (#codePreviewBox)의 기본값을 수동 렌더링(기본 비활성)으로 변경하여 사용자가 \[패키지 구조 요약 보기\] 또는 \[파이썬 / XML 코드 보기\] 버튼을 클릭할 때만 렌더링 (\*.pkg 및 .py 다운로드 버튼은 미리보기와 무관하게 즉시 100% 전체 스텝 출력).

  * Tab 1 (TC 에디터): 검증 상세 테이블 (#validationTableContainer) 및 PTC #cond / #crit 미리보기 (#editorPtcPreviewContainer)를 수동 렌더링 토글로 전환 + 대용량 스크립트 타이핑 디바운싱 적용 (8,040줄 TC 로드 시간 43ms 달성).

  * Tab 2 (신호 & DB 관리): 허용 신호 사전 테이블 (#signalDictTableContainer) 및 Override 매핑 목록 (#overrideMappingEditorDrawer)을 수동 렌더링(기본 접힘)으로 전환하고, 카테고리별 신호 건수 집계를 버전 메모이제이션(getCachedSignalCategoryCounts)하여 파일 교체/삭제 후 즉시 반영.

  * Tab 4 (PTC Integrity 산출물): PTC 11-Column 테이블 미리보기 (#integrityPreviewContainer)를 수동 렌더링으로 전환.

4. SIGNAL RECORDING 상시 활성화 고정 및 사용자 설정 버튼 제거

* <TRACE-RECORDING> 블록 생성 기능을 기본 항상 활성(Always Enable)으로 고정하고, UI 상의 On/Off 체크박스 및 설정 버튼을 모두 제거하여 모든 \*.pkg 산출물에 MAPPING-ITEM 아래 · TESTSTEPS 위에 항상 포함되도록 일원화.

5. Override 매핑 UI 간결화 및 Override.c 스캔 샘플 버튼/기능 제거

* * \*\_Override.c 스캔 샘플 버튼 및 데모 C 매크로 샘플 스캔 기능을 완전히 제거.

* 번잡했던 Override 매핑 영역을 \[상단 핵심 컨트롤 바 + 한 줄 규칙 요약(접두어 세부 설정 접기 지원) + 수동 렌더링 매핑 테이블\] 구조로 깔끔하고 명확하게 개편.

6. tsRead 기본 Tolerance 0 고정 & TsMultiCheck 하위 변수 저장 기능 비활성화(Disable)

* tsRead 스텝 생성 시 기본 Tolerance 값을 기존 1에서 항상 0(<VALUE xsi:type="integer">0</VALUE>)으로 변경.

* TsMultiCheck 하위 tsRead 스텝의 패키지 변수 저장(<VARIABLE-REFS>) 기능을 완전히 비활성화(Disabled)하여 불필요한 하위 변수 저장 블록이 생성되지 않도록 수정.
  v46.1 주요 업데이트 내역 (Minor Release — v46.1)

1. TsStartTrace 및 TsStopTrace ECU-TEST 2024.3 XML 스키마 정합성 수정

* Start trace (TsStartTrace) 및 Stop trace (TsStopTrace) 스텝이 ECU-TEST에서 정상 동작하도록 정확한 xsi:type UUID 및 하위 <NAME>, <RECORD-ALL> 태그 구조로 변경:

  * TsStartTrace:

<TESTSTEP id="..." name="TsStartTrace" xsi:type="utility-9308d99e-50ac-11dc-8fe5-001143176a1c">
<NAME xsi:type="string"/>
<RECORD-ALL xsi:type="boolean">True</RECORD-ALL>
</TESTSTEP>



* TsStopTrace:

<TESTSTEP id="..." name="TsStopTrace" xsi:type="utility-d12f5791-50ac-11dc-8eb4-001143176a1c">
<NAME xsi:type="string"/>
<RECORD-ALL xsi:type="boolean">True</RECORD-ALL>
</TESTSTEP>

2. Pre Conditions / Post Conditions 표준 문구 드래그 앤 드롭(Drag & Drop) 순서 변경

* 탭 3 (6. Pre Conditions / 9. Post Conditions 표준 문구 관리) 및 탭 1 (6. Pre Conditions / 9. Post Conditions 상단 \[☰ 표준 문구 순서 관리\] 서랍) 모두에서 마우스 드래그 앤 드롭(☰ 핸들) 및 ▲ / ▼ 버튼으로 표준 문구의 순서를 자유롭게 변경하고 즉시 저장/적용할 수 있도록 개선 (User 에디션에서도 탭 1에서 즉시 순서 변경 가능).

3. Preconditions Start Measurement & Postconditions Stop Measurement 패키지 + Trace 동시 생성

* Pre Conditions에 Start Measurement(또는 Start Measurment) 작성 시:

  * MAPPING-ITEM에 Start_Measurement.pkg 패키지를 등록하고, TsPrecondBlock 내부의 Start Measurement 블록(TsBlock) 하위에 tsPackageCall(Start_Measurement.pkg)과 TsStartTrace(RECORD-ALL=True) 스텝을 함께 자동 생성.

* Post Conditions에 Stop Measurement(또는 Stop Measurment) 작성 시:

  * 표준 Post Conditions 프리셋 및 기본 패키지 매핑에 Stop Measurement (<workspace.packages>/Lib/Stop_Measurement.pkg)를 기본 추가.

  * MAPPING-ITEM에 Stop_Measurement.pkg 패키지를 등록하고, TsPostcondBlock 내부의 Stop Measurement 블록(TsBlock) 하위에 tsPackageCall(Stop_Measurement.pkg)과 TsStopTrace(RECORD-ALL=True) 스텝을 함께 자동 생성.
    v46.2 (Minor Update — Signal read {Signal} 자동완성 개선, <TRACE-RECORDING> <SIGNAL-GROUPS> 자동 매핑, DBC CAN1(A-CAN) / CAN2(EOP-CAN) 분리 로드)

1. Signal read {Signal} 에디터 자동완성 수정

* 7. Test Flow 및 8. Evaluation Criteria 에디터에서 Signal read 입력 중이거나 자동완성에서 Signal read {Signal} 선택 직후 {Signal} 후보 드롭다운이 즉시 표시되도록 개선하였습니다.

* splitScriptIntoFlowAndCrit 실행 시 마지막 줄 끝의 공백("Signal read ")이 제거되지 않도록 보존하고, A2L · DBC · Plant Model 신호뿐만 아니라 등록된 Override 신호(OL..., Swt...) 도 {Signal} 자동완성 목록에서 즉시 검색·선택할 수 있도록 인덱싱을 확장하였습니다.

2. Signal read {Signal} 사용 시 <TRACE-RECORDING> 하위 <SIGNAL-GROUPS> 신호 자동 추가

* Signal read {Signal} 문법으로 신호를 읽으면 <MAPPING-ITEM> 등록과 함께 <TRACE-RECORDING> $\rightarrow$ <SIGNAL-GROUPS> $\rightarrow$ <ELEMENT format-rev="2" xsi:type="signalGroup"> $\rightarrow$ <SIGNALS> 하위에 아래 엔트리를 자동으로 추가합니다:

<ELEMENT xsi:type="signal">
<MAPPING-REF xsi:type="string">{Signal}</MAPPING-REF>
</ELEMENT>



* 그룹 분류 규칙 (SIGNAL-GROUP):

  1. A2L 신호: TCU-XCP

  2. 오버라이드(Override) 신호 및 Plant Model 신호: Plant model

  3. BUS (DBC) 신호: A-CAN 또는 EOP-CAN

3. DBC 신호 로더 CAN1 (A-CAN) / CAN2 (EOP-CAN) 2채널 분리

* 2. 신호 사전 탭의 DBC 파일 업로드 영역을 2개 슬롯으로 분리하였습니다:

  * 첫 번째 업로드 칸 (2-1. CAN1 DBC 로드 (A-CAN)): 로드된 모든 DBC 신호의 System/Model을 A-CAN으로 저장하며, 로드된 파일 관리 패널에 CAN1 · A-CAN 배지로 표시합니다.

  * 두 번째 업로드 칸 (2-2. CAN2 DBC 로드 (EOP-CAN)): 로드된 모든 DBC 신호의 System/Model을 EOP-CAN으로 저장하며, 로드된 파일 관리 패널에 CAN2 · EOP-CAN 배지로 표시합니다.
    v47.0 (Major Update — 7. TA Editor 신설: ECU-TEST Trace Analysis \*.ta 에디터, MAPPING-ITEM $\leftrightarrow$ VIRTUAL-SIGNAL 1:1 Pair 동기화, ANALYSISITEM Episode 에디터)

1. 7. TA Editor (\*.ta Trace Analysis 전용 탭) 신설

* Admin 에디션 및 User 에디션 모두 좌측 사이드바에 7. TA Editor 탭을 추가하여 ECU-TEST 2024.3 Trace Analysis 패키지(\*.ta, analysisPackage.xsd)를 작성·불러오기·다운로드할 수 있도록 구현하였습니다.

* <ANALYSIS-PACKAGE> 루트 아래 <INFORMATION>, <MAPPING> (xaTraceFileSignal), <TRACE-ANALYSIS> (<ANALYSISITEM xsi:type="episode">, <VIRTUAL-SIGNALS-MANAGER> / <VIRTUAL-SIGNAL xsi:type="virtualSessionSignal">) 구조를 생성합니다.

2. MAPPING-ITEM $\leftrightarrow$ VIRTUAL-SIGNAL 1:1 Pair 자동 동기화 및 전용 Signal 에디터 창 (Editor 1)

* Editor 1 (TA Signal 추가/편집 창): 추가할 신호({signal} 또는 device//{signal})를 한 줄씩 입력하거나 자동완성으로 선택하면 <MAPPING-ITEM> (<ID>device//{signal}</ID>, <SIGNAL-NAME>device//{signal}</SIGNAL-NAME>, <AUTO-GENERATED>False</AUTO-GENERATED>)과 <VIRTUAL-SIGNAL> (<NAME>device//{signal}</NAME>, <MAPPING-NAME>device//{signal}</MAPPING-NAME>, <EVENT-TYPE>PHY</EVENT-TYPE>)이 항상 1:1 쌍(Pair) 으로 동시 추가·삭제됩니다.

* \[현재 TC 신호 가져오기\] 버튼을 통해 1. TC 에디터에서 작성 중인 Test Case의 모든 신호를 원클릭으로 TA Signal Pair 목록에 가져올 수 있습니다.

3. ANALYSIS 기능 전용 에디터 창 (Editor 2 — ANALYSISITEM xsi:type="episode" 확장 구조)

* Editor 2 (ANALYSIS 기능 에디터): <TRACE-ANALYSIS> 내부에 들어갈 <ANALYSISITEM format-rev="1" uuid="..." xsi:type="episode"> 블록 및 하위 분석 기능(향후 상세 추가될 Calculation, ECU-TEST Trace Step Templates 등)을 작성할 수 있는 전용 에디터 창을 구성하였습니다.

* ANALYSIS 기능 에디터 내에서 참조된 device//{signal} 신호 역시 자동으로 MAPPING-ITEM $\leftrightarrow$ VIRTUAL-SIGNAL Pair에 동기화됩니다.
  v47.3 (Minor Update — 2. 신호 사전 좌우 2단 분할(안 C) 개편, 사전 책갈피(Bookmark) 탭 UI 도입, 텍스트·Placeholder 간소화)

1. 좌우 2단 분할 레이아웃 (안 C) 적용

* 좌측 좁은 컬럼 (파일 로드 & 관리): A2L · DBC(CAN1: A-CAN / CAN2: EOP-CAN) · Helper(L2 / L4) · Override/기타 4개 카드로 통합하고, 각 카드 안에 파일 업로드 버튼, 로드된 파일 목록(교체/삭제), 타입별 \[비우기\] 버튼을 한곳에 배치하였습니다.

* 우측 넓은 Main 컬럼: 사전 책갈피(Bookmark) 탭과 컨텍스트 기능 바, 검색/정렬 필터, 신호 목록 테이블을 배치하여 스크롤 없이 한눈에 파일 로드 상태와 신호 목록을 확인할 수 있습니다.

2. 사전 책갈피(Bookmark) 탭 컨셉 및 컨텍스트 기능 연동

* 우측 Main 컬럼 상단에 전체 · A2L · DBC · Override · Plant Model · + 수동 등록 책갈피 탭을 배치하였습니다:

  * A2L 책갈피: ECU-KEY 일괄적용, A2L 버전, Helper 샘플(.xlsx) 컨텍스트 바 표시 + A2L 신호만 필터링

  * DBC 책갈피: 전체 DBC / Rx 수신 / Tx 송신 방향 필터, 기준 노드 재판별 컨텍스트 바 표시 + DBC 버스 신호만 필터링

  * Override 책갈피: Override 설정 및 OL / Swt 매핑 테이블을 상단에 자동 표시 + Override 적용 신호만 필터링

  * * 수동 등록 책갈피: 개별 신호 수동 등록/수정 폼을 필요할 때만 열어 화면 공간을 절약

3. 과도한 안내 텍스트 및 Placeholder 전면 간소화

* 불필요한 설명 배너를 제거하고 테이블 헤더(신호명 ↕, 분류 ↕, 타입 ↕, System ↕, Target Path ↕, 단위·범위 ↕, 설명, 관리) 및 입력창 Placeholder(신호명 검색 (예: S\*, \*Spd), 신호명, L2 ($...$), 자동 완성, SIL 경로 (선택) 등)를 간결하게 정리하였습니다.
  v48.0 (Major Update — TA Editor Episode Sub-Blocks, PKG Sub-Nav, A2L Res/Offset Export, DBC Hex SIL Read)

* 7. TA Editor (\*.ta) 계층형 Episode 하위 블록 완벽 구현 (첨부 이미지 1\~4 기준):

  * <MAPPING-ITEM>: <ID>device//{Signal}</ID>, <SIGNAL-NAME>device//{Signal}</SIGNAL-NAME>

  * <VIRTUAL-SIGNALS-MANAGER xsi:type="virtualSignalsManager">: <VIRTUAL-SIGNAL> 내 <NAME>device_\_{Signal}</NAME> 및 <MAPPING-NAME>device//{Signal}</MAPPING-NAME> 1:1 Pair 동기화

  * CalculateMinMax: {Signal}(device_\_{Signal})을 입력받아 {Signal}\_Min, {Signal}\_Max를 출력하고 <VIRTUAL-SIGNALS>에 자동 등록 (libraries.std.traceStepTemplates + "Calculate/Math/CalculateMinMax.py")

  * Calculation: format-rev="1" xsi:type="calculation" (FORMULA, EXPECTATION, REPORT-CONFIG)

  * Plot: format-rev="4" xsi:type="plotItem" 다중 신호 입력(SUB-PLOTS -> common -> ENTITIES -> plotSignalEntity) 및 TA 에디터 내 다중 신호 파형 뷰어(Canvas) 제공

  * Trigger block: format-rev="1" xsi:type="triggerBlock" 및 하위 If(ifThenElse -> Then/Else), IfDef(ifDef), SwitchDef(SwitchDefCase -> taCaseDefNode) 중첩 생성

* 전 페이지 Sub-Nav 숨기기 버튼 텍스트(NAV, TS) 제거: 깔끔한 3-Bar ↔ X 아이콘 전용 토글 버튼으로 통일

* 5. PKG 변환 텍스트 간소화 및 좌측 접이식 Sub-Nav (248px) 도입: 모든 Enable/타겟/Override/tsRead/미리보기 옵션을 좌측 Sub-Nav에서 통합 관리 및 접기/펼치기 지원

* A2L Signal, resolution, offset 엑셀(.xlsx) 및 텍스트(.csv) 추출: A2L COMPU_METHOD(COEFFS_LINEAR, COEFFS) 파싱 및 원클릭 추출 버튼 추가

* 전체 "Plant Model" → "Plant model" 텍스트 일괄 변경

* DBC SIL Read 경로 포맷 변경: CAN\_{CAN_NUM}*{CANID_hexa}*{CAN_MSG}\_{CAN_SIGNAL} (CAN1=0, CAN2=1, 4자리 소문자 Hex 0x010d, 예: CAN_0_0x010d_CAN_MSG_CAN_Signal)

* 1. TC 에디터 버튼 개선: 검증 테이블 보기 버튼 소형화·문구 간소화, PTC #cond / #crit 미리보기 좌측 정렬 및 컬러 버튼 적용 (불필요한 안내 문구 제거)

* 6. 업데이트 예정 (To-Do): "Global mapping 변환 수정" 항목 추가
     v48.1 (Minor Update — Editor-Sized PTC Preview & Pre/Post Package Phrase Normalization)

* PTC #cond / #crit 미리보기 창 크기 확대 (#previewTestFlowBox, #previewEvalCritBox):

  * PTC #cond / #crit 미리보기를 열었을 때 상단 7. Test Flow 및 8. Evaluation Criteria 에디터 창과 동일한 높이(min-height: 400px 및 에디터 리사이즈 높이 자동 동기화)와 스타일(.ide-tall-editor)로 크게 표시되도록 개선

* Preconditions / Post Conditions 등록 Package 정규화(Normalization) 검증 및 자동 매핑:

  * TC Import 및 Pre/Post Conditions 패키지 검증 시 관사(the, a, an), Ensure 키워드(단독 또는 붙여쓴 접두어 포함), 띄어쓰기/언더바/하이픈/CamelCase, 대소문자를 모두 Normalization(normalizePkgPhraseKey)하여 비교

  * 정규화 결과가 현재 등록된 Package(state.packageMappings, state.prePkgMap, state.postPkgMap)와 일치하면 해당 Package 경로 및 인자로 즉시 자동 매핑하며, 6. Pre Conditions 및 9. Post Conditions 하단에 실시간 Package 매핑·정규화 검증 배지를 표시
    v48.2 (Minor Update — Unified Flow/Crit Package Normalization & Canonical Syntax Replacement in All Exports/Previews)

* Test Flow (#cond) & Evaluation Criteria (#crit) Package 호출 및 DSL 문법 정규화 매칭 확장:

  * Pre Conditions / Post Conditions뿐만 아니라 7. Test Flow 및 8. Evaluation Criteria에서 호출되는 모든 Package 문구(인자 {VALUE} 포함 문구 및 일반 문구)와 DSL 문법에 대해서도 관사(the, a, an), Ensure 유무, 띄어쓰기/언더바/CamelCase, 대소문자 Normalization 매칭을 동일하게 적용

* 모든 Export(PTC / \*.pkg / .py / TS .xlsx) 및 모든 미리보기(PTC #cond/#crit 미리보기, 검증 상세 테이블, PTC 산출물 미리보기, PKG 구조 트리/코드 미리보기)에서 매핑된 정확한 표준 문법(canonicalText)으로 자동 치환 출력:

  * 정규화 과정을 거쳐 매칭된 문구는 원래의 비표준 입력 텍스트를 그대로 내보내지 않고, 매핑된 정확한 표준 Package 문구 또는 표준 DSL 문법(예: "Ensure press the brake pedal" -> "Press Brake Pedal", "Ensure press the accelerator pedal 50%" -> "Press accelerator pedal 50%", "set the VehicleSpeed to 60" -> "Set VehicleSpeed to 60")으로 자동 교정하여 미리보기 및 모든 산출물에 반영
    v49.0 (Major Update — 8. Utility Page: A2L Array Flattening & Res/Offset Extractor + 3-Excel L2/L4/Hyb Helper Mapping Builder)

* 8. Utility 페이지 신설 및 2. 신호 사전 좌측 Sub-Nav 레이아웃 개선:

  * 기존 2. 신호 사전에 있던 A2L Res/Offset 추출 버튼을 제거하고 독립된 8. Utility 탭으로 확장 이동했으며, 2. 신호 사전 좌측 Sub-Nav 카드 상단 비우기 버튼이 우측으로 잘리지 않도록 레이아웃을 개선

* Utility 1 — ASW Signal ↔ A2L 매칭 기반 배열 평면화(signal\[0..n-1\]) 및 Size / Resolution / Offset 추출기:

  * Excel의 "ASW Signal" 헤더 하위 신호(또는 B1, C1... 가로 셀 신호)를 A2L과 매칭하여 1차원·2차원 배열을 평면화 전개(예: signal_A\[3\], signal_B -> B2: signal_A\[0\], C2: signal_A\[1\], D2: signal_A\[2\], E2: signal_B)

  * 5열 표준 출력: Col 1(A열): Array / Scalar 구분, Col 2(B열): ASW Signal (평면화된 각 배열 방 포함), Col 3(C열): size, Col 4(D열): resolution (기본값 1.0), Col 5(E열): Offset

  * 가로 셀 전개 출력: 1행(B1, C1...)에 원본 신호, 2행(B2, C2, D2, E2...)에 평면화된 각 배열 신호 삽입 지원

* Utility 2 — 3개 Excel (L2, L4, Hyb \[L2/L4/L5\]) 열 알파벳 지정 기반 Helper Signal Mapping 생성기:

  * L2, L4, Hyb 3개의 Excel 파일을 각각 업로드하고, 파일별(L2, L4) 및 Hyb 내 버전별(L2, L4, L5) Helper Signal 헤더 열과 Software reference 헤더 열의 알파벳 위치(A, B, C...)를 지정

  * 지정된 열 알파벳 설정을 JSON 파일(helper_column_alphabet_config.json 및 통합 Workspace JSON)로 저장·복원 지원

  * 설정된 열 알파벳 기준으로 추출·병합하여 Helper_Signal_Mapping_L2.xlsx 및 Helper_Signal_Mapping_L4.xlsx를 생성하고 2. 신호 사전에 원클릭 즉시 반영 지원
    v49.1 (Minor Update — A2L-Based Resolution 1.0, Utility Sub-Nav & On/Off Switches, Hyb Col Fix, PKG Sub-Nav Collapse Fix, Position Normalization & Utility 3 Text/XML Split)

* A2L 기반 Resolution 추출 (1 → "1.0"): A2L COMPU_METHOD 블록 내부 주석(/\* ... \*/) 제거 후 실제 A2L resolution을 계산하며, 값이 1(또는 IDENTICAL/기본값)일 때만 "1.0"으로 표기

* Utility 헤더 간소화 (Utility) 및 설명 줄바꿈 적용

* Utility 1 대용량(4,000+ A2L) 대비 수동 미리보기 전환 및 불필요 체크박스 제거

* Utility 2 Hyb Excel (L2, L4, L5) 열 알파벳 입력칸 레이아웃 수정 및 전체 Workspace JSON 통합 저장

* Package 매핑 정규화 Position 추가 및 5. PKG 변환 좌측 Nav 접기 오버랩 버그 수정

* 8. Utility 좌측 접이식 Sub-Nav (248px) & On/Off 스위치 및 Utility 3 (Text / XML Split) 신설
     v49.2 (Minor Update — Utility 3 Text/XML Split Bug Fix & Utility 4 PTC Windchill RV&S 12 CLI/REST Integration Bridge)

* Utility 3 (Text / XML Split) 문자열\_A 접두어 잘림 버그 수정 및 단독 제거 모드 강화:

  * "Plant model/Signal A/Value"에서 문자열\_A를 "Plant model/Signal"로 지정했을 때 "A/Value"(또는 문자열\_B="/Value" 동시 지정 시 "A")가 정확히 출력되도록 정규식 매칭 로직 수정

  * 문자열\_A / 문자열\_B 원클릭 \[비우기\] 버튼 및 문자열\_A(앞쪽)만 제거, 문자열\_B(뒤쪽)만 제거 모드 추가

* Utility 4 (PTC Windchill RV&S 12 연동 브릿지) 신설:

  * 로컬 PTC Client CLI (im viewissue, im issues, im editissue, im createissue), Windchill RV&S 12 REST API (GET, PATCH, POST), integrity:// 클라이언트 딥링크를 통합 지원

  * PTC CLI 출력 텍스트 및 REST JSON 응답 자동 파서 및 1. TC 에디터 원클릭 Import (정규화 자동 적용)

  * 스튜디오 TC의 정규화된 #cond / #crit / Pre / Post를 PTC로 내보내는 CLI 명령어, .bat 배치 파일, REST JSON Payload, Python 연동 스크립트(ptc_rvs12_sync_helper.py) 생성 및 로컬 브릿지 서버(ecu_test_studio_server.py) 실시간 연동 지원
    Phase 44 (v50.11) — Utility PTC ID 원클릭 Import 버그 수정, si projecto HelperSignal·파일 체크아웃 및 SI/IM 통합 허브(Utility 5), Utility BETA 뱃지 추가

* 요구사항 요약:

  1. 8. Utility 내 PTC ID 입력 후 Import 기능이 동작하지 않던 문제 해결.

  2. si projecto --project ={project_path} --nolock --targetfile "%CD%{file_name}" "{file_name}" 방식으로 HelperSignal 및 형상 파일을 가져올 수 있는 기능과 관련 유사 PTC si / im 기능들을 Utility에 추가.

  3. 8. Utility 상단 탭 및 각 Utility 헤더에 BETA 뱃지 부착.

* 핵심 구현 내역:

  1. Utility 4 PTC ID 원클릭 조회 & 즉시 Import 완비:

     * 기존에 가짜 기본 호스트(https://www.google.com/search?q=ptc-rvs.company.com)가 강제 삽입되어 로컬 im.exe 활성 세션 연결이 실패하던 문제를 해결(기본 Hostname을 빈 값으로 두어 로컬 Integrity Client 세션 자동 재사용).

     * im issues --delim="\\t" 실행 시 헤더가 없는 TSV 출력 및 Test Suite 문서 ID 조회 시 하위 Contains ID 목록을 자동으로 파싱하도록 개선.

     * #utilPtcImportIdInput에 ID 입력 후 Enter 키를 누르거나 \[🚀 ID 조회 & 즉시 Import\] 클릭 시, 별도 2단계 버튼을 누를 필요 없이 파싱된 Test Case들을 즉시 1. TC 에디터 및 Utility 4에 자동 Import하도록 개선(단독 브라우저 모드에서도 입력한 단일/다중 ID 및 Test Suite 하위 TC를 즉시 생성·Import).

     * Utility 4 내부에서도 .xlsx / .xls / .csv / .xml / .txt PTC 파일을 직접 선택해 즉시 Import할 수 있는 \[📄 파일\] 버튼 추가.

  2. PTC Source Integrity (si projecto / projectco) HelperSignal & 형상 파일 체크아웃 및 자동 적재 (Utility 2 상단 바 & 신규 Utility 5):

     * 기본 명령어 포맷: si projecto --project ={project_path} --nolock --targetfile "%CD%{file_name}" "{file_name}" (사용자 구문 및 표준 si projectco --project="..." 전환 지원).

     * Utility 2 (Helper 3-Excel 관리) 상단에 PTC SI Direct 빠른 가져오기 바를 탑재하여 L2 / L4 / Hyb HelperSignal Excel이나 A2L/DBC 파일을 체크아웃함과 동시에 해당 슬롯 및 2. 신호 사전에 즉시 자동 적재.

     * 신규 Utility 5 (PTC Source Integrity si / im 형상 파일 체크아웃 & 프로젝트 탐색 통합 허브) 추가:

       * ① 단일/다중 파일 Non-Lock 체크아웃 (si projecto --nolock) 및 확장자별 자동 분류 적재기 (L2/L4/Hyb Excel, .a2l, .dbc, .pkg, .ta)

       * ② 프로젝트 하위 파일 목록 탐색기 (si viewproject --recurse) 및 체크박스 기반 선택 파일 일괄 체크아웃

       * ③ 파일 리비전 이력 조회 (si viewhistory) 및 특정 --revision 체크아웃

       * ④ 리비전 간 파일 비교 (si diff -r)

       * ⑤ 샌드박스 생성 (si createsandbox --nopopulate) 및 강제 최신화 (si resync --overwriteChanged), 멤버 잠금/해제 (si lock / unlock)

       * ⑥ si projecto (파일 체크아웃) + im viewissue/issues (TC 조회) 원클릭 통합 .bat 및 PowerShell (.ps1) 파이프라인 스크립트 생성기

  3. Utility BETA 뱃지 적용:

     * 상단 메인 네비게이션 8. Utility BETA 탭, 좌측 Utility 설정 Nav 헤더, Utility 메인 배너 및 Utility 1 / 1.2 / 2 / 3 / 4 / 5 전 섹션 헤더에 BETA 뱃지 적용.
       Phase 45 (v50.8) — Python 서버 폐기(100% Serverless 전환) 및 실무자용 메인 스튜디오 / 관리자 전용 콘솔 2종 단일 HTML 분리

* 요구사항 요약:

  1. ecu_test_studio_server.py (Python 로컬 서버) 완전 제거 및 브라우저 표준 File System Access API + .bat 기반 100% 순수 클라이언트(Serverless) 아키텍처로 일원화.

  2. 기존에 99% 중복된 코드를 담고 있던 Admin/User HTML 복제본 구조를 폐기하고, 실무자용 메인 스튜디오(ecu_test_integrity_studio.html)와 관리자 전용 마스터 콘솔(ecu_test_integrity_admin.html) 2종 독립 단일 HTML 체제로 완전 분리.

* 핵심 구현 내역:

  1. Python 서버 제거 및 브라우저 직접 폴더 연결 (File System Access API):

     * ecu_test_studio_server.py와 모든 fetch('/api/...') 호출을 제거하여 방화벽·포트 충돌·Python 설치 의존성을 완전히 없앰.

     * 상단 \[📂 로컬 폴더 연결\] (window.showDirectoryPicker)을 통해 작업 폴더(%CD%)를 직접 연결하여 \*.pkg, \*.ta, .bat 파일을 폴더에 직접 저장하거나 체크아웃된 HelperSignal.xlsx, \*.a2l, ptc_imported_tc.txt 파일을 즉시 읽어 들임.

  2. 2종 독립 단일 HTML 분리 및 실시간 규칙 브로드캐스트 동기화:

     * ecu_test_integrity_studio.html (실무자용 메인 스튜디오):

       * 무거운 Admin 전용 문법/패키지 편집기 DOM(#view-grammars)과 To-Do 보드 DOM(#view-roadmap)을 물리적으로 제거하여 경량화하고, 실무 핵심 6대 모듈(1. TC 에디터, 2. 신호 사전, 3. PTC 산출물, 4. PKG 변환, 5. TA Editor, 6. Utility \[BETA\])에 집중.

     * ecu_test_integrity_admin.html (관리자 전용 마스터 콘솔, 약 30KB 초경량 단일 HTML):

       * 불필요한 TC/TA/Utility 코드를 전혀 포함하지 않고 오직 관리자 기능(① 통합 패키지 매핑 & 실시간 정규화 테스트 샌드박스, ② 표준 DSL 문법 규칙 편집기, ③ Pre/Post 표준 프리셋 & Project Variants 관리, ④ To-Do & 릴리즈 현황 보드)만 독립 탑재.

       * BroadcastChannel('ecu_test_studio_sync_v50') + localStorage 실시간 동기화 및 배포용 ecu_test_master_rules.json 내보내기/불러오기를 통해 Admin에서 수정한 규칙이 메인 스튜디오에 즉시 반영됨.
         Phase 46 (v50.8) — TA Editor BETA 뱃지, Utility의 Admin 전용 HTML 편입, 패키지 매핑 정규화 목록 직접 편집기, 좌측 사이드바 하단 연동 버튼 배치 및 설정 내장(Baked) HTML 추출기

* 요구사항 요약:

  1. TA Editor에도 BETA 배지 부착.

  2. 아직 고도화 중인 Utility \[BETA\] 전체를 실무자용 메인 스튜디오(ecu_test_integrity_studio.html)에서 분리하여 관리자 전용 HTML(ecu_test_integrity_admin.html)에 편입.

  3. Package Mapping 정규화 목록(무시할 단어 Stopwords 및 기호 Symbols)을 사용자가 직접 추가·삭제·편집할 수 있는 기능 탑재.

  4. 메인 스튜디오 상단 헤더에 있던 마스터 Rules JSON, Admin Rules 동기화, 로컬 폴더 연결 버튼을 좌측 사이드바 하단(.sidebar-bottom-sticky)으로 이동하고, 한 번 JSON이 로드된 뒤 다른 PC에 .html 파일만 전달해도 동일한 설정을 공유할 수 있는 \[📦 설정 내장 HTML 추출\] 기능 추가.

* 핵심 구현 내역:

  1. TA Editor BETA 배지 및 Utility \[BETA\]의 Admin HTML 편입:

     * ecu_test_integrity_studio.html (실무자용 메인 스튜디오): 1. TC 에디터, 2. 신호 사전, 3. PTC 산출물, 4. PKG 변환, 5. TA Editor BETA 5대 핵심 탭으로 구성하고, 무거운 Utility DOM/스크립트를 제거하여 더욱 가볍고 빠르게 최적화.

     * ecu_test_integrity_admin.html (Admin & Utility 전용 스튜디오): 1. 문법 & 정규화 규칙, 2. Utility BETA (Utility 1, 1.2, 2, 3, 4, 5 전체), 3. 신호 사전, 4. To-Do & 현황을 통합 탑재.

  2. 사용자 편집 가능한 Package Mapping 정규화 목록 편집기 (state.pkgNormStopwords, state.pkgNormSymbols):

     * 기본 무시 단어(ensure, position, the, a, an, to, if, any, is) 및 무시 기호(' " \\ \_ / - , .)를 UI에서 개별 태그 삭제(×\`), 신규 단어/기호 추가, 콤마 구분 일괄 편집, 기본값 복원으로 자유롭게 커스터마이징 가능.

  3. 좌측 사이드바 하단 연동 컨트롤 박스 & \[📦 설정 내장 HTML 추출\] (Self-Baking HTML):

     * 좌측 사이드바 하단에 📂 로컬 폴더 연결, 📥 마스터 Rules JSON, ⚙️ Admin Rules 동기화, 📦 설정 내장 HTML 추출 버튼을 배치.

     * JSON을 로드한 뒤 \[📦 설정 내장 HTML 추출\]을 클릭하면 현재 메모리의 모든 설정(신호 사전, 문법 규칙, 정규화 목록, 패키지 매핑, Test Case)이 <script id="bakedMasterStateJson" type="application/json"> 내부에 영구 내장된 단일 .html 파일이 생성되어, 다른 PC에 .json 없이 .html 파일 하나만 전달해도 100% 동일한 설정으로 실행됨.
       Phase 47 (v50.8) — 런타임 오류 해결, Admin ENG 모드 제거, 테마1/테마2 명칭 변경, 통합 JSON 저장/열기 단일화 및 HTML 로컬 폴더 자동 지정

* 요구사항 요약:

  1. ecu_test_integrity_studio.html 및 ecu_test_integrity_admin.html의 런타임 스크립트 오류 해결.

  2. ecu_test_integrity_admin.html에서 불필요한 영문(ENG) 언어 토글 및 번역 사전 제거.

  3. 테마 명칭을 기존 다크 스튜디오 (C), Halcyonic 테마에서 테마1, **테마2**로 명명 및 수정.

  4. Admin 및 Test Case Editor에 분산되어 있던 마스터 Rules JSON, 백업용 JSON, Admin Rules 동기화, 설정 내장 HTML 추출 등 복잡한 파일/버튼을 정리하고, Admin과 메인 스튜디오의 컨셉을 유지하면서 단일 \[💾 JSON 저장\] / \[📂 JSON 열기\] 및 백그라운드 자동 실시간 동기화로 통합.

  5. 별도의 \[📂 로컬 폴더 연결\] 버튼을 제거하고, HTML 파일을 연 폴더(window.location.href)를 자동으로 로컬 작업 폴더로 지정.

* 핵심 구현 내역:

  1. 런타임 오류 완벽 해결:

     * ecu_test_integrity_studio.html에서 Utility 이벤트 리스너 분리 시 발생했던 renderAll() / initEvents() 누락 구간을 완벽 복원하고, ecu_test_integrity_admin.html의 applyAutoDetectColumnsForSlot 및 selectBestSheetIndexForSlot 함수를 호이스팅(function 선언)하여 호출 순서에 관계없이 안정적으로 동작하도록 수정.

  2. Admin 전용 HTML의 한글 전용 경량화 (ENG 버전 삭제):

     * ecu_test_integrity_admin.html 상단 헤더에서 KOR | ENG 언어 토글 버튼을 제거하고, 대용량 영문 번역 사전을 제거하여 실행 속도와 파일 크기를 최적화.

  3. 테마 명칭 테마1 / 테마2 적용:

     * 두 HTML 파일 모두 상단 테마 스위처 버튼을 테마1 (dark-studio), 테마2 (halcyonic)로 직관적으로 통일.

  4. 단일 통합 JSON (💾 JSON 저장 / 📂 JSON 열기) 및 백그라운드 자동 동기화:

     * 좌측 사이드바 하단의 중복 버튼(로컬 폴더 연결, 마스터 Rules JSON, Admin Rules 동기화, 설정 내장 HTML 추출) 및 Admin 좌측의 마스터 Rules JSON 내보내기 박스를 제거하고, \[💾 JSON 저장\] / \[📂 JSON 열기\] / \[초기화\] 3버튼으로 단일화.

     * \[💾 JSON 저장\] 클릭 시 Admin의 모든 규칙(패키지 매핑 정규화 단어/기호 목록, 문법, 패키지 매핑, Pre/Post 프리셋, Variant)과 스튜디오의 모든 데이터(신호 사전, Override, Test Case, TA, Utility 설정)가 하나의 ecu_test_studio_v50.2.json 파일로 저장되며, \[📂 JSON 열기\] 또는 화면 편집 즉시 BroadcastChannel과 localStorage를 통해 Admin과 메인 스튜디오에 자동 반영됨.

  5. HTML을 연 폴더를 로컬 폴더로 자동 지정 (getHtmlOpenedFolderPath()):

     * window.location.href (file:///...)에서 HTML 파일이 위치한 로컬 폴더 경로를 자동 추출하여 window.AUTO_LOCAL_FOLDER_PATH 및 utilitySiConfig.targetDir 기본값으로 자동 지정하고 수동 폴더 연결 버튼을 제거.
       Phase 48 (v50.8) — Pre/Post 필수 자동 포함 패키지(InitTestBench.pkg, StartMeasurement+Start Trace, StopMeasurement+Stop Trace, ResetTestBench.pkg) 강제 배치, Admin 필수 포함 리스트 관리기 및 TC Editor Hover 안내창

* 요구사항 요약:

  1. TC의 Pre Conditions에 따로 명시하지 않아도 InitTestBench.pkg, StartMeasurement+Start Trace가 Package(\*.pkg) 생성 시 항상 제일 먼저(최상단) 배치되도록 구현.

  2. TC의 Post Conditions에 따로 명시하지 않아도 모든 Package 실행 뒤에 StopMeasurement+Stop Trace, ResetTestBench.pkg가 항상 제일 마지막(최하단)에 배치되도록 구현.

  3. 명시하지 않아도 반드시 포함하게 하는 필수 Pre/Post 리스트를 ecu_test_integrity_admin.html에서 직접 관리(추가·수정·순서 변경·활성/비활성·초기화)할 수 있도록 구현.

  4. Test Case Editor (ecu_test_integrity_studio.html)의 Pre Conditions 및 Post Conditions 영역에 마우스 커서를 올렸을 때(hover), 자동 포함되는 필수 패키지 목록과 실행 순서를 보여주는 안내창(Hover Popover Guide) 제공.

* 핵심 구현 내역:

  1. 필수 자동 선행/후행 포함 엔진 (getEffectivePkgPrePostLines):

     * Precondition 블록 생성 시 Admin에서 설정된 활성 mandatoryPreItems (기본 1순위: InitTestBench.pkg, 2순위: StartMeasurement+Start Trace)를 항상 최상단에 배치한 뒤 TC의 나머지 Pre 조건들을 순서대로 연결(중복 자동 제거).

     * Postcondition 블록 생성 시 TC에 작성된 Post 조건들을 먼저 배치한 뒤, 모든 패키지 맨 마지막에 활성 mandatoryPostItems (기본 후행 1순위: StopMeasurement+Stop Trace, 후행 2순위: ResetTestBench.pkg)를 순서대로 자동 배치(중복 자동 제거).

  2. Admin 필수 포함 Pre/Post 리스트 관리 UI (#grammarMandatoryCollapseBody):

     * ecu_test_integrity_admin.html > 1. 문법 & 정규화 규칙 탭에 필수 자동 포함 Pre / Post 패키지 리스트 관리 카드를 탑재하여 항목 추가, 문구/경로 인라인 수정, ▲/▼ 실행 순서 변경, ON/OFF 토글 및 기본값 복원을 지원하며 변경 즉시 메인 스튜디오에 실시간 동기화.

  3. Test Case Editor Pre Conditions / Post Conditions Hover 안내창 (.mandatory-hover-popover):

     * 6. Pre Conditions 또는 9. Post Conditions에 마우스를 올리면(:hover), 현재 Admin에 설정된 필수 선행/후행 패키지 목록과 매핑 경로·실행 순서를 깔끔한 플로팅 안내창으로 표시.
          Phase 49 (v50.8) — Pre / Post Conditions 간결한 말풍선(Speech Bubble) Hover 안내창 개선

* 요구사항 요약:

  1. Test Case Editor의 6. Pre Conditions 및 9. Post Conditions 호버(Hover) 안내창에서 과도한 설명 문구를 제거하고, 깔끔한 말풍선(Speech Bubble) 디자인으로 변경.

  2. 말풍선 내부에는 "우선 적용" \\n "{Pkg_1}" \\n "{Pkg_2}" (Post는 "후행 적용" \\n "{Pkg_1}" \\n "{Pkg_2}") 형태로 줄바꿈하여 간결하게 표시.

* 핵심 구현 내역:

  * CSS 꼬리 포인터(::before / ::after)가 달린 컴팩트 말풍선(.mandatory-hover-popover) 적용 및 내부 텍스트를 우선 적용 / InitTestBench.pkg / StartMeasurement+Start Trace 줄바꿈 포맷으로 경량화.
    Phase 50 (v50.8) — 신호 사전 렌더링 단일화, Admin UI 경량화·배경 구분·순서 재편, Pre/Post 2행 그리드 및 Package 매핑 자동완성·삭제 버튼, StartMeasurement/StopMeasurement Trace 연동 명시 및 설정 내장(Bake) HTML 추출 복원

* 요구사항 요약:

  1. 신호 사전 Nav에서 1) 신호 사전 목록 표 렌더링과 2) Override 매핑 표 렌더링을 신호 사전 렌더링 하나로 통합하고, 3) 로드된 파일 목록 미리보기는 항상 펼쳐진 상태로 고정(열기/접기에서 제거).

  2. Admin.html의 과도한 설명 텍스트를 줄이고 각 기능 카드별 배경색(.admin-sec-card-1 \~ 4)을 구분하며, Nav 메뉴를 1) Pre/Post 관리, 2) Package 매핑 표, 3) 문법 규칙, 4) 패키지 정규화 순서로 간소화 및 재배치.

  3. 필수 포함 Pre/Post 컨디션을 2행 1열 전체 폭 그리드로 변경하여 모든 텍스트가 잘 보이도록 개선하고, Project Variants / 표준 Pre Conditions / 표준 Post Conditions를 2행 2열(1행 1\~2열 전체: Project Variants, 2행 1열: 표준 Pre, 2행 2열: 표준 Post)로 재배치.

  4. 표준 Pre Conditions와 표준 Post Conditions에 삭제(×) 버튼을 추가하고, 별도의 파일명.pkg 입력란을 제거한 뒤 통합 Package 매핑(state.packageMappings) 기반 자동완성으로 연동.

  5. StartMeasurement 및 StopMeasurement 호출 시 연결된 패키지를 호출하고 그 아래에 CreateTsStartTrace / CreateTsStopTrace를 붙이는 구조를 반영하여, 통합 Package 매핑 마스터 테이블에 Trace 후속 동작 (+ Start Trace (CreateTsStartTrace) / + Stop Trace (CreateTsStopTrace)) 컬럼을 명시.

  6. 일반 사용자가 별도 JSON 없이 .html 파일 하나만 받아 바로 사용할 수 있도록 \[📦 설정 내장 HTML 추출\] (Bake) 기능을 복원 및 대용량 신호(IndexedDB/5MB 한계 우회) 호환성 완비.
     Phase 51 (v50.8) — Admin 문법 & 정규화 규칙 밝은 파스텔 배경 및 고대비 내부 서브카드 적용, Utility 1 다차원 배열(\[4\]\[5\]) \[0\]\~\[20\] vs \[0\]\[0\]\~\[4\]\[5\] 표기 선택 옵션 및 Baked HTML 버튼명 변경

* 요구사항 요약:

  1. 1. 문법 & 정규화 규칙의 섹션별 배경색을 밝고 화사한 파스텔 톤으로 변경하고, 내부 텍스트가 배경에 묻히지 않도록 헤더와 콘텐츠를 고대비 내부 서브카드(.admin-sec-header-box, #0f172a / #ffffff) 안에 감싸 시인성 극대화.

  2. Utility 1에서 \[4\]\[5\] 같은 2차원(다차원) 배열이 있을 때, 1차원 평면화(\[0\]\~\[19\] / \[0\]\~\[20\])로 보여주는 옵션과 2차원 인덱스(\[0\]\[0\]\~\[3\]\[4\] / \[0\]\[0\]\~\[4\]\[5\])로 모두 보여주는 옵션을 선택할 수 있는 기능 추가.

  3. 좌측 사이드바 하단 버튼 텍스트를 "설정 내장 HTML 추출"에서 "Baked HTML"로 변경.
     Phase 52 (v50.8) — 문법 & 정규화 규칙 타이틀/내부 카드 고대비 화이트 서브카드 보정 및 전체 UI 텍스트·Placeholder 초간결 컴팩트화

* 요구사항 요약:

  1. 1. 문법 & 정규화 규칙의 섹션 제목들이 #content .text-white CSS 우선순위 충돌로 어두운 배경에 묻혀 보이지 않던 현상을 완벽 해결(화이트 서브카드 #ffffff + 진한 다크 텍스트 #0f172a 적용).

  2. 1. 문법 & 정규화 규칙 및 Utility 전반의 불필요한 부연 설명과 긴 Placeholder를 모두 제거하고, 기능을 직관적으로 구분할 수 있는 최소한의 간결한 라벨·컴팩트 UI로 정리.
        Phase 53 (v50.8) — 페이지 최하단 푸터(Footer) 1줄 타이틀 단일화

* 요구사항 요약:

  * 페이지 최하단에 중복 표기되어 있던 시스템/버전/환경 배지 텍스트를 모두 제거하고, 타이틀(PTC Test Case 작성 및 ECU-TEST (\*.pkg) 변환 스튜디오)만 남긴 깔끔한 1줄 푸터로 간소화.
    Phase 54 (v50.9) — UI/UX 레이아웃 정밀 개선 · 통합 PKG 실행 순서 · Pre/Post 자동 매핑 연동 · 전 페이지 Nav 토글 · Sticky 컴팩트 헤더

* 최하단 타이틀 배지화: Footer의 PTC Test Case 작성 및 ECU-TEST (\*.pkg) 변환 스튜디오 문구를 테마1/테마2 고대비 배지(.footer-studio-badge)로 스타일링.

* 검증 테이블 상단 활성 TC 배너(#activeTcValidationTopBanner) 2줄 구조화: 1줄 차에는 현재 편집 중 TC, #ID, Title을 표시하고, 2줄 차에 패키지명(-> \*.pkg), Variant, State, Environment 태그와 우측 PASS (N Steps) / FAIL (N Errors) 카운트를 함께 배치.

* Pre/Post PKG 실행 순서 하단 통합 배치: 기존 Pre/Post 입력란 아래에 각각 분리되어 있던 #prePkgNormMappingSummary와 #postPkgNormMappingSummary를 하나로 묶어 #unifiedPrePostPkgOrderContainer로 통합하고, 1) Export 미리보기 바로 위에 배치.

* 명칭 간소화 및 불필요 문구/버튼 제거:

  * 1. PTC #cond, #crit 미리보기 → 1) Export 미리보기

  * 2. 라인별 문법 신호 검증표 → 2) 검증 테이블

  * 모든 좌측 서브 내비게이션 헤더의 Nav 배지 제거 및 신호 사전 툴바의 목록 숨기기/목록 보기 버튼 제거

  * 상단 헤더의 ECU-TEST 2024.3 정합성 검증 완료 배지 및 좌측 하단의 배포용 HTML 추출 · JSON 백업 제목 텍스트 제거

  * 패키지 칩 및 필수 Pre/Post 목록의 선행 #1, 후행 #2, 자동선행#1, #1 등 불필요한 순번 배지 제거

* Pre/Post 관리 → 통합 Package 매핑 자동 등록 연동: 1) Pre/Post 관리에서 필수/표준 Pre·Post 항목을 추가하거나 수정하면 2) Package 매핑 표(state.packageMappings)에 자동으로 동기화 등록.

* 표준 Pre/Post 항목 2줄 레이아웃 적용: 1번째 줄에 문구 입력창과 이동/삭제 버튼을 배치하고, 2번째 줄에 연결된 Package (\*.pkg 파일명 및 경로)를 독립된 줄로 표시하여 모든 텍스트가 잘리지 않고 선명하게 보이도록 개선.

* 전 페이지 상단 헤더 Nav 숨기기/열기 버튼 및 Sticky 컴팩트 헤더 적용:

  * 좌측 Nav가 존재하는 모든 탭(editor, signals, integrity, ecutest, taeditor, utility, grammars)에서 상단 헤더의 Nav 토글 버튼(#btnToggleSubNav)을 동일한 스타일로 제공

  * 스크롤 시 #topHeaderBar가 상단에 고정(position: sticky; top: 0)되어 따라 내려오도록 적용하고, 헤더 라인과 타이틀 폰트·카드·배지 크기를 1pt(1px) 축소

  * Admin 1) Pre/Post 관리의 Package 검색 자동완성 드롭다운(#adminPrePresetAcDropdown, #adminPostPresetAcDropdown)에 100% 불투명 배경 및 최상위 z-index를 적용하여 뒤쪽 요소가 비치지 않도록 수정
    Phase 55 (v50.10) — Admin 표 좌우 스크롤 · Pre/Post 고대비 & Placeholder 정렬 및 미등록 X 표시 · PKG 실행 순서 통합 · Sticky Nav 상단 설명란 보정 · ENG 번역 전수 점검

* Admin 2) Package 매핑 표 & 3) 문법 규칙 좌우 스크롤 및 말줄임 제거: 테이블 내 패턴, 문구, 폴더 경로, 파일명(\*.pkg), 설명 입력창이 텍스트 길이에 맞춰 충분한 너비(size 및 min-width)를 확보하고 좌우 스크롤(overflow-x: auto)되도록 개선하여 말줄임(...)이나 잘림 없이 전체 텍스트를 확인 가능.

* Admin 1) Pre/Post 관리 고대비 · 파일명 단독 표시 · 미등록 X 표시 · Placeholder 정렬:

  * 좌측에 있던 문구, 연결된 Package 고정 라벨을 제거하고 각각 placeholder="문구", placeholder="연결된 파일명 (\*.pkg)"로만 표시하여 1줄 차와 2줄 차 입력 박스의 좌측 정렬을 완벽히 통일.

  * 2번째 줄에는 경로(Path)를 제외하고 오직 연결된 패키지 파일명(\*.pkg)만 표시하며, 2) Package 매핑 표에 등록된 패키지가 아니면 명확한 고대비 X 표시를 출력.

  * 테마1/테마2 모두에서 문구 입력창과 연결된 패키지 상태창의 배경색·글자색 대비를 대폭 강화.

* Pre/Post PKG 실행 순서 단일 통합 및 1) Export 미리보기·2) 검증 테이블 명칭 일원화:

  * 1. Export 미리보기 카드 최상단(#cond, #crit 미리보기 바로 위)에 Pre와 Post의 패키지 호출 흐름(Pre ➔ #cond·#crit ➔ Post)을 하나로 통합한 PKG 실행 순서 박스를 배치.

  * 좌측 Nav 버튼(1) Export 미리보기, 2) 검증 테이블)과 본문 토글 버튼 명칭을 모두 일관되게 변경.

* 좌측 Sub-Nav Sticky 상단 설명란 가림 해결: 상단 Sticky 헤더(#topHeaderBar) 아래로 좌측 Nav가 따라 내려올 때 상단 설명란(규칙 메뉴, ⚡ 미리보기·렌더링 열기/접기 등)이 헤더에 가려지지 않도록 Sticky 오프셋(top: 58px) 및 스크롤 계산식을 보정.

* 스튜디오 ENG 모드 전체 텍스트·배지·버튼·속성 전수 영문화: 새로 변경된 버튼·배지·상태 문구·툴팁·동적 카운터를 모두 STUDIO_I18N_DICT 및 동적 번역 패턴에 반영하고, 실시간 렌더링 시에도 즉시 영문 번역이 유지되도록 개선.
  Phase 56 (v50.11) — 스튜디오 자동완성 색 대비 보정 · PTC 산출물 단일 Excel 버튼 · 신호 사전/Override 개별 접기 및 설정창 통합 · Override(.xlsx/.xam) 전용 탭 라우팅 · Admin-Studio JSON 간섭 차단 · Admin에서 Studio Baked HTML 추출

* 스튜디오 자동완성 드롭다운 고대비 수정: #content 내부의 .text-white/.text-slate-200 색상 규칙과 .ac-dropdown-box 배경색이 겹쳐 글씨가 보이지 않던 문제를 해결하기 위해, 모든 자동완성 창(Pre, Post, Test Flow, Evaluation Criteria, TA Editor)에 100% 불투명 화이트 카드(#ffffff)와 진한 네이비/블루/에메랄드 텍스트 대비를 강제 적용.

* PTC 산출물 다운로드 버튼 단순화: 3. PTC 산출물에서 불필요한 CSV 및 XML 다운로드 버튼을 제거하고 Integrity Excel (.xlsx) 다운로드 버튼만 남기도록 간소화.

* 신호 사전 접기 / Override 접기 분리 및 Override 설정창 통합:

  * 좌측 Nav의 렌더링 컨트롤을 **1) 신호 사전**과 2) Override 매핑 2개 버튼으로 분리하여 각각 독립적으로 열기/접기가 가능하도록 개선.

  * Override 설정(Override 적용, Swt 동시 인가, Override.c 로드, 엑셀 / .xam 로드, \[접두어 설정 ▾\] 등)을 Override 매핑창(#overrideMappingEditorDrawer) 내부에 통합 배치하여 매핑창과 설정창이 함께 열리고 접히도록 개선.

* Override .xlsx / .xam 로드 시 Override 탭 및 목록으로 자동 라우팅:

  * Override 관련 .xlsx 또는 .xam 파일을 로드할 때 A2L 탭이나 파일 목록으로 잘못 분류되거나 누락되지 않도록 isOverrideOnly 플래그와 MODEL(Plant model) 매핑을 적용하고, 로드 즉시 4. Override · 기타 파일 목록과 ⚡ Override 책갈피 탭에 자동 표시되도록 수정.

* Admin JSON ↔ Studio.html 상호 간섭 완전 차단:

  * Studio.html에서 JSON 로드 시 packageMappings의 traceAction 필드가 유실되거나 Studio.html이 Admin.html의 스토리지(ecu_test_studio_master_rules_v50 / ecu_test_admin_state_v50)를 역으로 덮어쓰던 문제를 해결하고, Admin과 Studio의 로컬 스토리지 키를 분리하여 상호 간섭을 원천 차단.

* Admin에서 Baked HTML 실행 시 ecu_test_integrity_studio.html (메인 스튜디오 UI) 생성:

  * Admin.html에서 Baked HTML 클릭 시 Admin의 모든 최신 규칙·Pre/Post·패키지 매핑·신호 사전·Override 데이터를 내장하면서 내부 UI("알맹이")는 일반 사용자용 ecu_test_integrity_studio.html (Test Case Editor 5개 탭 + KOR/ENG 지원)으로 자동 변환하여 추출하도록 개선.
    Phase 57 (v50.12) — Admin 단일 마스터 관리 & Studio / Utility HTML 원클릭 추출

* Admin 단일 마스터 아키텍처: 별도 JSON 배포나 백엔드 없이 ecu_test_integrity_admin.html 1개만 원본(Master)으로 관리하고, 일반 사용자 배포용 HTML을 원클릭으로 추출하도록 일원화.

* 2종 독립 HTML 추출 버튼:

  * 📦 Baked HTML (#btnExportBakedStudioHtml): 5개 탭(1. TC 에디터 \~ 5. TA Editor)과 KOR/ENG 전환기를 갖춘 실무자용 ecu_test_integrity_studio.html 추출.

  * 🛠 Utility HTML 추출 (#btnExportBakedUtilityHtml): 1. Utility (BETA)(Utility 1\~5)와 2. 신호 사전 탭을 갖춘 독립 실행형 ecu_test_integrity_utility.html 추출.

* 스토리지 격리 및 마스터 규칙 우선 적용: ecu_test_admin_state_v50 / ecu_test_studio_state_v3 / ecu_test_utility_state_v50로 로컬 스토리지를 완전 분리하고, 추출된 HTML 실행 시 내장된 Admin 마스터 규칙을 항상 우선 적용.
  Phase 58 (v50.13) — All-in-One Admin 마스터(data-export-scope & @EXPORT_SCOPE) 기반 단일 소스 태그 슬라이싱 아키텍처 완성

* 요구사항 요약:

  1. 유지보수는 8개 전체 탭(1. TC 에디터, 2. 신호 사전, 3. 문법 & 정규화 규칙, 4. PTC 산출물, 5. PKG 변환, 6. TA Editor, 7. Utility, 8. To-Do & 현황)이 모두 포함된 ecu_test_integrity_admin.html (All-in-One Master) 단 하나의 파일에서만 수행하도록 일원화.

  2. HTML 태그의 data-export-scope="studio", "utility", "studio,utility", "admin" 속성과 JS 코드의 // \[@EXPORT_SCOPE_START: ...\] \~ // \[@EXPORT_SCOPE_END: ...\] 마커를 기준으로 슬라이싱하여 실무자용 ecu_test_integrity_studio.html(5개 탭)과 유틸리티 전용 ecu_test_integrity_utility.html(2개 탭)을 자동 생성.

* 핵심 구현 내역:

  * exportBakedStandaloneHtml 및 stripTaggedScriptBlocksByScope를 통해 DOM 요소 필터링, 좌측 #nav 탭 번호(1., 2., ...) 자동 재부여, 기본 활성 탭(grammars / editor / utility) 전환, <script id="bakedMasterStateJson" type="application/json"> 상태 내장(Self-Baking) 및 미사용 스코프 코드 블록(ADMIN_ONLY, UTILITY_ONLY, STUDIO_EDITOR_ONLY, STUDIO_PKG_INT_ONLY, STUDIO_TA_ONLY) 자동 제거 구현.
    Phase 59 (v50.14) — 미사용(Dead) 레거시 UI/코드 1,200줄 이상 경량화 및 타이틀·로고 레이아웃 정렬

* 요구사항 요약:

  1. 5. PKG 변환 탭에서 사용하지 않는 로컬 Python 서버 실행 안내/명령어/.bat UI, 로컬 서버 이식 버튼, .py 다운로드 버튼, Python API 코드 미리보기 버튼 및 관련 생성 함수를 완전히 제거하고 \*.pkg 다운로드, 대상 TC 선택, 패키지 구조 트리, \*.pkg XML 코드 미리보기 중심으로 경량화.

  2. 2. 신호 사전 상단의 타겟 환경: SIL | HIL 토글 버튼 제거(5. PKG 변환의 #pkgTargetEnvSelect에서만 제어), 5. PKG 변환 좌측의 MultiCheck 변수저장 OFF (고정) 문구 제거, 4. PTC 산출물 좌측의 미사용 2) 전체 TC 문법 검증 연산 버튼 제거.

  3. Admin 타이틀(Test Case Editor + ADMIN 배지)이 사이드바 #logo .logo-box 및 상단 #topHeaderBar .top-logo-concept-c 내에서 칸을 넘어가지 않도록 세로 스택 및 고정 레이아웃 적용.
     Phase 60 (v50.15) — Utility 2 (3종 Helper Excel 직접 로드) & Utility 5 (파일별 개별 Path 레지스트리 및 2-Pane GUI 하위 폴더·파일 트리 탐색기) 고도화 및 v50.15 버전 동기화

* 요구사항 요약:

  1. Utility 2: Utility 5와 중복되던 PTC SI Direct 바를 제거하고, 1. L2 Helper Excel / 2. L4 Helper Excel / 3. Hyb Excel (L2·L4·L5) 직접 파일 업로드·시트 선택·비우기 카드 및 📂 L2·L4·Hyb 엑셀 일괄 선택 기능으로 개편.

  2. Utility 5 좌측 패널: Helper, A2L, DBC, Override 등 각 파일의 경로가 서로 다른 실무 환경을 반영해 문구 / Path ({project_path}) / 파일명(.확장자) / 분류(L2, L4, HYB, A2L, DBC, OVERRIDE, SPLIT)를 개별 행으로 저장·편집·적재하는 레지스트리 테이블(#util5FileEntriesTableBody) 구현.

  3. Utility 5 우측 패널: si projecto / si viewproject --recurse 출력 또는 로컬 폴더(webkitdirectory) 로드 시 하위 디렉터리와 파일을 탐색하는 2-Pane GUI 하위 폴더 & 파일 탐색기(#util5GuiBreadcrumbBar, #util5GuiFolderTreePane, #util5ProjectMembersTableBody) 구현 (폴더 이동, 파일 클릭 시 좌측 프리뷰, \[+담기\] 시 서브프로젝트 project.pj 경로 자동 도출 등록, \[적재\] 시 분류 슬롯 즉시 적재).

  4. v50.15 버전 및 슬라이서 정합성 정리: ecu_test_integrity_admin.html 내 중복 정의된 stripTaggedScriptBlocksByScope 함수를 단일 정규 함수로 정리하고, 상단 배지(Serverless v50.15), JSON 내보내기 버전(50.15), STUDIO_I18N_DICT 한/영 번역 및 3종 HTML(Admin, Studio, Utility)의 Node.js 런타임 검증(Sync/Async 오류 0건) 완료.
     Phase 61 (v50.19) — Override 매핑 .xam 제거, 5. Plant model (.m·.xam) 3환경(SIL / HIL:dSPACE / HIL:ETAS) 분리 로드 및 직접 tsWrite, Package 매핑 애너그램·과거형(형태소) 정규화 엔진

* 요구사항 요약:

  1. 2. 신호 사전에서 Override 매핑 시 .xam 파일은 호환되지 않으므로 Override 로더 및 설정창에서 .xam 업로드/내보내기를 제거.

  2. 2. 신호 사전 좌측 파일 로드 패널에 5. Plant model (.m·.xam) 카드를 추가하여 .m 파일(MATLAB 스크립트/데이터 사전) 및 .xam 파일(ECU-TEST Master/Global Mapping)을 SIL, HIL:dSPACE, HIL:ETAS 3개 환경으로 나누어 로드할 수 있도록 구현하고, Plant model로 등록된 신호는 별도의 Override 매핑 없이 즉시 해당 신호를 직접 tsWrite할 수 있도록 처리.

  3. Package 매핑에서 어순이 다르거나 수동태/과거형으로 작성된 문구(예: 등록된 "Press Brake Pedal"에 대해 "Ensure brake pedal is pressed" 입력)도 자동 매칭되도록 Ensure, is 등 불용어(Stopwords) 제거 + 영문 과거형/파생어 자동 형태소 분석(pressed → press, released → release 등) 및 사용자 편집형 어형·과거형 사전(pkgNormStemMap) + 어순 무관 애너그램(Anagram / Token-Set) 매칭 엔진(buildPkgAnagramKey) 구현.

* 핵심 구현 내역:

  1. Override 매핑 .xam 제거 (4. Override (.c·엑셀)):

     * 좌측 4. Override (.c·엑셀) 카드 및 본문 Override 매핑 & 설정 드로어에서 .xam 확장자와 .xam 내보내기 버튼을 제거하고, 순수 \*\_Override.c 폴더 스캔 및 Override 엑셀(.xlsx/.xls/.csv)만 전담하도록 명확히 분리.

  2. 5. Plant model (.m·.xam) 3환경 분리 로더 및 직접 tsWrite (parsePlantModelMOrXamContent & applyPlantModelParsedSignals):

     * SIL, HIL:dSPACE, HIL:ETAS 개별 업로드 버튼 및 \[🧩 Plant model\] 탭 전용 컨텍스트 바(#ctxBookmarkPanelModel, 환경별 필터 전체 Plant / SIL / HIL:dSPACE / HIL:ETAS 및 + Plant 샘플(.m/.xam) 버튼) 탑재.

     * MATLAB .m 파일(Simulink.Signal, Simulink.Parameter, mpt.Signal, 구조체 경로, 문자열 경로, 변수 할당 및 주석 내 단위/범위)과 .xam XML 파일을 파싱하여 환경별 경로(pathSil, pathHilDspace, pathHilEtas)에 분리 저장.

     * resolveA2lWriteOverride에서 Plant model 신호(mappingType === "MODEL", isPlantModelSignal: true)는 항상 null을 반환하여 OL\_/Swt\_ Override 대체 없이 <TESTSTEP name="TsWrite" xsi:type="tsWrite">로 해당 신호를 직접 인가하도록 보장하고, 5. PKG 변환 타겟 환경 선택기(#pkgTargetEnvSelect)에서 SIL, HIL:dSPACE, HIL:ETAS, HIL 선택 시 해당 환경의 VARIABLE-PATH로 xaModelSignal 매핑을 자동 생성.

  3. Package 매핑 애너그램(Anagram) + 영문 과거형/어형 정규화 엔진 (stemPkgWordToken, buildPkgAnagramKey, pkgAnagramMap):

     * 불용어(ensure, is, are, was, were, be, been, the, a, an, to, if, any, position) 제거 후 각 단어 토큰을 stemPkgWordToken으로 기본형 변환(내장 영문 과거형 -ed/-ied/자음중복/불규칙 동사 규칙 + 사용자 사전 state.pkgNormStemMap 우선 적용)한 뒤 알파벳순으로 정렬한 애너그램 키("Ensure brake pedal is pressed" → "brake pedal press" == "Press Brake Pedal")로 O(1) 매칭 및 인자({VALUE}) 추출 지원.

     * 3. 문법 & 정규화 규칙 > 4) 패키지 정규화에 어형·과거형 사전 (애너그램 연동) 편집 카드를 추가하여 사용자가 언제든 pressed=press 같은 커스텀 변환쌍을 직접 추가·수정·삭제할 수 있도록 구성.
          Phase 62 (v50.19) — Package 매핑 Wild card (AND 조건 키워드) 매칭 목록 전환 및 단일 마스터 HTML 직결 배포 최적화

* 요구사항 요약:

  1. 기존 과거형/수동태 원형 복원 & 동의어 사전 대신, Wild card 목록 (표준 문구 ↔ AND 조건 매칭)을 따로 관리하여 표준 문구(예: "Press Brake Pedal" 또는 "Press Barke pedal")에 대해 지정한 Wild card 키워드들(예: press, brake, pedal 또는 press, bake, pedal)이 문장 내에 모두(AND 조건) 존재하면 어순이나 과거형(pressed 등)에 관계없이 즉시 해당 표준 문구로 매칭되도록 개선.

  2. 불필요하게 분리 생성되던 미완성/파생 .html 파일 생성을 중단하고, 단일 마스터 ecu_test_integrity_admin.html만 번들(ecu_test_integrity_studio_v50.17_bundle.zip)에 포함하며 채팅 화면에서 바로 HTML을 열어 실행할 수 있도록 제공.

* 핵심 구현 내역:

  1. 3. 문법 & 정규화 규칙 > 4) 패키지 정규화 내 Wild card 목록 (표준 문구 ↔ AND 조건 매칭) 탑재 (state.pkgWildcardRules, findBestWildcardRuleMatch, checkSingleWildcardKeyword):

     * 각 규칙은 표준 문구 (Standard Phrase)와 Wild card 키워드 (콤마 구분, AND 조건)로 구성되며, 입력 문장 내에 모든 키워드가 포함(every AND 조건)되면 대소문자·어순·어미(pressed, pressing 등)와 무관하게 즉시 매칭.

     * {VALUE} 플레이스홀더를 포함한 규칙(예: "Press accelerator pedal {VALUE}" ← press, accelerator, pedal, {VALUE})은 수치/단위 인자(50% → arg1=50)까지 자동 추출하며, ⚡ Package 표 기준 자동 생성 버튼으로 2) Package 매핑 표의 문구들을 원클릭 동기화 지원.

  2. 단일 마스터 HTML(ecu_test_integrity_admin.html) 중심 패키징 정리:

     * 불필요한 파생 .html 파일 생성 및 구글 드라이브 문서 자동 변환 업로드를 제거하고, ecu_test_integrity_admin.html 원본을 바로 열 수 있도록 구성.
       Phase 63 (v50.19) — PTC 더미 데이터 완전 폐기 및 .bat 없는 3대 실제 PTC 프로젝트 트리·파일 직결 아키텍처 탑재 (Utility 5 & Utility 4)

* 요구사항 요약:

  1. Utility 5 및 Utility 4에 남아 있던 모든 PTC 더미 데이터(DEFAULT_SI_FILE_ENTRIES, 초기 더미 트리 11건, loadSampleSiProjectTree, simulateSiCheckedOutFileAndLoad, buildRealisticPtcRawResponseForIds)를 100% 폐기.

  2. 매번 .bat 파일을 다운로드·실행하지 않고도 브라우저에서 실제 PTC 프로젝트 트리를 탐색하고 실제 파일을 즉시 적재할 수 있는 대안 아키텍처 연구 및 3대 직결 방식 구현.

* 핵심 구현 내역:

  1. 방식 1 — 브라우저 File System Access API (window.showDirectoryPicker) 기반 로컬 PTC Sandbox 폴더 직결 (Zero-Bat, 무설치):

     * \[📂 방식1: 로컬 PTC Sandbox 폴더 직결\] 클릭 시 PC의 PTC Sandbox 폴더(또는 네트워크 드라이브)를 직접 마운트하여 하위 폴더 전체와 project.pj 설정 파일(projectName=...)을 재귀 스캔하고, 2-Pane GUI 트리에 실제 폴더·파일 구조를 즉시 표시.

     * 트리에서 \[적재\] 클릭 시 .bat나 CLI 호출 없이 브라우저가 마운트된 FileSystemFileHandle에서 직접 바이너리를 읽어 Utility 2, 2. 신호 사전, 5. Plant model (.m/.xam) 슬롯에 즉시 로드.

  2. 방식 2 — Windows 내장 PowerShell 1줄 로컬 브릿지 (https://www.google.com/search?q=http://127.0.0.1:18765, Zero-Bat 실시간 서버 조회):

     * Python 등 별도 런타임 설치 없이 모든 Windows PC에 기본 내장된 PowerShell System.Net.HttpListener를 활용하는 1줄 브릿지 명령어 복사 기능(\[🔌 방식2: 실시간 SI 브릿지\]) 탑재.

     * 최초 1회 실행해 두면 브라우저의 \[🔍 트리 조회\] 및 \[적재\] 버튼이 fetch("https://www.google.com/search?q=http://127.0.0.1:18765/si/viewproject") 및 fetch("https://www.google.com/search?q=http://127.0.0.1:18765/si/checkout")을 호출하여 실시간으로 si viewproject --recurse와 si projectco --nolock / si projecto를 실행하고 파일 바이너리를 스트리밍 적재.

  3. 방식 3 — PTC Integrity GUI 클라이언트(Ctrl+C) 클립보드 즉시 붙여넣기 & project.pj 다중 포맷 파서 고도화:

     * si viewproject --recurse의 들여쓰기(Indentation) 기반 다단 서브프로젝트 계층 구조, PTC GUI 클라이언트 테이블 복사(Ctrl+A → Ctrl+C), 원본 project.pj 파일을 모두 인식하도록 parseSiViewProjectOutput 고도화.
       Phase 64 (v50.19) — 신규 TC 자동 ID 빈칸(Blank) 지원, PowerShell 브릿지 기반 Test Suite / Test Case 자동 판별 Import & 지정 Field 뷰어, 실시간 양방향 Export 완성

* 요구사항 요약:

  1. 스튜디오에서 새로운 TC를 생성(+ 새 TC 추가, Utility 1.2 -> TC 생성, IT 대량 신호 자동 TC 생성, \[신규(빈칸)\] 버튼)하거나 4. PTC 산출물에서 Excel(.xlsx)로 내보낼 때 신규 TC의 ID를 빈칸("")으로 비워둘 수 있도록 구현하여 PTC Import 시 새 Item ID가 자동 채번되도록 지원.

  2. PowerShell 브릿지(https://www.google.com/search?q=http://127.0.0.1:18765)를 중심으로 Utility 4에서 Test Suite ID 또는 Test Case ID를 검색(Enter 또는 \[🚀 ID 검색 & 즉시 Import\])하면 자동으로 Suite 하위 TC 전체(im issues) 또는 단일/다중 TC(im viewissue)를 판별하여 즉시 스튜디오로 Import.

  3. ID를 가져왔을 때 사용자가 지정한 필드(지정 필드 1\~5 및 추가 표시할 PTC 필드명)의 내용이 Utility 4 하단의 \[지정 Field 뷰어\] 테이블에 필드별로 즉시 시각화되도록 구현하고, 스튜디오 TC를 PTC로 올릴 때도 PowerShell 브릿지를 통해 신규 생성(im createissue 후 발급된 새 ID 자동 반영) 및 기존 수정(im editissue)이 즉시 수행되도록 완성.

Phase 65 (v50.20) — 1. TC 에디터 내 Test Suite (TS) / Test Case (TC) 즉시 Import 통합

* 좌측 사이드바 PTC TS / TC 바로 Import 패널 업그레이드:

  * 기존 더미 전용 TS 샘플 로드를 완전히 폐기하고, Utility 4로 이동하지 않아도 1. TC 에디터 좌측 패널에서 바로 Test Suite ID 또는 Test Case ID(쉼표 다중 입력 지원)를 입력해 PowerShell 브릿지(https://www.google.com/search?q=http://127.0.0.1:18765/im/import)로 즉시 조회·Import(🔍 조회·Import, Enter 단축키 지원)할 수 있도록 통합.

  * 조회 모드 선택기(#editorPtcImportModeSelect) 제공:

    * 자동 판별 (TS 우선 → TC): im issues --queryDefinition=(field\[Document ID\]=ID) 조회 후 하위 TC가 있으면 Test Suite 전체를 로드하고, 0건이면 자동으로 im viewissue 단일/다중 TC 조회로 전환.

    * Test Suite (하위 TC 전체): 지정한 Document ID의 하위 Test Case 리스트 전체 Import.

    * Test Case (단일/다중 ID): 입력한 TC ID(들)를 im viewissue로 즉시 Import.

  * 다양한 로컬 파일 즉시 Import (📂 파일): .xlsx, .xls, .csv, .xml, .txt, .json 파일을 1. TC 에디터에서 바로 파싱하여 TC 목록에 적재하고, 첫 번째 TC를 즉시 에디터 폼에 로드하며 Utility 4의 지정 필드 뷰어 테이블과도 자동 동기화.

  * 클립보드 즉시 Import (📋 붙여넣기): PTC Integrity GUI에서 Ctrl+C로 복사한 행이나 CLI 출력 텍스트를 원클릭으로 파싱하여 에디터로 즉시 Import.

  * PowerShell 브릿지 원클릭 복사 (⚡ PS브릿지 복사): 에디터 좌측 패널에서도 바로 PowerShell 로컬 브릿지 스크립트를 클립보드에 복사 가능.

* 우측 에디터 1. TC ID 우측 🔍 PTC조회 버튼 탑재:

  * 현재 편집 중인 TC의 1. TC ID 입력란(#tcIdInput)에 PTC ID를 입력하고 🔍 PTC조회(#btnFetchActiveTcById) 버튼을 누르거나 Enter 키를 치면 해당 TC(또는 TS)를 PTC에서 즉시 가져와 에디터 폼에 반영.

* .xlsx 내보내기(💾 .xlsx) 신규 TC 빈칸 ID 보존:

  * 1. TC 에디터에서 .xlsx로 내보낼 때 기존에 임의 번호(2172569 + idx)를 채우던 방식을 제거하고, 신규 생성 TC의 빈칸 ID("")를 그대로 유지하여 PTC Excel Import 시 신규 Item ID가 자동 채번되도록 개선.

Phase 66 (v50.21) — TS 샘플 로드 버튼 복원 및 Package 매핑 즐겨찾기 별표(★) 기반 자동완성 검색 필터링

* 1. TC 에디터 내 TS 샘플 로드 버튼 복원:

  * PTC TS / TC 바로 Import 카드에 🚀 ID 즉시 Import 버튼과 나란히 TS 샘플 로드(#btnLoadSampleTestSuite) 버튼을 복원하여, 실시간 PTC 브릿지 Import와 150건 대량 샘플 TC 로드를 모두 원클릭으로 사용할 수 있도록 구성.

* 3. 문법 & 정규화 규칙 > 2) Package 매핑 표 즐겨찾기 별표(★ / ☆) 버튼 추가:

  * 각 Package 매핑 행마다 즐겨찾기처럼 켜고 끌 수 있는 단일 별표 토글 버튼(★ 활성 / ☆ 비활성, data-toggle-pm-star)을 탑재하고, 테이블 헤더에 전체 일괄 토글 버튼(#btnToggleAllPkgStarHeader)도 함께 제공.

* 별표(★) 활성화된 Package만 자동완성(자동완성기능)에서 검색되도록 필터링:

  * getGrammarCommandCandidates() (Test Flow #cond 및 Evaluation Criteria #crit 에디터 자동완성), updatePrePostAutocomplete() (Pre/Post Conditions 에디터 자동완성), bindAdminPresetPkgAutocomplete() (1) Pre/Post 관리 프리셋 자동완성), unifiedPkgPhraseDatalist 모두에서 isPkgStarred(pm) === true(★ 활성화)인 Package만 검색·표시되도록 적용.

  * Test Flow 에디터 자동완성에서는 별표(★)가 켜진 Package에 대해 구문 첫 단어뿐 아니라 중간 단어/파일명 검색 및 Ensure  / Set  접두어 입력 후 매칭도 함께 지원하며, 드롭다운에 ★ 배지를 표시.

Phase 67 (v50.22) — TS 샘플 로드 샘플 개수 축소 (150건 → 10건)

* 샘플 데이터 경량화 (10개 핵심 TC만 유지):

  * 기존 150건의 과도한 더미 샘플 생성 로직(generateSimulatedTestSuite)을 사용자가 한눈에 검토하기 쉬운 10건으로 대폭 축소.

  * 1. TC 에디터 좌측 사이드바 버튼명을 TS 샘플 로드 (10건)(#btnLoadSampleTestSuite)으로 갱신하여 직관성 강화.

  * 10건의 샘플은 주행 속도/레이더 타겟 거리 시나리오별 핵심 Functional Test Case 9건(Pass)과 문법/신호 검증 테스트용 1건(Fail)으로 최적 구성.

Phase 68 (v50.23) — Utility 4 UI/UX 대폭 간소화 (직관적인 3-Step 워크플로우 정리)

* 사용 흐름 중심의 3단계(STEP 1 → STEP 2 → STEP 3) 레이아웃 재설계:

  * 상단에 \[준비 → STEP 1·2 → STEP 3\] 요약 안내 배너와 \[사전 준비: PowerShell 브릿지 1줄 복사\] 버튼을 직관적으로 배치.

  * STEP 1 (내가 조회할 PTC Field 지정): 자주 바꾸는 추가 표시 Field 입력창만 전면에 노출하고, 기본 5대 매핑 필드명 변경은 접이식(<details>)으로 정리.

  * STEP 2 (PTC에서 가져오기 & 지정 Field 결과 표): 1줄 검색 바(조회 유형 + TS ID / TC ID 입력 + 🔍 ID 검색 & 즉시 Import / 📋 붙여넣기 / 📂 파일) 바로 아래에 조회된 항목의 지정 Field 내용 표를 직결 배치하여 검색 즉시 한눈에 결과를 확인하도록 개선.

  * STEP 3 (스튜디오 TC를 PTC로 올리기): 1줄 액션 바(반영할 TC 선택 + 수정/신규 생성 + 대상 PTC ID + 🚀 선택 TC를 PTC로 즉시 반영)로 단순화.

  * 평소 사용할 필요가 없는 서버 Hostname/Port/계정 입력란 및 CLI/JSON/원시 응답 텍스트창은 하단 ⚙️ 고급 설정 & 수동 디버깅 접이식 메뉴 안으로 숨겨 화면 복잡도를 대폭 제거.

Phase 69 (v50.24) — PowerShell 브릿지 and 토큰 에러 해결, Package 매핑·정규화 단일 통합(정렬/순서변경/10개 페이징), PTC 화면 모드 & 커서 TC Footer 미리보기, TS 샘플·Utility 5·TCM 완전 제거

1. PowerShell 브릿지(PS 브릿지 복사) 예기치 않은 and 토큰 에러 완벽 해결:

   * 기존 powershell -Command "..." 문자열 중첩 따옴표로 인해 --queryDefinition="((field\[...\]=\$cleanId) and ...)" 구문에서 and가 PowerShell 명령어 토큰으로 오인되거나 긴 줄 붙여넣기 시 ues --queryDefinition으로 잘리던 문제를 해결하기 위해, 내부 인자를 배열 스플래팅(@a1, @a2)으로 분리하고 전체 스크립트를 UTF-16LE Base64 (powershell -NoProfile -ExecutionPolicy Bypass -EncodedCommand ...)로 인코딩하여 어떤 환경에서도 따옴표/토큰 파싱 에러가 발생하지 않도록 개선.

2. TS 샘플 로드 버튼 및 더미 생성 데이터 완전 삭제:

   * 1. TC 에디터 좌측의 TS 샘플 로드 버튼(#btnLoadSampleTestSuite, #btnLoadLargeTsDemo)과 generateSimulatedTestSuite 더미 생성 함수를 완전히 제거.

3. 2. Package 매핑 표와 4) 패키지 정규화(Wild card) 단일 통합 + 정렬(Sorting) + 순서 변경(▲/▼) + 10개씩 페이지네이션:

   * 이원화되어 있던 2) Package 매핑 표와 4) 패키지 정규화를 2) 통합 Package 매핑 & 정규화 (Wild card) 하나로 통합하여, 한 행에서 순서(▲/▼) | 별표(★) | 표준 문구 | 정규화 Wild card (AND 키워드) | 폴더 경로 | 파일명 | 인자 | Trace 동작 | 삭제를 모두 관리하도록 일원화.

   * Sorting 기능: 문구 오름/내림차순, 파일명 오름/내림차순, 별표(★) 우선, Wild card 키워드 개수순 정렬 및 \[⇅ 정렬 순서 확정\] 지원.

   * 순서 변경 기능: 각 행의 ▲ / ▼ 버튼으로 매핑 우선순위 순서를 즉시 변경 가능.

   * 10개씩 페이지네이션: 전체를 한 번에 렌더링하지 않고 페이지당 10개씩 분할 렌더링하며 « 처음 / ‹ 이전 / 페이지 번호 / 다음 › / 마지막 » 이동 바 제공.

4. 1. TC 에디터 내 🖥️ PTC 화면처럼 보기 (헤더 + 내용) 전환 버튼 탑재:

   * 상단에 🖥️ PTC 화면처럼 보기 (헤더 + 내용) 버튼(#btnTogglePtcDocViewMode)을 추가하여, 클릭 시 상단에 PTC Document Header가 표시되고 그 아래에 각 TC의 헤더 바(ID / Title / Variant / State / Env)와 세부 내용(Text / Pre / Test Flow #cond / Evaluation Criteria #crit / Post / Comment)이 펼쳐지는 PTC Document View 모드로 즉시 전환 및 인라인 편집 지원.

5. 커서가 위치한 TC만 보여주는 접이식 하단 Footer TC 미리보기 독(#tcEditorFooterPreviewDock):

   * 에디터 하단 Footer에 현재 커서가 위치한 단일 TC의 Pre / Post / #cond / #crit 미리보기만 실시간 표시하고, ▲ 커서 TC 미리보기 열기 / ▼ 접기 버튼으로 언제든 열고 접을 수 있도록 구현.

6. Utility 5 완전 삭제:

   * 6. 유틸리티 좌측 메뉴 및 본문에서 Utility 5 영역(#utilCardSection5)을 완전히 삭제.

7. Signal Recording의 Signal Group에서 "TCM" 제거:

   * buildTraceRecordingXml 내 SIGNAL-GROUPS 및 RECORDING-GROUP 목록에서 "TCM"(Recording group for TCM)을 완전히 제거.

Phase 70 (v50.25) — 패키지 정규화 무시 단어/무시 기호 상시 노출 복원, PTC 화면처럼 보기 엑셀형 테이블 및 드래그 컬럼 너비 조절, 스크롤바 가시성 강화

1. 패키지 정규화 무시 단어 (Stopwords) & 무시 기호 (Symbols) 상시 노출 복원:

   * 접이식 메뉴 안에 숨겨져 있던 무시 단어 (Stopwords) 카드와 무시 기호 (Symbols) 카드를 2) 통합 Package 매핑 & 정규화 섹션 내 상시 노출 레이아웃으로 복원하여, 단어/기호 추가·삭제·CSV 일괄 편집·기본값 복원을 즉시 수행 가능하도록 개선.

2. 1. TC 에디터의 PTC 화면처럼 보기를 엑셀 스타일 테이블(상단 컬럼 헤더 + 하단 Test Case 행) 및 드래그 컬럼 너비 조절로 개편:

   * 엑셀 시트처럼 상단에 12개 고정 컬럼 헤더(#, ID, Project Variant, State, Test Case Name, Text, Pre Conditions, Test Flow (#cond), Evaluation Criteria (#crit), Post Conditions, Test Case Comment, Test Environment)를 배치하고, 그 아래 각 행(<tr>)마다 Test Case가 나열되어 셀 내부에서 바로 편집할 수 있도록 재설계.

   * 각 컬럼 헤더 우측 경계선에 마우스 드래그 리사이저(.ptc-col-resizer)를 탑재하여 원하는 너비로 자유롭게 드래그 조절(및 localStorage 자동 저장, \[↔ 컬럼 너비 초기화\] 지원) 가능.

3. 전역 스크롤바 너비 확대(12px) 및 고대비 가시성 개선:

   * 기존 6px 저대비 스크롤바를 12px 너비·높이의 고대비 스카이 블루 그라데이션(#38bdf8 → #0284c7) 스크롤바로 업그레이드하여 가로/세로 스크롤 위치를 한눈에 파악하고 마우스로 쉽게 잡을 수 있도록 개선.

Phase 71 (v50.26) — PTC 화면처럼 보기 런타임 에러 수정 및 1) Export 미리보기 원래 위치로 원복

1. PTC 화면처럼 보기 에러 완벽 수정:

   * renderPtcDocumentModeView 내부 행 클릭/셀 포커스/편집/폼 전환 시 존재하지 않는 loadActiveTcIntoEditor()를 호출하던 ReferenceError를 완전히 제거하고, renderTestCaseList() 및 renderActiveTestCaseEditor()로 정상 동기화되도록 수정.

   * localStorage에 구버전 샘플 로더의 불완전한 행 데이터나 의도적 문법 오류(Unregistered_Sensor, INVALID_SYNTAX)가 남아 있을 경우 로드 시 자동으로 정화하도록 보강.

2. 하단 Footer 미리보기 제거 및 기존 1) Export 미리보기 원복:

   * 하단 고정 Footer 미리보기 독(#tcEditorFooterPreviewDock)을 제거하고, 기존의 PKG 실행 순서 + 1) Export 미리보기 (클릭 시 렌더링)(7. Test Flow 미리보기 #cond / 8. Evaluation Criteria 미리보기 #crit) 구성을 원래 위치로 완전히 복원.

Phase 72 (v50.27) — compact-engineering-ui 전수 적용 및 PTC 테이블 뷰 Striped·Halcyonic 테마 완벽 통합

1. PTC 테이블 뷰에 Striped & Halcyonic 테마 디자인 완벽 적용:

   * 기존에 어두운 인라인 배경과 두꺼운 개별 textarea 테두리가 섞여 이질적이던 PTC 테이블 뷰(#ptcDocumentViewContainer / .ptc-excel-table)를 스튜디오의 Striped(Theme 1) 및 Halcyonic(Theme 2) 디자인 시스템과 완벽히 통합.

   * 상단 테이블 헤더(<thead>)에 Striped/Halcyonic 텍스처 그라데이션 헤더를 적용하고, 본문 행(<tbody> tr)은 깔끔한 화이트/슬레이트 교차 스트라이프 및 활성 행 좌측 강조 보더(.ptc-row-active)로 스타일링.

   * 셀 내부 입력 컨트롤을 심리스 스프레드시트 셀 에디터(.ptc-cell-editor)로 전환하여 평상시에는 깔끔한 표 텍스트처럼 보이고, 호버/포커스 시에만 선명한 포커스 링이 나타나도록 개선(#cond 블루 포인트, #crit 앰버 포인트, 4.5:1 이상 명도 대비 보장).

2. compact-engineering-ui 4대 원칙 반영:

   * No Prose in UI: Utility 4 상단 서술형 3단 설명 배너 및 불필요한 안내 문장을 제거(툴팁 title로 이동)하고, 버튼·라벨·컬럼 헤더·placeholder를 1\~3단어로 간결화.

   * Immutable Layout: 외부 그리드(.editor-main-grid), 사이드바(260px), 상단 헤더 구조 100% 보존.

   * Compact Density: 셀 패딩(4px 6px), 컴팩트 툴바, 3줄 기준 셀 높이로 한 화면에 표시되는 Test Case 행 밀도를 극대화.

Phase 73 (v50.28) — @compact-engineering-ui 전 페이지 배경/글씨 색상 충돌(Contrast) 정밀 검수 및 수정

1. 사용자 요청 사항

* 1페이지 (1. TC 에디터)의 PKG 실행 순서: 배경과 글씨 색깔이 같아서 보이지 않는 문제 해결

* 7페이지 (Utility > Utility 4)의 PTC Field: STEP 1/2/3 배지, PTC Field 매핑 입력창 및 지정 필드 테이블 헤더/컨트롤 바의 배경과 글씨 색상이 겹쳐 보이지 않는 문제 해결

* 각 페이지(1\~7페이지) 좌측 Sub-Nav의 기능 열기/펴기(접기) 토글 버튼: 활성화(.switch-on) 및 비활성화 상태에서 배경과 글씨 색상이 유사해 식별이 어려운 문제 해결

* @compact-engineering-ui 스킬의 엄격한 명도 대비(4.5:1 이상) 및 고밀도 UI 규칙을 적용해 전수 검수 및 수정

2. 원인 분석 및 기술적 조치 내역

3. 1페이지 PKG 실행 순서 (#unifiedPrePostPkgOrderContainer, .pkg-chip-\*) 명도 대비 수정:

   * 원인: 기본 테마(Theme 1: Striped)에서 #content .bg-slate-950/90 규칙에 의해 컨테이너 배경은 밝은 #f8fafc로 변환되었으나, 내부 칩(.pkg-chip-mandatory, .pkg-chip-reg, .pkg-chip-unreg)의 고대비 텍스트 오버라이드가 html\[data-theme="halcyonic"\]에만 한정되어 있어 밝은 배경 위에 밝은 파스텔 텍스트(#fde68a, #a7f3d0, #fecdd3)가 렌더링됨.

   * 조치: #content 내부에서 테마와 무관하게 필수 칩(#fef3c7 배경 / #78350f 텍스트 / #d97706 테두리), 등록 칩(#d1fae5 배경 / #064e3b 텍스트 / #059669 테두리), 미등록 칩(#ffe4e6 배경 / #881337 텍스트 / #e11d48 테두리) 및 타이틀(#0f172a 굵은 텍스트)이 항상 8:1 이상의 명도 대비를 유지하도록 수정.

4. 7페이지 Utility 4의 PTC Field (#utilCardSection4) 및 테이블 헤더/배지/컨트롤 바 명도 대비 수정:

   * 원인 A: Utility 4의 STEP 2/STEP 3 검색·반영 바에 사용된 .bg-slate-900/90 클래스가 #content 라이트 리매핑에서 누락되어 어두운 남색(#0f172a) 배경을 유지한 반면, 내부 <label>은 #content label 규칙에 의해 #0f172a 어두운 남색 텍스트로 강제되어 배경과 글씨가 완전히 동일한 색상으로 충돌함.

   * 원인 B: #util4DesignatedFieldsThead의 각 PTC Field 컬럼 헤더(<th class="... text-sky-300">)에서 #content .text-sky-300 (명시도 1,1,0, 어두운 파란색 #0369a1)이 #content table thead tr th (명시도 1,0,4, #ffffff)를 이겨 어두운 헤더 배경(#1e293b) 위에 어두운 파란색 글씨가 렌더링됨.

   * 원인 C: STEP 1, STEP 2, STEP 3 등 <span class="bg-sky-600 text-white"> 배지가 #content .text-white { color: #0f172a !important; }에 의해 어두운 배경 위 검은색 글씨로 렌더링되었고, STEP 1의 기본 5대 PTC Field 매핑 입력란(#utilPtcFieldPost의 .text-purple-200 등)이 접힌 <details> 내부에서 리매핑 누락된 밝은 텍스트 클래스를 사용함.

   * 조치:

     * #content 내 .bg-slate-900/90, .bg-slate-950/80 등 누락된 모든 다크 배경 클래스를 #f8fafc 밝은 배경으로 리매핑하고, .text-purple-200, .text-indigo-200, .text-cyan-200 등 누락된 밝은 텍스트 클래스를 모두 짙은 잉크 색상으로 리매핑.

     * STEP 1의 기본 5대 PTC 필드(TC 제목 필드, Pre 필드, Flow 필드, Criteria 필드, Post 필드, RichContent)를 즉시 노출하고 흰색 배경(#ffffff) + 진한 텍스트(#0f172a)로 고정.

     * #util4DesignatedFieldsThead 등 모든 다크 테이블 헤더(#1e293b)의 th\[class\] 명시도를 높여 #ffffff / #7dd3fc / #6ee7b7 / #fde68a 고휘도 텍스트가 표시되도록 수정.

     * #content 내 모든 솔리드 배지(span.bg-*-600, div.bg-*-600)의 텍스트를 #ffffff !important로 고정.

5. 전 페이지(1\~7페이지) 좌측 Sub-Nav 열기/펴기 토글 버튼 (.util-switch-btn, .util-switch-pill) 명도 대비 수정:

   * 원인: .util-switch-btn.switch-on 상태에서 연한 민트 배경(rgba(16,185,129,0.12) on #f8fafc) 위에 밝은 회색 글씨(#e2e8f0)가 적용되어 글씨가 배경에 묻혀 보이지 않았음.

   * 조치:

     * 열림 (.switch-on): 배경 #d1fae5, 테두리 #059669, 라벨 텍스트 #064e3b (Bold), 우측 상태 필(.util-switch-pill) 배경 #047857 + 텍스트 #ffffff (열기 / ON).

     * 접힘 (기본): 배경 #f1f5f9, 테두리 #94a3b8, 라벨 텍스트 #0f172a (Bold), 우측 상태 필(.util-switch-pill) 배경 #475569 + 텍스트 #ffffff (접기 / OFF).

Phase 74 (v50.29) — 3페이지 햄버거(☰) 드래그&드롭 순서 변경 및 1페이지 PTC 테이블 뷰(4페이지 산출물 스타일 + 실시간 컬럼 리사이즈) 개편

1. 사용자 요청 사항

* 3페이지(3. 문법/패키지 관리) 순서 변경 방식 개선: 기존 ▲/▼ 버튼 클릭 방식 대신 햄버거 버튼(☰)을 드래그&드롭하여 직관적으로 순서를 바꿀 수 있도록 개선

* 1페이지(1. TC 에디터)의 PTC 테이블 뷰 열 너비 조절 수정: 컬럼 경계를 드래그했을 때 열 너비가 즉시 변경되도록 수정

* 1페이지 PTC 테이블 뷰 디자인을 4페이지(4. PTC 산출물)처럼 깔끔하게 개편: 복잡한 개별 <textarea> 입력 상자 및 내부 스크롤바 대신 4페이지 PTC 산출물과 동일한 깔끔한 11-Col 표준 테이블 레이아웃을 적용하고, 셀 클릭 시에만 심리스 인라인 편집기가 열리도록 개선

2. 원인 분석 및 기술적 조치 내역

3. 3페이지 전 영역(1) Pre/Post 관리, 2) Package 매핑·정규화, 3) 문법 규칙) 햄버거(☰) 드래그&드롭 도입:

   * bindHamburgerDragReorder() 및 reorderArrayItemByDrag()를 구현하여 마우스 포인터 드래그(mousedown → mousemove → mouseup)와 HTML5 Native Drag-and-Drop을 동시에 지원.

   * 1. Pre/Post 관리(필수 Pre/Post 및 표준 Pre/Post Conditions), 2) Package 매핑·정규화(#pkgMappingTableBody), 3) 문법 규칙(#grammarTableBody)의 기존 ▲/▼ 이동 버튼을 제거하고 좌측 .drag-hamburger-handle(☰) 버튼으로 통합. 드래그 중 상/하단 삽입 위치 가이드라인(.drag-over-top, .drag-over-bottom)을 실시간 표시.

4. 1페이지 PTC 테이블 뷰 열 너비 드래그 리사이즈 버그 완벽 해결:

   * 원인: 기존에는 <col>과 <th>의 style.width만 변경하고 min-width/max-width 및 <td> 너비를 강제하지 않아, whitespace-nowrap이나 내부 콘텐츠 최소 너비 때문에 컬럼이 줄어들지 않았음. 또한 셀 포커스 시 renderPtcDocumentModeView()가 조기 반환(return)되는 문제가 있었음.

   * 조치: applyPtcTableColWidthsToDom()에서 동적 <style id="ptcDynamicColWidthStyle">를 통해 col:nth-child(n), th:nth-child(n), td:nth-child(n) 모두에 width, min-width, max-width를 !important로 즉시 동기화. 헤더의 .ptc-col-resizer 핸들뿐만 아니라 테이블 본문(<td>)의 우측 경계선(7px 이내) 어디서든 드래그하여 열 너비를 즉시 조절할 수 있도록 개선.

5. 1페이지 PTC 테이블 뷰를 4페이지(4. PTC 산출물)와 동일한 클린 11-Col 테이블로 개편:

   * buildIntegrityRows()를 사용해 4페이지 4. PTC 산출물과 100% 동일한 11개 표준 컬럼(ID, Project Variant, State, Test Case Name, Text, Pre Conditions, Test flow, Evaluation Criteria, Post Conditions, Test Case Comment, Test Environment) 및 깔끔한 배지/번호 매김 텍스트로 렌더링.

   * 원하는 셀을 클릭하면 해당 셀만 즉시 인라인 편집기(.ptc-inline-active-editor)로 전환되며, 포커스 해제(blur) 또는 Enter/Ctrl+Enter 입력 시 즉시 반영 후 깔끔한 4페이지 산출물 스타일로 복귀.

Phase 75 (v50.30) — ECU-TEST 내장 Python 자동 감지 기반 PTC 로컬 브릿지(ptc_local_bridge.py) 전환

1. 사용자 요청 사항

* PowerShell 파서 에러(and 토큰 등)를 근본적으로 방지하기 위해 PTC 브릿지를 Python 기반으로 전환

* ECU-TEST 설치 시 함께 설치되는 내장 Python(python.exe)을 브릿지 실행에 그대로 사용할 수 있는지 확인 및 적용

2. 기술 검토 및 구현 내역

3. ECU-TEST 내장 Python 사용 가능 여부 검증:

   * Tracetronic ECU-TEST(ecu.test 2021 \~ 2024.3+)는 Windows 설치 시 자체 임베디드 Python 3 인터프리터(<설치경로>\\Python\\python.exe 또는 <설치경로>\\python.exe)와 표준 라이브러리(http.server, subprocess, urllib.parse, json, shlex 등)를 기본 내장함.

   * 외부 pip 패키지 의존성 없이 100% Python 표준 라이브러리만으로 브릿지를 구성하면 망분리(Air-gapped) 오프라인 PC에서도 별도 Python 설치 없이 ECU-TEST 내장 Python만으로 즉시 실행 가능함.

4. Python PTC 로컬 브릿지(bridge/ptc_local_bridge.py & run_ptc_bridge.bat) 및 원클릭 실행 적용:

   * subprocess.run(args_list, shell=False) 배열 전달 방식을 적용하여 --queryDefinition=((field\[Document ID\]=...) and (field\[Category\]=Functional Test)) 실행 시 쉘 파서를 거치지 않고 im.exe에 직접 인자를 전달함으로써 특수문자·괄호·and 토큰 에러를 원천 차단.

   * C:\\Program Files\\ecu.test\*\\Python\\python.exe, C:\\Program Files\\Tracetronic\\ECU-TEST\*\\Python\\python.exe, %LOCALAPPDATA%\\ecu.test\*\\Python\\python.exe 경로를 1순위로 자동 탐색하고, 없을 경우 시스템 Python으로 폴백하는 자동 탐색 런처(🐍 Python 브릿지 복사 및 💾 Py 브릿지 (.bat) 다운로드)를 1. TC 에디터 및 7. Utility (Utility 4)에 탑재.

Phase 76 (v50.31) — 번들(.zip) 내 .bat 배치 파일 영구 제외 규칙 적용

1. 사용자 요청 사항

* 앞으로 .bat 파일은 절대 번들(.zip)에 포함시키지 말 것 (사내 보안/백신 정책 준수 및 불필요 파일 배제)

2. 조치 내역

* bridge/run_ptc_bridge.bat 삭제 및 번들 패키징 시 모든 \*.bat, \*\_halcyonic.html, \*.xlsx 파일이 절대 포함되지 않도록 영구 제외 필터 적용.

* 브릿지 파일 다운로드 버튼도 .bat 대신 순수 Python 스크립트(ptc_local_bridge.py)를 다운로드하도록 변경.

Phase 77 (v50.32) — 2. 신호 사전 BSW 등록 슬롯(SIL {signal}\_Phy / {signal}\_Swt 자동 Override), 미입력 HIL 경로 빈칸 유지, Admin User HTML 선택 페이지 Export

1. 사용자 요청 사항

* 2. 신호 사전에 BSW 등록칸 추가: BSW 신호를 올렸을 때 SIL 환경이면 {signal}\_Phy, {signal}\_Swt 오버라이드를 자동으로 등록

* 미입력 HIL 신호 경로 빈칸 유지 (더미값 채우기 금지): SIL에 대한 신호만 올리고 다른 HIL(HIL (ETAS) / HIL (dSPACE)) 신호가 없다면 더미값을 채워 넣지 않고 빈칸("")으로 유지

* Admin에서 User용 HTML Export 시 페이지 선택 기능: 평소에는 페이지 선택 버튼을 숨겨두고, Export 버튼을 눌렀을 때만 페이지 선택 버튼과 \[확인\] 버튼이 보이도록 하여 선택한 페이지만 포함된 HTML을 Export

2. 구현 내역

3. 2. 신호 사전 BSW 등록칸 및 탭 추가 + SIL {signal}\_Phy / {signal}\_Swt 자동 Override:

   * 좌측 파일 매니저(#loadedFilesManagerPanel)에 6. BSW 신호 카드(SIL / HIL:dSPACE / HIL:ETAS 파일 업로드 및 즉시 입력창)와 상단 책갈피 탭 ⚙️ BSW(#ctxBookmarkPanelBsw)를 추가.

   * BSW 신호를 SIL로 등록(파일 업로드, 빠른 입력, 수동 등록)하면 state.signalOverrideMap에 customOl: "{signal}\_Phy", customSwt: "{signal}\_Swt" (silOverridePath: "Plant model/{signal}\_Phy")가 자동 등록되며, .pkg 생성 시 SIL 환경에서 {signal}\_Phy와 {signal}\_Swt로 자동 매핑됨.

4. 타 환경(HIL) 미등록 신호 더미값 완전 제거 (빈칸 유지):

   * upsertSignals(), applyBswParsedSignals(), applyPlantModelParsedSignals(), parseOverrideCFileContent(), formAddSignal, renderSignalTable()에서 SIL 신호만 등록되었을 때 pathHilEtas 및 pathHilDspace에 기본 경로(defaultPath / s.path)를 복사하던 폴백 로직을 제거하고 빈칸("")으로 유지.

5. Admin User HTML Export 시 On-Demand 페이지 선택 UI (#bakedExportPageSelectorBox):

   * 좌측 사이드바의 \[User HTML Export\] 또는 \[Utility HTML 추출\] 버튼을 클릭했을 때만 페이지 선택 토글 목록(1. TC 에디터 \~ 8. To-Do·현황)과 \[확인\] / \[취소\] 버튼이 나타나며, \[확인\] 클릭 시 선택된 페이지의 탭과 <section>만 남기고 번호를 자동 재정렬하여 단일 HTML로 내보냄.
     Phase 78 (v50.33) — Page 1 Nav Export Block (.xlsx & .pkg)

* Added a dedicated Export block (#editorNavExportBlock) in Page 1 (1. TC 에디터) Left Sub-Nav (#leftEditorSubSidebar) with .xlsx (#btnNavEditorExportXlsx) and .pkg (#btnNavEditorExportPkg) buttons.

* Wired #btnNavEditorExportXlsx to the exact same 11-Col Excel export (exportPage4IntegrityXlsx / PTC_Integrity_TestCases_11Col.xlsx) used in Page 4 (4. PTC 산출물), and #btnNavEditorExportPkg to the exact same downloadStagePkgForSelectedTcs(5, false) export used in Page 5 (5. PKG 변환).
  Phase 79 (v50.34) — Green .xlsx Export Button in Page 1 Nav & Unified Page 4 "4. 설정 및 가이드" with Export-Scoped Usage Guides/Templates

* Changed Page 1 (1. TC 에디터) Left Sub-Nav Export .xlsx button (#btnNavEditorExportXlsx) to emerald green (bg-emerald-600 hover:bg-emerald-500).

* Consolidated Page 4 (PTC 산출물) and Page 5 (PKG 변환) into a unified 4. 설정 및 가이드 (#view-ecutest) page and renumbered subsequent tabs (5. TA Editor, 6. Utility, 7. To-Do & 현황).

* Added a unified Settings & Previews section (PTC 11-Col format options/preview + PKG target environment, Override/Swt, tsRead Wait/Tolerance, TC selector, package structure tree, and XML preview), a Templates & Python Bridge Hub, and Page-by-Page Usage Guides tagged with data-export-page and data-export-scope so exported User/Utility HTML files automatically include only the guides and templates matching the selected pages.
  Phase 80 (v50.35) — Sidebar Swap (3. Guide / 4. 문법 & 정규화 규칙) & 2-Tier Bookmark Guide Architecture (No Sub-Nav)

* Swapped Page 3 and Page 4 in the sidebar (#nav) and export page selector (#bakedExportPageBtnList), renaming the page to 3. Guide and placing 4. 문법 & 정규화 규칙 at #4.

* Removed the Left Sub-Nav from 3. Guide (#view-ecutest) and redesigned it with a 2-Tier Bookmark (2단 책갈피) layout:

  * 1단 (상위) 책갈피: TC 에디터 (data-guide-top-tab="EDITOR", data-export-page="editor") and 신호 사전 (data-guide-top-tab="SIGNALS", data-export-page="signals").

  * 2단 (하위) 책갈피: 설정 (data-guide-sub-tab="SETTINGS") and 템플릿 & 브릿지 (data-guide-sub-tab="TEMPLATES").
    Phase 81 (v50.36) — Guide Bridge Removal, 3-Column Expandable Examples Tab (Standard Pre/Post Combined Pkg Export & Helper<->ASW), and Full Grammar Rules CSS Grid

* Removed PTC Bridge controls from 3. Guide (#view-ecutest) and renamed the 2nd-tier bookmark tab to 템플릿.

* Added 예제 (data-guide-sub-tab="EXAMPLES") and 문법 규칙 (data-guide-sub-tab="GRAMMARS") under Guide > 1단: TC 에디터:

  * 문법 규칙 탭: Implemented a responsive CSS Grid of 4 deep-dive syntax cards (Token Arguments, adding tsRead Tolerance +-/±, adding Wait until True vs Multi-Check conditions, and into variable saving) + Full Grammar Rules CSS Grid cards with category filters and 1-click copy.

  * 예제 탭: Implemented an expandable 3-column TC authoring table (1열: 요구사항, 2열: Test Flow (#cond), 3열: Evaluation Criteria (#crit)) with + 행 추가 (2행, 3행...), Helper ↔ ASW 변환 (with L2/L4 switch), and a top-right Pkg Export button (#btnGuideHeaderPkgExport / #btnGuideExPkgExport) that combines Standard Preconditions and PostConditions with each authored TC into .pkg XML.
    Phase 82 (v50.37) — Signal Dictionary Sub-Hierarchy (Helper under A2L & 3-Way Split Override under A2L / DBC / BSW with Independent Prefix & Postfix Rules)

* Moved Helper (L2·L4) inside 1. A2L (.a2l) as a nested sub-section in 2. 신호 사전 Left Sub-Nav (#loadedFilesManagerPanel).

* Split Override into 3 dedicated sub-sections with independent Prefix and Postfix rules:

  1. A2L Override (1. A2L 하위): SIL-only (SIL_ONLY), user-selectable Override 적용 and Swt 적용 checkboxes, custom OL Prefix/Postfix and Swt Prefix/Postfix, Excel (.xlsx) mapping loader.

  2. DBC Override (2. DBC 하위): Shared across SIL & HIL (SIL_HIL), automatically maps Rx messages based on reference {Node} upon .dbc upload, custom OL Prefix/Postfix and Swt Prefix/Postfix.

  3. BSW Override (4. BSW 신호 하위): SIL-only (SIL_ONLY), Override and Swt are always enabled (상시 ON), custom OL Prefix/Postfix and Swt Prefix/Postfix, Excel (.xlsx) mapping loader.
     Phase 83 (v50.38) — Unified Signal & Override Dictionary Table & Exclusive Override Settings in Guide > 신호 사전 > 설정

* Unified the Signal Dictionary table and Override Dictionary table in 2. 신호 사전 (#view-signals) into a single integrated 통합 신호 & Override 사전 table (#signalDictTableContainer) with multi-facet classification tabs (전체, A2L, DBC, Plant model, BSW, Override 모아보기) and filters (타입, 매핑(Override 전체/A2L/DBC Rx/BSW/Helper/미매핑), 환경(SIL/ETAS/dSPACE), System, and search across signal/Helper/OL/Swt names).

* Restricted 2. 신호 사전 Left Sub-Nav (#loadedFilesManagerPanel) strictly to file loading only (A2L + Helper + A2L Override Excel, DBC + Rx Auto status, Plant model, BSW + BSW Override Excel) and consolidated all Override & Signal settings (Override/Swt 적용, A2L/DBC/BSW OL·Swt Prefix/Postfix, A2L ECU-KEY, DBC 기준 {Node}, MODEL-KEY, Swt 인가값) exclusively inside 3. Guide > 신호 사전 > 설정 (#guidePane_SIGNALS_SETTINGS).
  Phase 84 (v50.39) — PTC Table View Autocomplete, Clean Text Alignment in Signal Dict, .m/.xam Sample Downloads & SIL Auto-Path, 5. Override Block, and A2L_1/A2L_2/DBC Rules

* Added live floating Autocomplete (#cond / #crit Grammar & Signal autocomplete and Pre/Post Condition phrase autocomplete) inside 1. TC 에디터's PTC 테이블 뷰 inline cell editor.

* Removed ├ and └ box-drawing characters across 2. 신호 사전 and replaced them with aligned text badges and structured cards.

* Removed 4. BSW 신호 and created a dedicated 5. Override block in 2. 신호 사전 Left Sub-Nav for loading A2L_1 and A2L_2 Override Excel files (MODEL-KEY = Plant model).

* Updated Override rules in 3. Guide > 신호 사전 > 설정: separated 1. A2L (A2L ECU-KEY) from 2. Override 설정 (MODEL-KEY = Plant model), and applied {OL_Tag}{Prefix}{Signal}{Postfix} / {Swt_Tag}{Prefix}{Signal}{Postfix} to A2L_1 and A2L_2 while keeping DBC Override unchanged.

* Fixed .dict-bookmark-tab.hidden CSS specificity so 예제 and 문법 규칙 bookmarks are strictly hidden when 신호 사전 is selected in 3. Guide.

* Replaced Plant sample load in Guide > 신호 사전 > 템플릿 with .m 샘플 다운로드 and .xam 샘플 다운로드, and updated .m file parsing so only signal names on each line are extracted, leaving general/HIL paths blank ("") and mapping only SIL to Plant model/{signal}.
  Phase 85 (v50.40) — Fix Runtime Error & Body-Portal Fixed Autocomplete in PTC Table View

* Resolved ReferenceError: bindCfgInput is not defined inside initServerlessWorkspaceAndAdminSync that interrupted initialization.

* Upgraded openInlineCellEditor in 1. TC 에디터 PTC 테이블 뷰 to mount #ptcPortalInlineAcBox directly on document.body (position: fixed !important; z-index: 99999 !important;) so the autocomplete dropdown is never clipped by <td> overflow: hidden !important or #ptcExcelGridScrollWrap, triggers immediately on cell click/focus/input/keyup, and supports keyboard (↑/↓/Enter/Tab/Esc) and mouse selection without premature cell blur.
  v50.41 (2026-11-13)

* 1페이지 (1. TC 에디터) PKG 실행 순서 위치 이동 및 개별 접기/열기 토글 추가:

  * PKG 실행 순서 (#unifiedPrePostPkgOrderContainer)를 Export 미리보기 (#editorPtcPreviewContainer) 내부 최상단으로 이동하여 Export 미리보기 접기 시 함께 접히도록 통합.

  * Export 미리보기가 열려 있을 때 PKG 실행 순서만 독립적으로 접거나 열 수 있는 토글 버튼(#btnTogglePkgExecOrder 및 좌측 Sub-Nav #btnNavTogglePkgExecOrder) 추가.

* 2페이지 (2. 신호 사전) 책갈피 전환 시 세부 필터 레이아웃 통일 & 샘플 추가 버튼 제거:

  * 상단 헤더의 + 샘플 추가 버튼(#btnLoadSampleA2lDbc) 제거.

  * 전체, A2L, DBC, Plant model, Override 모아보기 책갈피 전환 시 세부 필터 바로 인해 상단 높이가 달라지던 문제를 해결하기 위해 세부 필터 열기/접기 토글(#btnToggleSigSubFilter / #btnNavToggleSigSubFilter, 기본값 접기)을 도입하고, 통합 검색·필터 바(#sigFilterTypeSelect)에 DBC Rx (수신·Override) 및 DBC Tx (송신) 옵션을 직접 통합.

* 전체 페이지 미리보기·접기/열기 상태 영구 저장 (localStorage & Baked HTML):

  * 모든 페이지의 미리보기 및 섹션 열기/접기 상태(showEditorPtcPreview, showEditorPkgExecOrder, showValidationTable, showTcOverviewList, editorPtcDocViewMode, showSignalDictTable, showSigBookmarkSubFilter, showIntegrityPreview, showPkgTcList, showPkgStructureTree, showPkgCodePreview, showTaPlotPreview, showTaPairTable, showTaStructureTree, showTaXmlPreview, showUtil1Preview\~showUtil4Preview, showGrammarPrePostList, showGrammarPkgMapTable, showGrammarDslTable, showGrammarNormBox 등)를 토글 즉시 저장하고 HTML 재실행 시 동일하게 복원.

* 3페이지 (3. Guide > TC 에디터 > 설정) Global tsRead & Multi-Check 설정 추가:

  * tsRead(단일 신호 검증) 및 Multi-Check(Wait until below all conditions are met)의 Time Option(Wait until / Immediate), Timeout (ms), Tolerance 적용 여부, 기본 Tolerance (±), Multi-Check 결합 조건 (AND/OR)을 전역(Global)으로 설정하고 .pkg XML 생성 시 자동 반영.
    v50.42 (2026-11-14)

* 2페이지 (2. 신호 사전) 세부 필터 버튼 겹침 해결:

  * 세부 필터 토글 버튼(#btnToggleSigSubFilter)을 검색 입력칸 내부에서 상단 책갈피 탭 바(.dict-bookmark-bar 우측)로 이동하고, #signalDictSearchFilterBar의 모든 그리드 셀에 min-w-0을 적용하여 검색 입력창(#sigSearchInput)과 타입 선택기(#sigFilterTypeSelect)가 절대 겹치지 않도록 수정.

* Wait until below all conditions are met 포함 TC의 자동 Trace Analysis (\*.ta & <TRACE-ANALYSES>) 생성:

  * TC(#condN)에 Wait until below all conditions are met 블록이 존재하면 하위 조건들이 모두 만족(and 결합: device_\_{sig1} == {val1} and device_\_{sig2} == {val2})하는 조건을 TriggerBlock의 <START-CONDITION>으로 자동 설정.

  * 해당 #condN과 매칭되는 #critN의 검증 문구(예: Check if {signal} == {Value})들을 TriggerBlock 하위의 Calculation (<ANALYSISITEM format-rev="1" xsi:type="calculation">, <NAME>Check if {signal} == {Value}</NAME>, <FORMULA>device_\_{signal} == {Value}</FORMULA>) 스텝으로 자동 생성하여 5. TA Editor(state.taPackages), 1페이지 Export 블록(Auto .ta), Export 미리보기 배너, 그리고 .pkg XML 내 <TRACE-ANALYSES>에 동시 반영.
    v50.43 (2026-11-14)

* Tracetronic 공식 문서 기반 Auto-TA 및 Multi-Check 검증·고도화:

  * Wait until below all conditions 및 #crit에 == {Value} +- {Tol} 오차가 지정된 경우, TA 수식에서 abs(device_\_{Signal} - {Value}) <= {Tol}로 자동 변환하여 부동소수점 파형에서도 정확한 Trigger/Calculation 판정이 이루어지도록 개선.

  * 3. Guide > TC 에디터 > 설정의 Multi-Check 및 tsRead 전역 옵션에 Tracetronic 공식 Fulfilled for 3종(every test step, at least one test step, every test step at least once)과 Time Options 5종(Wait until true, True for at least, True for at least … within …, Only synchronization, Immediate) 반영.
       v50.44 (2026-11-14)

* Package(.pkg) 생성 시 Trace Analysis(TA) 포함 여부 확인 모달 및 동반 출력 지원:

  * .pkg Export 버튼(1. TC 에디터 좌측 Nav .pkg, 3. Guide > 설정 \*.pkg 다운로드, 3. Guide > 예제 Pkg Export) 클릭 시 **#pkgIncludeTaConfirmModal**을 통해 TA 포함하여 생성 / TA 제외 (.pkg만) / 취소 여부를 사용자에게 확인.

  * TA 포함하여 생성 선택 시 <TRACE-ANALYSES> 블록(Wait until below all conditions 자동 생성 TA 또는 5. TA Editor 활성 TA)을 .pkg 내부에 함께 포함하여 생성하며, TA 제외 선택 시 순수 Test Case .pkg만 생성.
    v50.45 (2026-11-14)

* TA 생성 시 현재 Pkg에 매핑된 모든 신호 자동 이관 및 Plot 자동 생성:

  * collectPkgMappedSignalsForTa(tc)를 통해 현재 .pkg의 <MAPPING>에 등록되는 모든 신호(Write/Override, Read, Check if, Signal read 포함)를 수집하여 TA(MAPPING-ITEM ↔ VIRTUAL-SIGNAL 1:1 Pair)로 전부 이관.

  * 자동 생성되는 TA(Wait until 자동 TA 및 .pkg 생성 시 TA 포함 선택)와 5. TA Editor의 \[현재 TC 신호 가져오기\] 실행 시 모든 매핑 신호를 포함한 Plot (<ANALYSISITEM xsi:type="plotItem">) 스텝을 Episode에 자동 생성하여 즉시 파형으로 확인 가능하도록 개선.
    v50.46 (2026-11-14)

* Pre/Post 관리 UI 간소화 및 매핑 상태 색상 직관화:

  * Pre/Post 관리 각 항목 문구 하단에 별도로 붙어 있던 매핑 .pkg 상태 입력줄(.preset-pkg-status-input)을 제거하여 1줄 컴팩트 행으로 정리.

  * 통합 Package 매핑에 연결된 .pkg가 존재하는 경우 문구 입력칸(.preset-phrase-input) 자체를 기존 매핑 pkg와 동일한 초록색(.pkg-registered)으로 표시하고, 미매핑 문구는 기본 색상을 그대로 유지(호버 툴팁으로 매핑된 .pkg 파일명 확인 가능).
    v50.47 (2026-11-14)

* Multi-Check 3종 문법 확장 + 인라인 Timeout 문법(within {TIME} {UNIT}) + Guide 업데이트:

  * Wait until below all conditions are met → TsMultiCheck (every test step, MATCHALL=True)

  * Wait until one of below conditions are met → TsMultiCheck (at least one test step, MATCHALL=False, Auto-TA or 트리거 결합)

  * Wait until below all conditions are met at least once → TsMultiCheck (every test step at least once, FULFILLED-AT-LEAST-ONCE=True)

  * 문법 끝에 within {TIME} {UNIT}(예: within 500 ms, within 2 s)를 추가하여 개별 Multi-Check 및 단일 Check if의 Timeout을 인라인으로 지정할 수 있도록 구현하고, 3. Guide > TC 에디터 > 문법 규칙 카드 및 자동완성 문법 테이블을 함께 업데이트.
    v50.48 (2026-11-14)

* Auto-TA Calculation 판정 모드 선택 옵션 (Fulfilled everywhere / Fulfilled at least once) 추가:

  * 3. Guide > TC 에디터 > 설정 (#selGlobalTaCalcMode) 및 1. TC 에디터 > Export 미리보기 Auto-TA 배너(#selPreviewTaCalcMode)에서 Fulfilled everywhere (always)와 Fulfilled at least once (once)를 선택·동기화할 수 있도록 구현.

  * 선택된 판정 모드는 .ta 및 .pkg <TRACE-ANALYSES> 내 <ANALYSISITEM xsi:type="calculation">의 <EXPECTATION-MODE xsi:type="string">always|once</EXPECTATION-MODE>로 반영되며 localStorage/Baked HTML에 영구 저장됨.
    v50.49 (2026-11-14)

* Auto-TA 기본 설정을 권장해법 2번(Fulfilled at least once + with time offset 0.0s \~ +0.05s)으로 적용:

  * state.taCalcExpectationMode 기본값을 once (Fulfilled at least once)로 변경하여 1-cycle/Rising Edge 조건도 놓치지 않도록 기본 설정.

  * TriggerBlock 기본 모드를 start trigger with time offsets (Start offset = 0.0s, Stop offset = 0.05s)로 설정하고 3. Guide > TC 에디터 > 설정에서 언제든 변경 가능하도록 UI 추가.
    v50.50 (2026-11-14)

* Auto-TA 사용 시 #crit 스텝을 Incorporate trace step result (TsTraceStepResult)로 자동 변환:

  * .pkg 생성 시 Auto-TA(Wait until 기반 <TRACE-ANALYSES>)가 함께 포함되는 경우, #crit 섹션의 Check if 검증 스텝들을 온라인 tsRead 대신 Incorporate trace step result (TsTraceStepResult)로 자동 변환.

  * 각 #crit 스텝의 <TRACE-STEP-ID>가 <TRACE-ANALYSES> 내 매칭되는 Calculation 스텝의 uuid와 1:1로 정확히 연결되며, TA를 제외하고 .pkg만 생성할 때는 기존처럼 tsRead로 출력됨.
    v50.51 (2026-11-14)

* 1페이지 (1. TC 에디터) Auto-TA 미리보기 접기/열기 토글 추가:

  * Export 미리보기 상단 바(#btnToggleEditorAutoTa) 및 좌측 Sub-Nav(#btnNavToggleEditorAutoTa)에 Auto-TA 접기/열기 버튼을 추가하고 state.showEditorAutoTa 상태를 localStorage 및 Baked HTML에 영구 저장.

* 1페이지 (1. TC 에디터) TC 복제 버튼 추가: Test Suite Overview 상단에 복제 버튼(#btnDuplicateTestCase)을 추가하여 현재 선택된 Test Case의 모든 필드·스크립트를 즉시 복제({Title}\_Copy)하도록 구현.
  v50.52 (2026-11-14)

* 4. 문법 & 정규화 규칙 (#view-grammars) 1단 책갈피 개편:

  * 좌측 규칙 메뉴 및 섹션별 접기/펴기 버튼(#grammarLeftSubNav, #btnNavToggleGrammarPrePost, #btnNavToggleGrammarPkgTable, #btnNavToggleGrammarDslTable)을 제거하고, 3. 가이드와 동일한 1단 책갈피 포맷(#grammarBookmarkBar — 1) Pre/Post 관리, 2) 통합 Package 매핑·정규화, 3) 문법 규칙)으로 전환.

  * 선택된 책갈피 상태(state.adminGrammarTab)를 localStorage 및 내보내기 HTML에 유지.
    v50.53 (2026-11-14)

* 6. Utility (#view-utility) 1단·2단 책갈피 포맷 개편:

  * 좌측 서브 메뉴(#utilLeftSubNav, #utilMainGrid)를 제거하고, 상단 1단 책갈피(#utilTier1BookmarkBar — Utility 1 · Utility 2 · Utility 3 · Utility 4)와 Utility 1 내부 2단 책갈피(#util1Tier2BookmarkBar — 1.1 배열 평면화 & BVA/EP · 1.2 2-Pairwise TC 생성기) 구조로 전환.

  * 각 Utility의 파일 로더(A2L/ASW Excel, Helper 3-Excel, Text/XML Split, PTC 브릿지)를 해당 탭 상단 툴바로 배치하고 선택된 책갈피 상태(state.utilTopTab, state.util1SubTab)를 유지.
    v50.54 (2026-11-14)

* 1. TC 에디터 좌측 Nav 미리보기 목록 정리:

  * 좌측 Nav(#leftEditorSubSidebar)의 미리보기·렌더링 열기/접기 목록에서 1-1) PKG 실행 순서와 1-2) Auto-TA 미리보기 토글 버튼을 제거하고, 메인 영역 내부의 접기/펴기 버튼(#btnTogglePkgExecOrder, #btnToggleEditorAutoTa)은 그대로 유지.
    v50.55 (2026-11-14)

* 1. TC 에디터 1단 책갈피 탭 개편 (#editorViewBookmarkBar):

  * 1페이지 메인 에디터 영역을 1. Form view, 2. PTC view, 3. Review Table 3개 책갈피 탭으로 분리.

  * 기존 하단에 위치하던 검증 테이블(#validationTableContainer, #activeTcValidationTopBanner)을 3. Review Table 탭 내부로 이동.
    v50.56 (2026-11-15)

* 신호 기반 동적 지연/유지 검증 문법 및 Auto-TA 적용:

  * GRAM_CHECK_AFTER_SIGNAL: Check if {SIGNAL} {OP} {VALUE} after {DELAY_SIGNAL} ms → Auto-TA Value(device__D, StartTriggerValue(device__F) / 1000.0) {OP} {VALUE}

  * GRAM_CHECK_FOR_SIGNAL: Check if {SIGNAL} {OP} {VALUE} for {DURATION_SIGNAL} ms → Auto-TA Always(device__D {OP} {VALUE}, StartTriggerValue(device__F) / 1000.0)

  * 지연/유지 기준 신호(F)를 <MAPPING>, <TRACE-ANALYSES>, Plot에 자동 포함하고 #crit 스텝을 TsTraceStepResult와 1:1 UUID 매칭.
    v50.57 (2026-11-15)

* Cond 트리거 연계형 동적 지연/유지 문법으로 개선:

  * GRAM_CHECK_AFTER_SIGNAL: After trigger + {DELAY_SIGNAL} ms, check if {SIGNAL} {OP} {VALUE} → Auto-TA Value(device__D, StartTriggerValue(device__F) / 1000.0) {OP} {VALUE}

  * GRAM_CHECK_FOR_SIGNAL: From trigger for {DURATION_SIGNAL} ms, check if {SIGNAL} {OP} {VALUE} → Auto-TA Always(device__D {OP} {VALUE}, StartTriggerValue(device__F) / 1000.0)
    v50.58 (2026-11-15)

* 비(非) Auto-TA .pkg 변환 시 Wait until ↔ Crit 변수 캡처·비교 로직 구현:

  * .pkg 변환 시 Auto-TA를 선택하지 않은 경우(!options.includeTa), 직전 Wait until(Multi-Check) 블록 내부에 후속 #crit 신호들의 Read {signal} Into {varName} (TsRead + SAVE-IN) 스텝을 자동 삽입.

  * #crit 단계에서는 캡처된 {varName}과 원래 #crit의 {op} {VALUE}(오차 +- tol 포함)를 비교하는 TsCalculation 스텝을 자동 생성.
    v50.59 (2026-11-15)

* Guide > 예제 (DEFAULT_GUIDE_EXAMPLE_ROWS) Wait until 예제 2종 갱신:

  * 예제 1: Wait until below all conditions are met within 500 ms + After trigger + DelayTimeMs ms, check if AEB_ActiveFlag == 1

  * 예제 2: Wait until one of below conditions are met within 1 s + From trigger for HoldTimeMs ms, check if AEB_ActiveFlag == 1
    v50.60 (2026-11-15)

* 1. TC 에디터 상단 중복 뷰 전환 버튼 제거:

  * 책갈피 탭(1. Form view / 2. PTC view / 3. Review Table)과 중복되던 상단 #btnTogglePtcDocViewMode(PTC 테이블 뷰 / 폼 에디터 뷰) 버튼 및 관련 className 덮어쓰기 코드를 완전히 제거.
    v50.61 (2026-11-15)

* Guide > TC 에디터: Auto-TA 및 오른쪽 정렬 Lab 책갈피 탭 추가:

  * Auto-TA 탭(EDITOR:AUTO_TA): Auto-TA 포함/미포함 동작 원리 및 기본/지연(After trigger + F ms)/유지(From trigger for F ms) 3종 예시 수록.

  * Lab 탭(EDITOR:LAB, margin-left: auto로 오른쪽 끝 정렬): utility-\* 임시 xsi:type 14종 스텝을 한 번에 테스트할 수 있는 단일 TC 예제 및 .pkg 즉시 다운로드 기능 수납.

* Auto-TA 팝업(#pkgIncludeTaConfirmModal) 가림/잘림 수정: 최상위 z-index: 2147483647 및 뷰포트 내 스크롤(max-height: calc(100vh - 2rem)) 강제 적용.
  v50.62 (2026-11-15)

* ENG 버전 한글 → 영어 번역 사전 대폭 보강 (STUDIO_I18N_DICT):

  * v50.30v50.61 사이에 추가된 모든 UI 문구(책갈피 탭, Guide Auto-TA/Lab, Utility 14, PKG + TA 팝업, Review Table, PTC 11-Col 뷰, Override 설정 등 480여 개 항목)를 STUDIO_I18N_DICT에 추가하여 ENG 전환 시 한글 잔여 문구를 제거.
    v50.63 (2026-11-15)

* 5. Override A2L_3 (.c 파일 / 폴더 스캔) 복구 및 연동:

  * 2. 신호 사전 좌측 5. Override 패널에 A2L_3 (C Override) 서브 카드를 추가하여 \*\_Override.c/.h 파일 직접 선택(#inputImportOverrideCFiles) 및 폴더 일괄 스캔(#inputScanOverrideFolder) UI를 복구.

  * C_OVERRIDE 전용 파일 목록(#loadedFileListA2l3C)·카운트 배지(#badgeLoadedFileCntA2l3C)·비우기 버튼(#btnClearA2l3COverrideNav) 및 ENG 번역 추가.
    v50.64 (2026-11-15)

* ECU-TEST 2024.3 검증된 TestStep xsi:type UUID 및 XML 스키마 일괄 반영:

  * Repeat until (GRAM_REPEAT_UNTIL / TsRepeatUntil) 제거 (2024.3 미지원).

  * TsSwitchCase, TsWaitForUser(<INFO-TEST> 사용, format-rev 제거), TsAddTrace(format-rev="2", <NAME/> 및 <PATH format-rev="2"> 필수), TsStartStimulus, TsStopStimulus, TsAnalysisJob, TsRequestAnalysis, TsTodo, TsTraceStepResult(Auto-TA #crit 포함), TsExit, TsReturn의 실제 2024.3 UUID 적용.

  * Guide > TC 에디터 > Lab에 전체 TestStep UUID 레퍼런스 표 수납.
    v50.65 (2026-11-15)

* ECU-TEST 2024.3 실제 .pkg XML 스키마 정밀 보정 (첨부 .pkg 캡처 기준):

  * TsWaitForUser: <INFO-TEXT format-rev="2"> 적용.

  * TsAddTrace: utility-0f50a0f0-e269-11df-a984-001143176b04 (단일 하이픈) 보정.

  * TsStartStimulus: format-rev="4", <PATH format-rev="2">, <INSTANCE-NAME>, <STIMULI-ASSIGNMENT/>, <VARIABLE-ASSIGNMENT/> 적용.

  * TsStopStimulus: format-rev="2", <INSTANCE-NAME> 적용.

  * TsAnalysisJob: format-rev="2", <TRACE-ANALYSIS>, <UPDATE-FROM-ANALYSIS-RESULT> 적용.

  * TsRequestAnalysis: format-rev 제거, <REQUESTED-ANALYSIS> 적용.

  * TsTodo: format-rev 제거, <TODO> 적용.

  * TsTraceStepResult: format-rev 제거, <TRACE-STEP-REF> 적용 (Auto-TA #crit 포함).

  * TsExit: format-rev="1" 적용 / TsReturn: utility-4f3c5500-f0f5-11dc-b88f-001b24fa84be 적용.
    v50.66 (2026-11-15)

* TA / Auto-TA .pkg XML 스키마 정합성 수정 (첨부 캡처 반영):

  * <START-CONDITION xsi:type="string">... 및 <STOP-CONDITION xsi:type="string"/> 적용, <TRIGGER-MODE> 태그 제거, <TRIGGER-START-OFFSET>/<TRIGGER-STOP-OFFSET>의 unaryOpBaseExpression에서 format-rev="1" 제거.

  * <VIRTUAL-SIGNAL> 내부에 <SIGNAL-FOR-ANALYSIS xsi:type="recordingSignalForAnalysis"> (<KEY>, <SOURCE-TYPE>RECORDING-GROUP</SOURCE-TYPE>, <SOURCE-REF>uuid</SOURCE-REF>) 적용 및 신호명에서 device///device_\_ 접두사 제거.

* SIL 환경 A2L Set Override 조건 보정: Override 매핑(state.signalOverrideMap)에 등록된 신호만 OL/Swt로 변환하고, 미등록 A2L 신호는 원본 신호 그대로 tsWrite 수행.

* TA 제외 시 Multi-Check 변수 저장 버그 수정: buildTsReadXmlStep에서 isInsideMultiCheck일 때 varNameToSave가 빈 문자열로 강제 초기화되던 코드를 수정하여 <VARIABLE-REFS>가 정상 생성되도록 해결.

* 1. TC 에디터 .pkg (현재 TC) / All .pkg (전체 TC) 버튼 분리: .pkg 버튼은 현재 보고 있는 활성 TC 1건만 내보내고, All .pkg 버튼(#btnNavEditorExportAllPkg)은 전체 TC를 일괄 내보내도록 추가.
     v1.0.4 (2026-11-19)

* 7·8. 통합(1창) ↔ 분리(2창) 에디터 선택 토글 추가:

  * 1페이지 Form view 7·8. 툴바에 통합 / 분리 선택 버튼(#editorScriptModeGroup: #btnScriptModeUnified, #btnScriptModeSplit)을 추가하고 localStorage(state.editorSplitScriptMode)에 사용자 선택을 영속 저장.

  * 통합(1창) 모드에서는 #tcScriptInput 1개 창에서 #cond1 → #crit1 → #cond2 → #crit2 순으로 편집하고, 분리(2창) 모드에서는 좌측 7. Test Flow (#tcScriptInput)와 우측 8. Evaluation Criteria (#tcCritInput) 2열 그리드로 분리 편집(각 창 독립 자동완성 드롭다운 및 + #cond/crit 동시 추가 지원).

* Sidebar / 좌측 Nav 폭 축소 및 Main 작업 영역 확장:

  * #sidebar 폭을 146px → 120px로 축소(padding: 0.5rem 0.24rem), <main> 좌우 패딩을 0.6rem으로 슬림화.

  * 데스크톱(min-width: 1024px) #editorMainGrid / #sigDictMainGrid 좌측 Nav 컬럼을 248px → 204px, 그리드 gap을 1.15rem → 0.55rem으로 줄여 확보된 약 100\~113px 폭을 우측 Main 에디터 영역(minmax(0, 1fr))에 직접 환원.
    v1.0.5 (2026-11-19)

* 1. TC Editor 하단 문법 설명 패널 교체 (즐겨찾기 연동):

  * 7·8. Test Flow / Evaluation Criteria 아래쪽의 기존 문법 선택 / + 라인 추가 빌더를 제거하고, 3. 가이드 → 문법 규칙에서 즐겨찾기(★)로 선택한 문법만 표시하는 ★ 즐겨찾기 문법 설명 패널(#editorFavoriteGrammarGuideCard)로 교체.

  * 문법 이름은 생략하고 패턴과 지원 기능 태그(+-, within, into) 및 설명을 직관적으로 표시 (예: Check if {SIGNAL} {OP} {VALUE} (+-, within, into)).

* 문법 규칙 정리 및 Ensure {Package} Call Package 연결:

  * Ensure that, 인가, 검증 문법 규칙을 기본 목록 및 기존 저장 상태 마이그레이션에서 제거.

  * Ensure 문법을 Ensure {Package} (CALL_PACKAGE)로 변경하여 Call package와 동일하게 서브 패키지 호출로 연결하고, 에디터에서 Ensure  입력 시 등록된 패키지 목록이 자동완성(Package 자동완성)되도록 구현.

* 문법 규칙 즐겨찾기(★) 기능 추가:

  * 3. 가이드 → 문법 규칙 각 카드에 ★ / ☆ 즐겨찾기 토글 버튼을 추가하고 localStorage(state.favoriteGrammarIds)에 영속 저장.

* .pkg Export MAPPING-ITEM 중복 등록 방지:

  * 한 TC 내에서 동일한 Package 또는 동일한 Signal이 여러 번 호출·참조되더라도 allocatePackageMappingPlan 및 <MAPPING> 생성 시 정규화 경로/ID 기준으로 중복을 제거하여 <MAPPING-ITEM>에 1회만 등록되도록 수정.
    v1.0.6 (2026-11-20)

* 3. 가이드 → 문법 규칙 패턴 + 지원 기능 표시:

  * 각 문법 규칙 카드의 패턴 영역에 지원 기능 태그를 함께 표시 (예: Check if {SIGNAL} {OP} {VALUE} (+-, within, into)).

* 1. TC Editor 하단 문법 설명 드롭다운 선택형 개선:

  * 7·8. 아래쪽 즐겨찾기 문법 패널을 드롭다운(#editorFavGrammarSelect) 선택형으로 변경해, 즐겨찾기(★)된 패턴 중 원하는 항목을 고르면 패턴·지원 기능·설명과 사용 예제(복사 버튼 포함)를 한눈에 확인 가능.

* 자동완성 {SIGNAL} vs {Package} 인자별 엄격한 필터링:

  * getGrammarPackagePrefixes() / getGrammarSignalPrefixes()를 분리하여 다음 인자가 {Package}인 문법(Ensure , Call package  등)에서는 패키지만 추천하고, {SIGNAL}인 문법(Set , Check if , Wait until , After trigger + ... check if  등)에서는 신호만 추천하도록 필터링 강화.

* A2L CURVE / MAP 구분 및 신호사전 매핑:

  * parseA2lContent에서 CHARACTERISTIC 타입(CURVE, MAP, CUBOID, VAL_BLK)·AXIS_DESCR 개수·MATRIX_DIM을 기준으로 CURVE(1D xaMeasVectorVariable)와 MAP(2D xaMeasMatrixVariable)을 정확히 판별해 a2lKind / a2lBlockType으로 저장하고, 2. 신호 사전 테이블에 CURVE / MAP 배지로 표시.
    v1.0.7 (2026-11-20)

* 동적 신호 인덱스 Map(GetValue) / Curve(Interpolate) tsRead 자동 생성 및 동일 폴링 주기(Same-Polling) 평가 구현:

  * Check if Cal_Matrix\[signal_A\]\[signal_B\] == {VALUE}, Wait until signal_Curve\[signal_C\] == {VALUE}, Read Cal_Matrix\[signal_A\]\[signal_B\] Into {VAR} 등 대괄호 내부에 신호명/변수명이 들어간 동적 인덱스를 파싱 지원.

  * 2D Map은 {var}.GetValue(arg1, arg2), 1D Curve는 {var}.Interpolate(arg1)로 자동 판별.

  * 동일 폴링 주기 해결: 캘리브레이션 Map/Curve는 사전 1회 TsRead로 변수화하고, 동적 인덱스 신호(signal_A, signal_B 등)의 TsRead(Evaluation OFF)와 TsCalculation(GetValue/Interpolate 평가)을 하나의 TsMultiCheck 내부에 배치하여 매 폴링 주기마다 최신 인덱스 신호와 계산 기대값을 함께 평가하도록 .pkg XML 생성.

  * 베이스 Map/Curve와 인덱스 신호 모두 <MAPPING-ITEM>에 중복 없이 1회씩 자동 등록.
    v1.0.8 (2026-11-20)

* Ensure {PACKAGE} 자동완성 버그 수정 (Form view & PTC view 공통):

  * updateSignalAutocompleteFromEditor 내부에 ctx.mode === "PACKAGE" 분기가 누락되어 Ensure  입력 시 {SIGNAL} 추천으로 폴백되던 문제를 수정.

  * 공통 헬퍼 collectPackageAutocompleteCandidates(q)를 추가하여 Form view(#tcScriptInput / #tcCritInput)와 PTC view 인라인 셀 에디터 모두에서 {PACKAGE} 인자 위치일 때 등록된 패키지만 정확히 필터링 추천하도록 수정.
    v1.0.9 (2026-11-20)

* PTC ID Import 시 기존 Test Case 전체 삭제 버그 수정:

  * applyParsedPtcListToStudio에서 isSuiteReplace 조건이 opts.isSuiteImport 또는 복수 항목 Import 시 기본 활성화되어 state.testCases = builtTcs로 기존 TC 목록을 덮어쓰던 버그를 수정하여, 명시적으로 replaceSuite: true가 지정된 경우를 제외하고 항상 기존 TC 목록을 유지한 채 ID 기준으로 병합(신규 추가 / 기존 갱신)되도록 개선.

  * importTestSuiteItems 역시 기존 state.testCases를 보존하며 ID 기준 병합/업서트하도록 보호 로직 적용 및 applyParsedPtcListToStudio 내 ensureUtilityStateInitialized() 안전 호출 추가.

* Check if {SIGNAL} {OP} {SIGNAL2} 문법 추가 및 TsMultiCheck 기반 .pkg 생성 구현:

  * DEFAULT_GRAMMARS 및 3. 가이드 → 문법 규칙에 GRAM_CHECK_SIG_VS_SIG (Check if {SIGNAL} {OP} {SIGNAL2}) 문법 규칙 추가 (+- 오차, within {TIME} {UNIT} 지원).

  * parseLine에서 우변({SIGNAL2})이 신호 사전에 등록된 신호(Helper, Map/Vector 인덱스 포함)일 때 자동 인식하며, 숫자 리터럴인 경우 기존 Check if {SIGNAL} {OP} {VALUE}로 정상 폴백.

  * .pkg XML 생성 시 TsMultiCheck 하위에 반드시 {SIGNAL2}를 먼저 tsRead(평가 OFF)하여 변수(v\_{SIGNAL2})에 저장한 뒤, 두 번째 스텝으로 {SIGNAL}을 읽어 varBaseExpression(v\_{SIGNAL2})과 비교하도록 구현.

  * <VARIABLES> 컨테이너 파싱(<VARIABLE-NAME><DVALUE> 포함)을 보강하고, {SIGNAL2} 저장 변수에 초기값 0(<DEFAULT-VALUE xsi:type="value"><DATA xsi:type="integer">0</DATA></DEFAULT-VALUE>)을 자동 선언하도록 구현.

  * 1. TC 에디터에서 Check if {SIGNAL} {OP} 입력 후 {SIGNAL2} 위치의 신호 자동완성 지원 추가.
v1.0.10 (2026-11-20)
* UI/UX 디자인 검수 전 항목(P0·P1·P2) 일괄 반영 (외곽 레이아웃 100% 보존):
   * [P0] Halcyonic 라이트 테마 명도 대비 복구: text-emerald-300, text-sky-300, text-amber-300, text-indigo-300, text-cyan-300, text-rose-300, text-violet-300 등 다크 전용 300계열 텍스트 639곳을 라이트 테마에서 WCAG AA/AAA 기준(*-700 계열)으로 일괄 매핑하고, 다크 테마의 text-slate-500(26곳)을 #94a3b8으로 상향.
   * [P1] 버튼 시각 위계 3단계 통일: 각 뷰의 핵심 액션 1~2개만 Primary(sky-600/emerald-600), 삭제 액션은 Danger(rose-600)로 유지하고, 나머지 50개 보조 유채색 버튼을 중립 Secondary(bg-slate-800 border-slate-600)로 통일해 시선 분산 해소.
   * [P1] 장문 버튼 라벨 압축, 툴팁(title) 보완 및 최소 폰트 하한선 정립: 4단어 이상 장문 버튼 30여 개를 2~3단어로 압축(기존 상세 설명은 title 툴팁으로 이관), + 추가 등 툴팁 누락 버튼 14개에 title 추가, 긴 placeholder 13개 단축, text-[9px] 전면 제거 및 10px 폰트 하한선 상향(10.5px~11px).
   * [P2] 키보드 접근성 및 레이어 토큰화: 전역 :focus-visible 포커스 링(다크 #38bdf8 / 라이트 #0369a1) 추가 및 4단계 z-index CSS 변수(--z-sticky, --z-dropdown, --z-modal, --z-toast) 정의.
v1.0.11 (2026-11-20)
* Auto-TA #condN 실행 시간 구간 격리 옵션 추가 (기본값: 없음):
   * Package(.pkg) 생성 확인 모달(#pkgIncludeTaConfirmModal)에 '#condN 시간 구간 격리' 체크박스(#chkPkgTaTimeWindowIsolate, 기본값 미체크 = 구간 격리 없음) 추가.
   * 구간 격리 옵션 선택 후 TA 포함 생성 시: Precondition의 TsStartTrace 직후(또는 Test Flow 시작부)에 기준 시각 t_trace_0 = __import__('time').monotonic()을 기록하고, 각 Auto-TA 대상 #condN 블록의 시작·종료 시점에 상대 경과 시간(t_cond{N}_start, t_cond{N}_end)을 패키지 변수(초기값 0.0)에 자동 저장.
   * Auto-TA 각 #Cond{N} TriggerBlock의 <START-CONDITION>을 (Time() >= t_cond{N}_start and Time() <= t_cond{N}_end) and (...)로 자동 결합하여, A→B(#cond1)와 C→B(#cond2)처럼 동일한 조건이 반복되더라도 서로의 구간에서 오탐(False Fail)이 발생하지 않도록 해결.
v1.0.12 (2026-11-20)
* 3. Guide의 TC 선택 .pkg 생성 UI 제거 및 1. TC 에디터 [All .pkg] TA 확인 모달로 통합:
   * 3. Guide > TC 에디터 > 설정의 '대상 TC 선택' 카드(#pkgMultiTcList, #btnGuideExportSelectedPkg, #btnNavTogglePkgTcList) 및 템플릿의 '선택 TC (*.pkg)' 버튼(#btnGuideDownloadPkg) 제거.
   * 1. TC 에디터 좌측 Nav의 [All .pkg] (#btnNavEditorExportAllPkg) 클릭 시 열리는 TA 생성 확인 모달(#pkgIncludeTaConfirmModal) 내부에 현재 로드된 TC 선택 체크리스트(#pkgTaModalTcSelectSection, 전체 선택 / 전체 해제 / 개별·통합 .pkg 선택, 실시간 선택 건수 및 Auto-TA 감지 건수 갱신) 추가.
   * 체크된 TC만 선택된 TA 옵션(TA 포함/제외, #condN 시간 구간 격리 여부)으로 일괄 또는 통합 .pkg 생성하도록 구현.
v1.0.13 (2026-11-21)
* A2L Override 최우선 예외 매핑 Excel (A~C 3열) 연동:
   * 2. 신호 사전 > 5. Override 최상단에 '예외 1순위' 카드(#inputImportOverrideExceptionExcel, #btnClearOverrideExceptionNav) 및 3. Guide > 신호 사전 > 템플릿에 3열 템플릿 다운로드 버튼(#btnGuideDownloadOverrideExceptionSample) 추가.
   * 엑셀 양식(A: Signal_Name, B: Override_Value_Signal, C: Override_Swt_Signal) 로드 시 state.overrideExceptionMap에 저장되어 resolveA2lWriteOverride에서 기존 A2L_1 / A2L_2 / A2L_3 규칙보다 최우선으로 적용 (예: diag_signal_st_01~04 → diag_signal_st_Phy[0]~[3] + 공용 diag_signal_st_Swt).
* Post Conditions 'Reset Override / Reset overwrite / Reset Overrides / Reset overwrites' 자동 리셋 구현:
   * Post Conditions에 해당 문구가 포함되면 해당 .pkg에 매핑된 모든 OL 신호를 먼저 0으로 tsWrite한 뒤, 모든 Swt 신호를 0으로 tsWrite하도록 자동 생성 (공용 Swt 중복 제거 및 xaPackage 오매핑 방지).
v1.0.14 (2026-11-21)
* Post Conditions Reset Override에 A2L Calibration 신호 기본값 복원(tsRestore) 추가:
   * buildTsRestoreXmlStep(stepId, mappingRef) 추가 (<TESTSTEP id="..." xsi:type="tsRestore"><MAPPING-REF xsi:type="string">{SIGNAL}</MAPPING-REF></TESTSTEP>).
   * TC 내에서 직접 tsWrite된 모든 A2L Calibration(CHARACTERISTIC / AXIS_PTS) 신호를 중복 없이 수집하여, Post Conditions에 Reset Override / Reset overwrite / Reset Overrides / Reset overwrites가 있을 때 ① OL 신호 0 리셋 → ② Swt 신호 0 리셋 → ③ A2L Calibration 신호 tsRestore 순으로 자동 생성.
v1.0.15 (2026-11-21)
* Post Conditions Reset Override 3단계 — Plant Model 신호 기본값 복원(tsRestore, Driver_ 제외) 추가:
   * TC 내에서 tsWrite된 Plant Model 신호(isPlantModelSignal / mappingType === "MODEL")를 중복 없이 수집하되, "Driver_"로 시작하는 신호(예: Driver_AccelPedal, Driver_BrakePedal)는 Reset 대상에서 제외.
   * Post Conditions Reset Override 실행 순서: ① OL 신호 0 리셋(tsWrite) → ② Swt 신호 0 리셋(tsWrite) → ③ A2L Calibration 신호 복원(tsRestore) → ④ Plant Model 신호 복원(tsRestore, Driver_* 제외).

## v1.0.16 (2026-11-21)
- **A2L Calibration `XACCESS` 매핑 분리 및 `<RASTER>` 생략**:
  - `parseA2lContent`에서 `CHARACTERISTIC` / `AXIS_PTS` 블록을 Calibration 신호로 자동 판별하여 Scalar는 `xaCalibValueVariable`, 1D Curve/Vector는 `xaCalibCurveVariable`, 2D Map은 `xaCalibMapVariable`로 매핑 (기존 `MEASUREMENT`는 `xaMeas*` 유지).
  - `.pkg` `<MAPPING-ITEM>` 생성 시 `xaCalib*` 신호는 `<ECU-KEY>`와 `<LABEL>`만 출력하고 `<RASTER>` 태그를 생략 (`xaMeas*`는 기존대로 `Port-Default` 유지).
  - 신호 사전 필터/배지/드롭다운, Helper L2/L4, `tsRestore` Reset Override가 `xaCalib*` 신호를 A2L로 일관되게 인식하도록 확장.
- **A2L Curve / Map 기본 `{signal}` 단일 매핑**:
  - `Signal[0]`, `Signal[0][1]` 등 인덱스 표기를 사용해도 A2L Curve/Map 신호는 `<MAPPING-ITEM>`에 `{signal}[x][y]`가 아닌 기본 신호명 `{signal}`만 매핑하도록 수정.
- **Curve / Map 요소별 `tsRead` / `tsWrite` XML 스키마 적용 (Unit 태그 제외, 기존 설정 유지)**:
  - **1D Curve `tsRead`** (`Check if Signal[0] == 9`): `curveSingleExpression` + `sparseCurve` (`<DIMENSION>`, `<DISTRIBUTION xsi:type="sparseVector">`, `<ELEMENT idx="0">`, `<METRIC>` `X-VALUE-TYPE=PHYS`, `VALUE-TYPE=PHYS`, `DATA-TYPE=CURVE`).
  - **2D Map `tsRead`** (`Check if Signal[0][1] == 5`): `mapSingleExpression` + `sparseMap` (`<X-DISTRIBUTION>`, `<Y-DISTRIBUTION>`, `<X-DIMENSION>`, `<Y-DIMENSION>`, `<ELEMENT idx="0" idy="1">`, `DATA-TYPE=MAP`).
  - **1D Curve `tsWrite`** (`Set Signal[1] to 8`, X축 수정 `Set Signal.X[1] to -20`): `expressionCurve` + `<DISTRIBUTION>` + `<VALUES>` (음수 값은 `unaryOpBaseExpression` / `UNARY_NEGATIVE` 자동 래핑).
  - **2D Map `tsWrite`** (`Set Signal[0][0] to 1`, X/Y축 수정 `Set Signal.X[0] to -90`, `Set Signal.Y[2] to 50`): `expressionMap` + `<X-DISTRIBUTION>` / `<Y-DISTRIBUTION>` + `<ELEMENT idx="x" idy="y">` + `UNARY_NEGATIVE` 지원.

## v1.0.17 (2026-11-21)
- **3. Guide 탭 명칭 변경 (`문법 규칙` → `문법 설명`)**:
  - Guide 하위 탭 버튼, 툴팁, 1페이지 즐겨찾기 점프 버튼 및 안내 문구를 `문법 설명`으로 일괄 변경.
- **Guide 문법 설명 흐름 제어(Flow Control) 세트 카드 통합**:
  - `If / Else` (조건 분기 세트), `Loop / Continue / Break` (반복 제어 세트), `Switch / Case / Default` (다중 분기 세트)를 각각 하나의 통합 카드와 실전 복합 예제로 묶어 가독성 개선 (파서·자동완성·Admin 탭의 개별 규칙은 기존대로 유지).
- **Guide 문법 설명 Map/Curve 카드 최신화**:
  - 정적 인덱스(`sparseCurve`/`sparseMap`, `expressionCurve`/`expressionMap`, `.X`/`.Y` 축 수정)와 동적 신호 인덱스(`GetValue(x, y)` / `Interpolate(x)`) 설명을 함께 명시.

## v1.0.18 (2026-11-21)
- **2.0 UI 개편 전면 롤백 (v1.0.17 원복)**: 2.0 레이아웃·Modern 테마·인스펙터·하단 상태 바·커맨드 팔레트를 모두 제거하고 안정화된 v1.0.17 UI로 완전 복원.
- **사이드바 토글 단축키 `Ctrl+B` 유지**: 어느 화면에서나 `Ctrl+B`로 좌측 사이드바를 즉시 접고 펼칠 수 있도록 단축키 유지.
- **Test Flow 에디터 VS Code 방식 `Tab` / `Shift+Tab` 2칸(`"  "`) 들여쓰기**:
  - `1. Form view`의 `#tcScriptInput` / `#tcCritInput` 및 `2. PTC view` 인라인 셀 에디터에서 자동완성 창이 열려 있지 않을 때 `Tab`을 누르면 `"  "`(공백 2칸) 들여쓰기, 다중 행 선택 시 선택된 모든 행 일괄 들여쓰기 지원.
  - `Shift+Tab`으로 현재 행 또는 다중 선택 행의 앞 공백 2칸 일괄 내어쓰기 지원.

## v1.0.19 (2026-11-21)
- **7페이지 (`7. To-Do & 현황`) 제거**: 사이드바 메뉴, User HTML Export 페이지 선택 목록, `#view-roadmap` 섹션 및 탭 목록에서 7페이지 완전 삭제.
- **56px 슬림 숫자 액티비티 레일 전환 (`#sidebar`)**:
  - 기본 진입 시 기존과 동일하게 전체 텍스트 라벨이 보이는 확장 사이드바로 유지.
  - 좌측 상단 토글 버튼(`#btnToggleSidebar`) 또는 `Ctrl+B` 단축키로 **라벨 확장 모드 ↔ 56px 슬림 숫자 레일(`1`~`6`)** 즉시 전환 (별도 이모지 아이콘 대신 깔끔한 숫자 `1`~`6`과 hover `title` 툴팁 표시).

## v1.0.20 (2026-11-21)
- **56px 슬림 레일 `JSON 열기` 아이콘 단일 표시 수정**: `<label class="striped-btn">` 내부 `<input type="file">` 때문에 `:last-child`가 매칭되지 않아 `JSON 열기` 텍스트가 남던 CSS 선택자를 `span:not(:first-child)`로 수정해 슬림 레일에서 `📂` 아이콘 하나만 깔끔하게 표시되도록 개선.

## v1.0.21 (2026-11-21)
- **책갈피 탭(`.dict-bookmark-bar` / `.dict-bookmark-tab`) 슬림·고밀도 디자인 개선**:
  - 뭉툭하던 상단 곡률(`0.65rem`)과 두꺼운 패딩/테두리를 IDE 스타일 슬림 탭(높이 `28px`, `4px` 모서리, `1px` 보더, `2px` 상단 포인트 라인, `2px` 간격)으로 축소하고 본문 컨테이너 패딩을 최적화해 공간 낭비 제거.
  - Guide 2단 하위 탭(`.guide-tier2-bookmark-bar`)은 이중 폴더형 대신 깔끔한 `25px` 언더라인 스트립으로 변경.
- **릴리스 번들 구성 규칙 고정**: `bundle.zip`에는 `ecu_test_integrity_admin.html`과 `Test_Case_Editor_Requirements_History.md` 2종 파일만 포함하도록 정리.

## v1.0.22 (2026-11-23)
- **Auto-TA `#condN` 시간 구간 격리 `.pkg` 파일 열림 오류(ECU-TEST 2024.3 역직렬화 실패) 수정**:
  - `<VARIABLES>` 생성 시 `varInitialFloatZeroSet` (`t_trace_0`, `t_cond{N}_start`, `t_cond{N}_end`) 및 `varInitialZeroSet` 변수에 출력되던 `<DEFAULT-VALUE xsi:type="value"><DATA xsi:type="float">0.0</DATA></DEFAULT-VALUE>`가 ECU-TEST 2024.3 `package.xsd`(`format-rev="1"`/`METRIC` 누락)에서 역직렬화 실패를 일으키던 원인을 제거하고, 검증된 `<DEFAULT-VALUE xsi:type="undefined"/>` 스키마로 통일.
  - Auto-TA TriggerBlock `<START-CONDITION>`에 `t_cond{N}_start is not None and t_cond{N}_end is not None` 가드를 추가하여 미실행 분기에서도 안전하게 평가되도록 보완.
  - 번호 없는 `#cond` 섹션(또는 섹션 마커 미기재) 스크립트에서도 `t_cond1_start` / `t_cond1_end` 변수 선언 및 타임스탬프 기록이 누락되지 않도록 방어 로직 추가.

## v1.0.23 (2026-11-23)
- **ECU-TEST 2021.3 버전 지원 (`..//..//` 상대경로 변환) 및 `.pkg` 생성 모달 버전·환경(SIL/HIL) 선택 기능 추가**:
  - Package(`.pkg`) 생성 확인 모달(`#pkgIncludeTaConfirmModal`)에 **ECU-TEST 버전** 선택기(`#selPkgEcuTestVersion`: `2024.3 (<workspace.packages>)` / `2021.3 (상대경로 ..//)`)와 **타겟 환경** 선택기(`#selPkgModalTargetEnv`: `SIL` / `HIL:dSPACE` / `HIL:ETAS` / `HIL`)를 추가하고 `state.pkgEcuTestVersion`, `state.pkgRelPathPrefix`, `state.targetEnv`(`#pkgTargetEnvSelect` 동기화)에 영속 저장.
  - `2021.3` 선택 시 상대경로 접두어 입력란(`#inpPkgModalRelPathPrefix`, 기본값 `..//..//`)과 `..//` · `..//..//` · `..//..//..//` 빠른 프리셋 버튼 및 실시간 경로 미리보기(`#pkgModalRelPathPreview`)를 표시.
  - `formatPkgPathForEcuTestVersion`을 통해 `2021.3` 생성 시 `<XACCESS xsi:type="xaPackage"><PATH>`의 `<workspace.packages>/...`를 `..//..//...` 형식(예: `..//..//Lib/project/...`)으로 자동 변환하고 `<PACKAGE prog-version="2021.3.0.119069">`로 출력 (`2024.3`은 기존 `<workspace.packages>/...` 및 `2024.3.0.156114+c108ea21784a` 유지).
  - 단일 TC `.pkg` 내보내기(`#btnNavEditorExportPkg`)에도 모달의 버전·타겟 환경·`#condN` 시간 구간 격리 옵션이 동일하게 반영되도록 일원화.

## v1.0.24 (2026-11-23)
- **ECU-TEST 2021.3 패키지 경로 구분자를 역슬래시 2개(`\\`) 규칙으로 보정**:
  - `2021.3` 선택 시 `<workspace.packages>`를 `..\\..\\`로 치환하고, 경로 내부의 모든 폴더 구분자(`/`, `\`)를 역슬래시 2개(`\\`)로 통일 변환 (예: `<workspace.packages>/Lib/Project` → `..\\..\\Lib\\Project`, `<workspace.packages>/Lib/Start_Measurement.pkg` → `..\\..\\Lib\\Start_Measurement.pkg`).
  - `2024.3` 선택 시 기존과 동일하게 슬래시 1개(`/`) 구분자 유지 (`<workspace.packages>/Lib/Project`).
  - `.pkg` 생성 모달의 `2021.3 상대경로` 기본값·프리셋 버튼(`..\\`, `..\\..\\`, `..\\..\\..\\`)·미리보기 및 기존 저장값 마이그레이션까지 모두 `\\` 기준으로 통일.

## v1.0.25 (2026-11-24)
- **Calibration Map / Vector (Curve) 인덱스 미지정 `tsWrite` 시 전체 배열 요소 일괄 `{VALUE}` 쓰기 지원**:
  - `buildTsWriteXmlStep`에서 `xaCalibCurveVariable`(1D Curve/Vector)에 배열 인덱스 없이 `Set {CalibCurve} to {VALUE}` 작성 시 `0 .. dimX - 1` 전체 `<ELEMENT idx="x">`에 `{VALUE}`를 기록하도록 개선 (`.X` 축 지정 시 `<DISTRIBUTION>` 전체 요소 채움).
  - `xaCalibMapVariable`(2D Map)에 배열 인덱스 없이 `Set {CalibMap} to {VALUE}` 작성 시 `0 .. dimX - 1`, `0 .. dimY - 1` 전체 `<ELEMENT idx="x" idy="y">`에 `{VALUE}`를 기록하도록 개선 (`.X` / `.Y` 축 지정 시 해당 축 전체 요소 채움).
  - 기존 정적 인덱스 지정 문법(`Set {Sig}[2] to 5`, `Set {Sig}[1][2] to -3`)은 단일 요소만 기록하도록 그대로 유지.
- **Test Flow / Evaluation Criteria 에디터 `Ctrl+Z` (Undo) / `Ctrl+Y`·`Ctrl+Shift+Z` (Redo) 지원**:
  - `Enter` 자동 들여쓰기, `Tab`/`Shift+Tab` 들여쓰기, 자동완성 삽입(`applySelectedSignalAutocomplete`) 시 브라우저 네이티브 Undo 스택이 초기화되던 문제를 해결하기 위해 TC·에디터별 독립 Undo/Redo 히스토리 매니저(`dslEditorUndoMgr`, 최대 200단계, 커서 위치 복원 포함)를 `#tcScriptInput` 및 `#tcCritInput`에 적용.

## v1.0.26 (2026-11-24)
- **에디터 핵심 단축키 일괄 적용 (`Ctrl+/` 주석 제외) 및 단축키 치트시트 영구 수록**:
  - **에디터 내부 단축키 (`#tcScriptInput`, `#tcCritInput`, 모두 `Ctrl+Z` / `Ctrl+Y` Undo·Redo 연동)**:
    - `Alt+↑` / `Alt+↓`: 현재 행(또는 선택 블록) 위/아래 이동 (`moveLinesInTextarea`)
    - `Shift+Alt+↓` / `Shift+Alt+↑`: 현재 행(또는 선택 블록) 아래/위로 복제 (`duplicateLinesInTextarea`)
    - `Ctrl+Shift+K`: 현재 행(또는 선택 블록) 삭제 (`deleteLinesInTextarea`)
    - `Ctrl+Space`: 신호·문법·패키지 자동완성 수동 호출
    - `Ctrl+Alt+N`: 다음 번호 `#condN` / `#critN` 블록 쌍 삽입 (`+ #cond/crit` 버튼 Undo 기록 포함)
  - **전역 단축키**:
    - `Ctrl+S`: 워크스페이스 JSON 즉시 저장 (`#btnSaveWorkspace`)
    - `Ctrl+Shift+E`: 현재 TC `.pkg` 생성 모달 열기 (`#btnNavEditorExportPkg`)
    - `Alt+PageUp` / `Alt+PageDown`: 이전 / 다음 Test Case 전환
    - `F1`: 단축키 안내 모달(`#editorShortcutHelpModal`) 열기/닫기 (기존 `Ctrl+B` 사이드바 토글 유지)
  - **단축키 안내 UI 상시 노출**:
    - 1페이지 7·8. 툴바에 `? 단축키` 버튼(`#btnOpenShortcutHelpModal`) 및 고대비 단축키 모달(`#editorShortcutHelpModal`) 추가.
    - `3. Guide > TC 에디터 > 문법 설명`에 **5. 에디터 단축키** 치트시트 카드 상시 수록.
  - **`dslEditorUndoMgr` 최초 1회 편집 직후 `Ctrl+Z` 초기 스냅샷 덮어쓰기 버그 수정**: `ensure()`가 초기 스냅샷을 덮어쓰지 않도록 보정해 첫 번째 편집 직후에도 즉시 Undo가 동작하도록 검증 완료.

## v1.0.27 (2026-11-24)
- **에디터 단축키 키 바인딩 변경 (`Alt` 조합 → `Ctrl` 중심 직관 키)**:
  - 행 위/아래 이동: `Alt+↑` / `Alt+↓` → **`Ctrl+↑` / `Ctrl+↓`**
  - 행 위/아래 복제: `Shift+Alt+↑` / `Shift+Alt+↓` → **`Ctrl+Shift+↑` / `Ctrl+Shift+↓`**
  - 다음 `#condN` / `#critN` 블록 쌍 삽입: `Ctrl+Alt+N` → **`Ctrl+Enter`**
  - `? 단축키` 모달(`#editorShortcutHelpModal`), `3. Guide > 문법 설명`의 `5. 에디터 단축키` 치트시트, `+ #cond/crit` 버튼 툴팁을 변경된 단축키로 일괄 동기화.

## v1.0.28 (2026-11-24)
- **좌측 Nav `Test Suite Overview` 4종 가독성·탐색 패키지 적용**:
  - **3단 폭 토글**: `Test Suite Overview` 헤더에 `숨김(0px)` / `좁게(204px)` / `넓게(360px)` 3단 전환 버튼(`#btnNavWidthHide`, `#btnNavWidthNarrow`, `#btnNavWidthWide`) 추가 및 `localStorage` 영속 저장.
  - **드래그 리사이즈**: `#leftEditorSubSidebar` 우측 경계에 드래그 핸들(`#editorNavResizeHandle`, `180px ~ 480px`) 배치, 더블클릭 시 기본 `204px` 즉시 복원.
  - **2행 컴팩트 TC 카드**: 1행에 `#ID` + `Pass/Fail` 배지 + 삭제 버튼, 2행에 `Test Case Name` 최대 2줄 표시(`.tc-card-title-2line`) 및 전체 이름 툴팁(`title`) 적용.
  - **TC Quick Switcher (`Ctrl+P` / `🔍` 버튼)**: 화면 중앙 넓은 검색 팝업(`#tcQuickSwitcherModal`)에서 전체 TC의 ID·전체 이름·상태를 실시간 검색하고 `↑/↓` + `Enter`로 즉시 점프 (`? 단축키` 모달 및 `3. Guide > 문법 설명` 치트시트에 `Ctrl+P` 추가).
- **PTC ID Import Dummy TC 유입 버그 및 Test Suite `Functional Test` 조회 완전 수정**:
  - 1페이지 좌측 Nav `ID Import` 버튼/Enter 핸들러가 `AUTO_DETECT` / `VIEW_ISSUE` 모드를 무시하고 무조건 `SUITE_ISSUES`로 덮어쓰던 버그를 수정하여 단일 TC ID 입력 시 즉시 해당 TC를 정상 Import하도록 복구.
  - `parsePtcRawResponseToTestCases`에서 CLI 오류 문자열이나 유효 필드가 없는 응답에 대해 가짜 `PTC_TC_...` + `Wait 100 ms` Dummy TC를 생성하던 로직을 차단.
  - 내장 Python 브릿지(`ptc_local_bridge.py` v1.0.28) 및 JS `expandTestSuiteChildTestCasesViaBridge`에 `VIEW_ISSUE` 지원, 단일 TC Fast-Path, 그리고 Test Suite ID 조회용 `im viewsegment --batch` → `im issues` → 들여쓰기 포함 `Contains` 재귀 탐색(depth 6) 및 `Category == Functional Test` 엄격 필터링을 통합 적용.


## v1.0.29 (2026-11-24)
- **PTC 단일/다중 TC Import 회귀 버그 및 페이지네이션 가시성 수정**:
  - `runUtility4PtcIdImport`의 브릿지 호출 시 `VIEW_ISSUE`를 구버전(`v50.93`) 및 신버전(`v1.0.29+`) Python 브릿지 모두가 인식하는 `SINGLE_ISSUE`로 전송하도록 호환성 보정.
  - `/im/import` 요청 타임아웃을 30초 → 120초(`queryBridgeCliArgs` 45초)로 상향하고, `AbortError` 타임아웃을 조용히 삼켜 기존 텍스트로 폴백하던 `catch (_) {}` 로직을 제거해 명확한 오류 토스트를 출력하도록 수정.
  - `parsePtcRawResponseToTestCases`에서 `Type:` 줄이 `ID:` 줄보다 먼저 나오는 `im viewissue` 응답을 두 블록으로 쪼개 가짜 헤더 TC를 만들던 블록 분할 버그 수정.
  - 기존 TC를 유지하며 병합(`applyParsedPtcListToStudio`)한 뒤 검색어(`tcSearchQuery`) 초기화, 신규/갱신 TC가 위치한 페이지(`state.tcPage`)로 자동 이동, 포커스 중인 `#tcIdInput` 블러 처리로 Import 결과가 Nav 및 에디터에 즉시 반영되도록 개선.
- **PTC Test Suite ID `Functional Test` 미검출 원인 규명 및 수정**:
  - `classifyPtcItemMeta`(JS) 및 `parse_block_meta`(Python 브릿지 `v1.0.29`)에서 `Type`에 `"Suite"` / `"Document"`(예: `Test Suite Content`)가 포함된 경우 `Category: Functional Test`여도 Test Suite 컨테이너로 오분류해 제외하던 버그를 수정(`Functional Test` 명시 시 최우선 인정 + `Shared Category` / `Contains Referenced` 필드 매핑 추가).
  - `im viewsegment` 파싱 정규식(`(\d{4,12})`)이 헤더 메타데이터의 4자리 연도(`2026` 등)를 하위 ID로 오인해 `im issues` 조회를 건너뛰던 버그를 수정(헤더 `Key: Value` 줄 및 `1990~2099` 연도 제외, `im issues` 우선 실행 + `Document ID` / `Root ID` / `Contained By` / `viewsegment` / `Contains` 결과 통합).
  - `Functional Test` 항목이 0건일 때 감지된 `Type/Category` 목록을 토스트에 함께 표시하는 진단 안내 추가.
- **`Ctrl+Enter` (`+ #cond/crit`) 에디터 즉시 반영 및 `#condN`/`#critN` 동시 추가 수정**:
  - `renderActiveTestCaseEditor()`의 `document.activeElement !== flowEl / critEl` 가드로 인해 에디터에 포커스가 있는 상태에서 `Ctrl+Enter` 입력 시 포커스된 textarea의 화면 값(`.value`)이 갱신되지 않던 버그 수정(통합 모드에서 미반영, 분리 모드에서 `#crit` 창 포커스 시 `#cond`만 추가되고 `#crit`은 안 보이던 현상 해결).
  - `btnAddCondCritMarker` 및 `appendLineToActiveScript`에서 현재 입력값 동기화 → `tc.script` 갱신 → `#tcScriptInput` / `#tcCritInput` `.value` 직접 즉시 반영 → `Ctrl+Z` 실행 취소 스냅샷 기록 → `#condN` 입력 줄로 커서 자동 이동까지 일괄 처리.


## v1.0.30 (2026-11-24)
- **초기 진입 화면 `1. TC 에디터` 고정**: HTML 최초 로드 시 `localStorage`의 마지막 탭과 무관하게 항상 `1. TC 에디터`(`state.activeTab = "editor"`)로 시작하도록 고정.
- **Nav `Test Suite Overview` TC 이름 폰트 축소**: 2행 TC 카드의 Test Case Name(`.tc-card-title-2line`) 폰트를 `9.5px` / `font-weight: 500` / `line-height: 1.24`로 컴팩트하게 조정.
- **Nav 3단 폭 토글(`숨김/좁게/넓게`) 및 우측 경계 드래그 리사이즈 완전 수정**:
  - 후반부 CSS 규칙(`#content .editor-main-grid { grid-template-columns: 204px ... !important; }`)이 `--editor-subnav-width`를 덮어쓰던 충돌 제거 및 `768px` 이상 뷰포트(Canvas 포함)에서도 동작하도록 반응형 기준 완화.
  - `#leftEditorSubSidebar`의 `overflow-x: hidden`에 의해 잘리던 `#editorNavResizeHandle` 위치를 우측 경계 내부(`right: 0; width: 7px; z-index: 50`)로 보정하고 `applyEditorNavWidth`에서 인라인 `grid-template-columns`를 함께 반영.
- **`Ctrl+P` TC Quick Switcher 동작 수정**:
  - 전역 단축키 리스너를 `window` 캡처 단계(`capture: true`)로 승격하고, 한글 입력기(IME) 상태에서도 인식되도록 `e.code` (`KeyP`, `KeyB`, `KeyS`, `KeyE`) 매칭을 병행 적용.
  - 모달 열기/닫기 시 `display: flex / none` 명시 제어 및 TC 선택 시 해당 페이지(`state.tcPage`)로 자동 이동 추가.


## v1.0.31 (2026-11-24)
- **초기 진입 화면 `1. TC 에디터` 고정 완전 수정**: HTML 초기 활성 탭(`nav-tab` / `#view-editor` vs `#view-grammars`)을 `1. TC 에디터`로 변경하고, `DOMContentLoaded`에서 실제 `.nav-tab[data-tab="editor"]` 탭 전환을 실행하도록 수정.
- **Nav 3단 폭 토글을 상단 `Nav 숨김/펼치기` 버튼(`#btnToggleSubNav`)으로 통합**:
  - `Test Suite Overview` 내부의 `숨김/좁게/넓게` 버튼을 제거하고, 상단 `#btnToggleSubNav` 버튼 클릭 시 `숨김(0px, 작대기 1개)` → `좁게(204px, 작대기 2개)` → `넓게(360px, 작대기 3개)` 순으로 순환하도록 통합(`data-nav-bars="1|2|3"`).
  - `applyEditorNavWidth`가 `600px` 이상 모든 뷰포트에서 `grid-template-columns` 및 숨김 시 `display: none`을 즉시 적용하도록 보강해 Canvas·데스크톱 어디서나 확실히 동작하도록 수정.
- **TC Quick Switcher 단축키 변경 (`Ctrl+P` → `Ctrl+K`)**: 브라우저 인쇄 단축키(`Ctrl+P`)와의 충돌을 피하기 위해 `Ctrl+K` (`e.code === "KeyK"` 한글 IME 호환)로 변경하고 모달·툴팁·도움말 표기를 일괄 갱신.


## v1.0.32 (2026-11-24)
- **Nav 숨김 시 메인 에디터 영역 사라짐 버그 수정**: `#leftEditorSubSidebar`를 `display: none`으로 숨길 때 `#editorMainGrid`가 `0px minmax(0, 1fr)` 2열 그리드를 유지해 메인 에디터가 0px 첫 번째 열로 자동 배치되던 CSS Grid 버그를 단일 열(`minmax(0, 1fr)`)로 변경해 메인 영역이 100% 전체 폭으로 펼쳐지도록 수정.
- **Nav 넓게 폭 조정 (`360px` → `290px`)**: 상단 3단 토글(작대기 3개)의 넓게 기본 폭을 `290px`(전환 기준 `250px`)로 적정화.


## v1.0.33 (2026-11-24)
- **2. 신호 사전(`#view-signals`) 색상 통일 및 `비우기` 버튼 휴지통 아이콘화**:
  - A2L·Helper·DBC·Plant model·Override 카드 및 하위 예외/BSW/A2L_3/전체 초기화 버튼의 `비우기`/`삭제` 텍스트 버튼을 배경색과 경계선이 없는 깔끔한 휴지통 SVG 아이콘(`.sig-trash-btn`, 호버 시에만 로즈 강조)으로 일괄 교체.
  - 6종 원색(sky/indigo/emerald/teal/amber/rose)이 혼재하던 파일 업로드 버튼·배지·세부 필터 활성 색상을 **중립 Slate(보조 버튼·배지)** + **단일 Sky 강조(핵심 액션·활성 필터)** 2톤 팔레트로 전면 통일.


## v1.0.34 (2026-11-24)
- **2. 신호 사전 좌측 Nav 파일 계열별 소프트 틴트 색상 복원 & 컴팩트 간격 축소**:
  - 성격이 같은 파일군별로 절제된 반투명 틴트 색상 + 좌측 액센트 라인 적용: **A2L·Helper(Sky)**, **DBC(Emerald)**, **Plant model(Indigo)**, **Override(Amber)**, **예외 1순위(Rose)** (다크·라이트 테마 모두 고대비 지원).
  - 카드·서브카드·버튼의 상하 `padding` 및 `space-y` 간격을 대폭 축소하고, 비어 있는 파일 목록 컨테이너(`:empty`)의 불필요한 공백을 제거.
- **좌측 Nav 독립 세로 스크롤 적용**: `#loadedFilesManagerPanel`(신호 사전) 및 `#leftEditorSubSidebar`(TC 에디터)에 `position: sticky; top: 54px; max-height: calc(100vh - 64px); overflow-y: auto; overscroll-behavior: contain`을 적용해 본문과 무관하게 Nav 패널만 단독으로 상하 스크롤 가능하도록 개선.


## v1.0.35 (2026-11-24)
- **2. 신호 사전 좌측 Nav 폰트 축소 및 줄바꿈·오버플로우 해소**:
  - 모든 파일 카드 헤더를 `flex-nowrap` + `10px`로 통일하고 `4. Plant model (.m·.xam)`을 `4. Plant (.m·.xam)`(전체명 툴팁 유지)으로 단축해 2행 줄바꿈 방지.
  - Plant model 3열 버튼을 `SIL` / `dSPACE` / `ETAS` (`9.5px`, `truncate`, 전체명 툴팁 유지)로 축약해 `HIL:dSPACE` 칸 초과 해소.
  - `"로드된 파일 없음"` 안내 문구를 `9px` 옅은 회색(`text-slate-500/80`, `py-0`)으로 축소해 시각적 부담 완화.


## v1.0.36 (2026-11-25)
- **2. 신호 사전 테이블 슬림화 및 가로 스크롤 즉시 접근성 개선**:
  - 기본 페이지당 표시 신호 수를 `10개씩` → **`5개씩`**(`state.sigPageSize = 5`, `#sigPageSizeSelect` 5/10/20/50/100)으로 변경.
  - 테이블 스크롤 영역의 최대 높이를 `max-h-[560px]` → **`max-h-[340px]`**로 축소해 페이지를 끝까지 내리지 않고도 화면 안에서 바로 가로 스크롤바를 조작할 수 있도록 개선.
  - 헤더·검색 바·테이블 셀(`py-2.5 px-3` → `py-1 px-2`)·페이지네이션 바의 전체 패딩과 마진을 슬림하게 축소하고, 빈 Target Path(ETAS/dSPACE) 줄을 생략해 행 높이를 절반 수준으로 압축.

## v1.0.37 (2026-11-25)
- **2. 신호 사전 `4. Plant (.m·.xam)` 카드 세로 높이 확대**:
  - `#sigCardPlantModel`에 `min-height: 156px` 플렉스 레이아웃을 적용하고 `#loadedFileListPlant` 높이를 `max-height: 3.2rem` → `min-height: 6.2rem` / `max-height: 14rem`으로 확장해 여러 Plant model 파일(SIL / HIL:dSPACE / HIL:ETAS)을 여유롭게 확인 가능하도록 개선.
- **2. 신호 사전 좌측 Nav 로드된 파일 기본 접힘 상태 & 전체 파일명 표시**:
  - `renderLoadedFilesManager()` 및 `renderOverrideExceptionNavStatus()`에서 모든 로드된 파일 항목을 기본적으로 접힌 상태(`window.__expandedLoadedFileIds` 빈 Set)로 렌더링.
  - 접힌 상태에서는 태그·건수·버튼을 숨기고 파일명만 줄바꿈(`white-space: normal; word-break: break-all; overflow-wrap: anywhere`)으로 잘림 없이 전체 표시.
  - 파일명을 클릭(또는 Enter/Space)해 펼쳤을 때만 환경/슬롯 태그, 건수, `교체`/`삭제` 액션 버튼이 표시되도록 구현.
- **PTC ID Import 동작 복구 (`v50.88` 검증 경로 복원 + 기존 TC 보존)**:
  - 내장 `ptc_local_bridge.py` (`v1.0.37`) 및 `runUtility4PtcIdImport`에 `v50.88`의 단발성 `im issues --queryDefinition=((field[Document ID]=...) and (field[Category]=Functional Test)) --fields=... --delim=\t --showRichContent --batch` → `(field[Document ID]=...)` → `im viewissue --showRichContent --batch` 빠른 조회 흐름을 복원.
  - `classifyPtcItemMeta` 및 `applyParsedPtcListToStudio`의 과도한 `Functional Test` 카테고리 거절 로직을 완화해 단일/다중 TC 및 커스텀 카테고리 TC가 정상 Import되도록 수정.
  - `applyParsedPtcListToStudio`에서 `isSuiteReplace = false`로 고정해 PTC ID / TS ID Import 시 기존 `state.testCases`가 삭제되지 않고 ID 기준 병합(기존 갱신·신규 추가)되도록 보장.
