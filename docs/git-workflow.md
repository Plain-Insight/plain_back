# 🌿 Git Branch Strategy

## 📋 브랜치 구조

```
main (프로덕션)
├── develop (개발 통합)
    ├── feat/login-system
    ├── feat/user-dashboard  
    ├── feat/ai-integration
    └── feat/data-processing
```

## 🎯 브랜치 설명

### **main** 🚀
- **목적**: 안정적인 프로덕션 브랜치
- **특징**: 항상 배포 가능한 상태 유지
- **보호**: 직접 푸시 금지, PR을 통해서만 업데이트
- **자동화**: 머지 시 자동 배포 실행

### **develop** 🔧
- **목적**: 개발 통합 브랜치 (기본 브랜치)
- **특징**: 모든 기능 개발의 베이스
- **역할**: 기능 브랜치들이 머지되는 중심점
- **테스트**: 통합 테스트 및 품질 검사 실행

### **feat/*** ✨
- **목적**: 새로운 기능별 개발 브랜치
- **명명 규칙**: `feat/기능명` (예: `feat/user-authentication`)
- **생성**: develop 브랜치에서 분기
- **머지**: develop 브랜치로 PR 생성

## 🔄 워크플로우

### 1. **새 기능 개발 시작**
```bash
# develop 브랜치에서 최신 코드 받기
git checkout develop
git pull origin develop

# 새 기능 브랜치 생성
git checkout -b feat/new-feature

# 개발 작업...
git add .
git commit -m "[FEATURE] 새 기능 구현"

# 브랜치 푸시
git push origin feat/new-feature
```

### 2. **Pull Request 생성**
- **From**: `feat/new-feature`
- **To**: `develop` 
- **리뷰**: 팀원 코드 리뷰 필수
- **체크**: CI/CD 파이프라인 통과 필수

### 3. **릴리즈 프로세스**
```bash
# develop → main PR 생성
# 모든 테스트 통과 후 머지
# main 브랜치 자동 배포
```

### 4. **브랜치 정리**
```bash
# 머지 완료된 기능 브랜치 삭제
git branch -d feat/completed-feature
git push origin --delete feat/completed-feature
```

## 📝 커밋 메시지 규칙

### **형식**
```
[TYPE] 제목

상세 설명 (선택사항)
```

### **타입**
- `[FEATURE]`: 새로운 기능 추가
- `[BUG]`: 버그 수정  
- `[DOCS]`: 문서 업데이트
- `[REFACTOR]`: 코드 리팩터링
- `[TEST]`: 테스트 추가/수정
- `[STYLE]`: 코드 스타일 변경

### **예시**
```bash
git commit -m "[FEATURE] 사용자 로그인 시스템 구현

- JWT 토큰 기반 인증 시스템
- 로그인/로그아웃 API 엔드포인트
- 사용자 세션 관리 기능"
```

## 🛡️ 브랜치 보호 규칙

### **main 브랜치**
- ✅ PR 리뷰 필수 (최소 1명)
- ✅ 상태 체크 통과 필수
- ✅ 최신 상태 유지 필수
- ❌ 직접 푸시 금지
- ❌ 강제 푸시 금지

### **develop 브랜치**  
- ✅ PR 리뷰 권장
- ✅ 상태 체크 통과 필수
- ✅ 최신 상태 유지 권장

## 🚀 자동화 트리거

### **develop 브랜치 푸시 시**
- 코드 품질 검사 (Black, isort, Flake8)
- 단위 테스트 실행
- 통합 테스트 실행
- 코드 커버리지 체크

### **main 브랜치 머지 시**
- 전체 테스트 스위트 실행
- 프로덕션 배포 준비
- 릴리즈 노트 자동 생성
- 태그 생성 및 GitHub Release

## 📊 브랜치 현황 모니터링

### **확인 방법**
```bash
# 로컬 브랜치 확인
git branch

# 원격 브랜치 포함 전체 확인  
git branch -a

# 브랜치 간 차이 확인
git log --oneline --graph --all

# 머지되지 않은 브랜치 확인
git branch --no-merged develop
```

### **정리 명령어**
```bash
# 머지 완료된 로컬 브랜치 정리
git branch --merged develop | grep -v develop | xargs git branch -d

# 원격에서 삭제된 브랜치 로컬에서 정리
git remote prune origin
```

## 🎯 다음 단계

1. **GitHub 설정**
   - develop을 기본 브랜치로 설정
   - 브랜치 보호 규칙 설정
   - PR 템플릿 활성화

2. **첫 번째 기능 브랜치 생성**
   - `feat/project-setup`
   - `feat/core-ai-module`
   - `feat/api-server`

3. **팀 가이드라인 공유**
   - 브랜치 전략 문서 공유
   - 커밋 메시지 규칙 교육
   - PR 리뷰 프로세스 정립