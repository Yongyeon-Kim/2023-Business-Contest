# 2023 공공데이터 창업 경진대회 - 반려동물 질병 진단 시스템

이 저장소는 2023년 공공데이터 창업 경진대회에 출품된 반려동물 질병 진단 시스템의 소스 코드입니다.
사용자가 반려동물의 이미지를 업로드하면 인공지능 모델(YOLOF)이 질병 유무와 종류를 분석하여 알려주는 웹 애플리케이션입니다.

## 📌 프로젝트 소개

이 프로젝트는 반려동물의 건강 관리를 돕기 위해 개발되었습니다. 주요 기능은 다음과 같습니다:

- **AI 질병 진단**: 반려동물 사진을 업로드하면 AI가 이미지를 분석하여 질병을 탐지하고 진단 결과를 제공합니다.
- **스케줄 관리**: 반려동물의 병원 방문 일정 등을 관리할 수 있는 캘린더 기능을 제공합니다.
- **대시보드**: 진단 이력 및 일정 등을 한눈에 볼 수 있는 관리자 대시보드 UI를 포함합니다.

## 🛠 기술 스택 (Tech Stack)

### Backend
- **Framework**: FastAPI
- **AI/ML**: PyTorch, YOLOF (You Only Look One-level Feature), OpenCV
- **Database**: TinyDB (JSON 기반 경량 데이터베이스)
- **Library**: `torch`, `torchvision`, `opencv-python`, `pycocotools` 등

### Frontend
- **Framework**: Next.js (React)
- **Language**: TypeScript
- **UI Library**: Material UI (MUI)
- **HTTP Client**: Axios
- **Visualization**: Recharts, Chart.js
- **Other**: FullCalendar (일정 관리), Firebase (연동)

## 📂 디렉토리 구조

```bash
├── BACKEND/            # FastAPI 기반의 AI 모델 서버
│   ├── config/         # 모델 설정 파일
│   ├── evaluator/      # 모델 평가 스크립트
│   ├── font/           # 결과 이미지에 한글 출력을 위한 폰트
│   ├── models/         # YOLOF 등 모델 정의
│   ├── static/         # 업로드된 이미지 및 결과 이미지 저장소
│   ├── demo_FastAPI.py # 모델 추론 로직 (Inference)
│   ├── main_FastAPI.py # API 엔트리 포인트
│   ├── train.py        # 모델 학습 스크립트
│   └── requirements.txt # Python 의존성 목록
│
└── FRONTEND/           # Next.js 기반의 웹 애플리케이션
    ├── src/            # 소스 코드 (Pages, Components 등)
    ├── public/         # 정적 리소스
    ├── next.config.js  # Next.js 설정
    └── package.json    # Node.js 의존성 목록
```

## 🚀 설치 및 실행 방법

### 1. Backend (AI Server) 실행

**필수 요건**: Python 3.8 이상, CUDA 지원 GPU (권장)

```bash
# BACKEND 디렉토리로 이동
cd BACKEND

# 의존성 패키지 설치
pip install -r requirements.txt

# 서버 실행 (uvicorn)
uvicorn main_FastAPI:app --reload
```

> **주의**: `demo_FastAPI.py` 내에 모델 가중치 파일 경로(`weight`)와 폰트 경로가 하드코딩되어 있을 수 있습니다. 실행 환경에 맞게 경로를 수정해야 할 수 있습니다.

### 2. Frontend (Web App) 실행

**필수 요건**: Node.js, npm 또는 yarn

```bash
# FRONTEND 디렉토리로 이동
cd FRONTEND

# 의존성 패키지 설치
npm install
# 또는
yarn install

# 개발 서버 실행
npm run dev
# 또는
yarn dev
```

웹 브라우저에서 `http://localhost:3000` (기본 설정 시)으로 접속하여 확인할 수 있습니다.

### 3. Docker로 실행 (전체 서비스)

**필수 요건**: Docker, Docker Compose

프로젝트 루트 디렉토리에서 다음 명령어로 전체 서비스(Backend + Frontend)를 한 번에 실행할 수 있습니다.

```bash
# 이미지 빌드 및 컨테이너 실행
docker-compose up --build

# 백그라운드에서 실행하려면 -d 옵션 사용
# docker-compose up -d --build
```

- **Frontend**: `https://localhost` (443 포트 매핑됨)
- **Backend**: `http://localhost:8000`

## ⚠️ 참고 사항

- 이 코드는 대회 참가를 목적으로 작성되어, 일부 경로(예: `/home/kyy/...`)가 하드코딩되어 있거나 로컬 환경에 특화된 설정이 포함되어 있을 수 있습니다. 실행 전 `BACKEND/demo_FastAPI.py` 등의 파일에서 경로 설정을 확인해 주세요.
- SSL 인증서 관련 설정(`mkcert` 등)이 포함되어 있으니, 로컬 개발 환경에 맞춰 `next.config.js`나 `package.json`의 스크립트를 조정해야 할 수 있습니다.
