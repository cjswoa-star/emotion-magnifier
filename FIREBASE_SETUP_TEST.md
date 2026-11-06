# 감정확대경 현황판 — Firebase 연동 점검 (2026-11-06)

## 소스와 주소

- 교사: `teacher-test.html`
- 참여자: `join-test.html`
- 기존 감정확대경: `index-v3.html` (원본 유지)
- Firebase DB: `emotion-share-test` 프로젝트의 `emotionMagnifierTest/sessions/{6자리 코드}`
- 보안 규칙 병합 후보: `firebase-rules-merge-proposed.json` (**Firebase에 자동 배포되지 않음**)
- 변경 전 백업: `backup-before-teacher-dashboard-20261106` 브랜치

## Firebase에서 직접 확인·적용할 사항

1. Firebase Console → Authentication → Sign-in method에서 **익명(Anonymous) 로그인**이 활성화되어 있는지 확인한다.
2. Realtime Database → Rules에서 현재 서버에 적용된 규칙을 먼저 백업한다.
3. 기존 FAMOUS PEOPLE 규칙과 다른 서비스의 규칙을 유지하면서 `emotionMagnifierTest` 하위 규칙만 추가한다. 제공된 병합 후보는 GitHub의 기존 `database.rules.json`을 기준으로 만들어졌으므로, **서버의 현행 규칙과 차이가 있으면 그대로 덮어쓰지 않는다.**
4. Rules를 게시한 뒤 Firebase 콘솔에서 `emotionMagnifierTest/sessions` 경로에 데이터가 생성되는지 확인한다.
5. 실사용 전 관리 계정 권한, 개인정보 처리 방식, 익명 로그인 악용 및 데이터 보관·삭제 정책을 추가 검토한다.

## 필수 실기기 점검

1. 교사 브라우저에서 `teacher-test.html` 열고 **새 참여방 만들기**를 선택한다.
2. QR과 6자리 코드가 화면에 표시되는지 확인한다.
3. **다른 브라우저 또는 다른 기기**에서 학생 주소로 입장한다. 코드를 입력하고 닉네임을 정한다.
4. 감정 퀴즈 10문제를 완료한다. 현황판의 완료 인원·평균 점수·순위가 자동 갱신되는지 확인한다. 재응시 결과의 문항별 응답 및 최고 점수가 저장되는지 확인한다.
5. 감정 지도에서 위치를 누른 뒤 **확인했어요**를 누른다. 전체 지도에 점 하나가 나타나는지 확인한다.
6. 교사 화면에서 감정 퀴즈/지도 박스를 클릭해 전체화면 확대, ESC 복귀, 순위 한 명씩 공개를 점검한다.
7. 잘못된 참여코드, 규칙 미적용, 다른 교사 브라우저에서 열기, 퀴즈 도중 나가기, 네트워크 끊김도 확인한다.

## 현재까지 확인된 범위

- GitHub 저장소에 프런트엔드 코드 저장 성공
- JavaScript 구문, V3 버튼/상태 명칭, 데이터 경로 정적 점검 완료
- 실제 서버 규칙 배포 및 실시간 다중기기 테스트 **미완료**
- 신규 Firebase 규칙은 파일로만 준비했으며 실제 데이터베이스에 게시하지 않음

**주의**: 보안 규칙 적용 및 테스트 전에 학생의 실명이나 민감한 감정 기록을 수집하지 않는다. 교사 현황판은 감정 지도에 닉네임을 표시하지 않지만, 데이터베이스에는 Firebase 사용자 ID가 함께 사용되므로 완전한 익명 수집과는 다르다.
