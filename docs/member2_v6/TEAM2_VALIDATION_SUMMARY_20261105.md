# 팀원 2 V6 검증 인계 요약

작성: 2026-11-05 KST

## 담당 범위
수량·날짜·금액·타입·정규화 및 계산 검증, C001/C008/C013/C017의 Native 출력부터 Adapter와 Python Safety V6까지의 연결을 담당한다. Studio 운영 및 IndependentQA와 최종 Gate는 구도훈, Gold·Evidence·CI 인계는 최유석, Human Gold 판단은 김민주 담당이다. 인계서는 역할 배정 자료이며 완료 인증이 아니다.

## 로컬 테스트
2026-11-05에 `python -m pytest tests/test_python_safety_v6.py -q -p no:cacheprovider` 실행: **104 passed**. 저장된 C001 재생과 합성/실패 회귀를 포함하며, 이번 실행은 실제 Studio/API 호출이나 새로 제공된 파일의 종단 간 테스트가 아니다. 이전 전체 회귀는 189 passed.

## 제공된 NormalizeDocuments JSON의 관찰
파일 내용을 읽어 요약한 것으로, PDF 원문 대조나 Python 결과 검증은 아직 하지 않았다. 출처와 실행 상태를 별도 확인해야 한다.

| 사례 | 파일에서 관찰한 내용 | 후속 검증 |
|---|---|---|
| C001 | PO1/R1 100 EA, 변경일 2026-11-08, 견적 60 EA. evidence 배열 비어 있음 | Native 바인딩 및 계산 결과와 원문 대조 |
| C008 | 발주 R1 40 EA, R2 60 EA; 통보는 R2 60 EA | R1 유지, R2 반영, 수량·금액 검증과 원문 대조 |
| C013 | 통보 PO999, 발주/견적 PO1. 통보와 발주에 충돌 및 supplier_id 관련 경고 | 경고 보존과 BLOCKED 처리 확인; 임의 값 보정 금지 |
| C017 | 변경일 2026-11-08의 ISO 형식; evidence 배열 비어 있음 | 실제 원문과 날짜 정규화 및 계산 검증 |

## 다음 단계
1. 운영 Workflow/Config/Job/Step/File ID와 PDF 해시를 담당자에게 받아 입력 바인딩과 출처를 확인한다.
2. 네 건의 원본 JSON을 보존해 안전한 Python 경로로 분석하고, 케이스별 상태·값·타입을 기록한다.
3. C013 경고와 PO 불일치에서 차단 결과를 확인하고, PDF 원문 및 Human Gold와 근거를 대조한다.
4. 최신 통합 저장소 및 대상 PR과 CI를 재확인한다. 인계서 작성 당시 통합 저장소 접근은 404로 차단되어 있었다.
5. 신규 유료 Studio 실행은 예산 승인 이후 진행한다.

참고: [Python Safety V6 인계](../PYTHON_SAFETY_V6_HANDOFF.md), [검증 매트릭스](VALIDATION_MATRIX.md).
