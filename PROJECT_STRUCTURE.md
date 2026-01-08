# 산그린호텔 웹사이트 프로젝트 구조

## 📦 전체 구조

```
산그린호텔/
├── src/                          # 소스 코드
│   ├── app/                      # 애플리케이션 컴포넌트
│   │   ├── App.tsx              # 메인 앱 컴포넌트
│   │   └── components/          # 재사용 가능한 UI 컴포넌트들
│   │       ├── figma/           # Figma 관련 컴포넌트
│   │       └── ui/              # 기본 UI 컴포넌트들
│   ├── imports/                 # Figma에서 가져온 파일들
│   │   ├── 0메인디자인.tsx      # 메인 페이지 디자인
│   │   └── svg-odl0poeqkm.ts   # SVG 경로 데이터
│   ├── styles/                  # 스타일 파일들
│   │   ├── index.css           # 메인 스타일 진입점
│   │   ├── fonts.css           # 폰트 설정
│   │   ├── tailwind.css        # Tailwind CSS 설정
│   │   └── theme.css           # 테마 변수 및 색상
│   └── main.tsx                # React 앱 진입점
│
├── public/                      # 정적 파일
│   ├── vite.svg                # 파비콘
│   └── .htaccess               # Apache 서버 설정
│
├── guidelines/                  # 프로젝트 가이드라인
│   └── Guidelines.md
│
├── index.html                   # HTML 진입점
├── package.json                 # 프로젝트 의존성 및 스크립트
├── vite.config.ts              # Vite 빌드 설정
├── postcss.config.mjs          # PostCSS 설정
├── tsconfig.json               # TypeScript 설정 (자동 생성)
│
├── README.md                    # 프로젝트 설명 (영문/한글 혼합)
├── DEPLOYMENT_KR.md            # 배포 가이드 (한글)
├── 시작하기.md                  # 빠른 시작 가이드 (한글)
├── PROJECT_STRUCTURE.md        # 이 파일
│
├── .gitignore                  # Git 제외 파일 목록
├── vercel.json                 # Vercel 배포 설정
└── netlify.toml                # Netlify 배포 설정
```

## 🔑 핵심 파일 설명

### `/src/main.tsx`
React 애플리케이션의 진입점입니다. DOM에 App 컴포넌트를 마운트합니다.

### `/src/app/App.tsx`
메인 애플리케이션 컴포넌트입니다. Figma에서 가져온 디자인 컴포넌트를 렌더링합니다.

### `/src/imports/0메인디자인.tsx`
Figma에서 직접 가져온 메인 페이지 디자인입니다. 모든 UI 요소와 레이아웃이 포함되어 있습니다.

주요 섹션:
- 헤더 (로고, 언어 선택, 메뉴)
- 히어로 섹션 (메인 이미지 + "The Day of Rest" 문구)
- 객실 목록 (101호~104호)
- 특별 시설 (수영장, 피트니스, 라운지, 루프탑 가든)
- 관광 정보 (남이섬)
- 예약 버튼
- 푸터 (연락처, SNS)

### `/src/styles/`
#### `fonts.css`
웹사이트에서 사용하는 모든 폰트를 로드합니다:
- Noto Sans KR (한글 기본 폰트)
- Nanum Gothic (한글 제목 폰트)
- Inter (영문 폰트)
- Baloo Bhai 2 (영문 장식 폰트)

#### `theme.css`
디자인 시스템의 색상, 간격, 테마 변수를 정의합니다.

#### `tailwind.css`
Tailwind CSS 기본 스타일을 가져옵니다.

### `/index.html`
웹사이트의 HTML 진입점입니다. 메타 태그와 타이틀이 설정되어 있습니다.

### `/package.json`
프로젝트의 의존성과 스크립트를 관리합니다.

사용 가능한 명령어:
- `npm run dev` - 개발 서버 실행
- `npm run build` - 프로덕션 빌드
- `npm run preview` - 빌드 미리보기

## 🎨 디자인 컴포넌트 구조

`/src/imports/0메인디자인.tsx` 파일의 주요 컴포넌트:

```
Component1 (메인)
├── Component5 (헤더/메뉴)
├── Rectangle1 (히어로 이미지)
├── Component2 (예약 버튼)
├── Component6 (객실 목록)
│   ├── Frame33 (101호)
│   ├── Frame34 (102호)
│   ├── Frame35 (103호)
│   └── Frame36 (104호)
├── Frame24 (특별 시설)
│   └── Component4
│       ├── Frame23 (탭 메뉴)
│       └── Frame15 (수영장 정보)
├── Frame25 (관광 정보)
│   ├── Text (제목)
│   ├── Text1 (남이섬 정보)
│   └── Rectangle (남이섬 이미지)
└── Frame26 (푸터)
    └── Footer
        ├── Frame2 (회사 정보)
        └── Frame3 (링크 & SNS)
```

## 🔧 설정 파일

### `vite.config.ts`
Vite 빌드 도구의 설정:
- React 플러그인
- Tailwind CSS 플러그인
- 경로 alias 설정 (`@` → `./src`)

### `vercel.json`
Vercel 배포 시 SPA(Single Page Application) 라우팅 설정

### `netlify.toml`
Netlify 배포 시 빌드 및 리다이렉트 설정

### `public/.htaccess`
Apache 서버에 배포 시 필요한 설정:
- SPA 라우팅
- Gzip 압축
- 브라우저 캐싱
- 보안 헤더

## 📊 기술 스택

### 프론트엔드
- **React 18.3** - UI 라이브러리
- **TypeScript** - 타입 안전성
- **Tailwind CSS 4.1** - 유틸리티 CSS 프레임워크

### 빌드 도구
- **Vite 6.3** - 빠른 개발 서버 및 빌드 도구
- **PostCSS** - CSS 전처리

### UI 컴포넌트
- **Radix UI** - 접근성 좋은 기본 컴포넌트
- **Lucide React** - 아이콘

### 폰트
- **Google Fonts** - Noto Sans KR, Inter, Baloo Bhai 2
- **Nanum Fonts** - Nanum Gothic

## 🎯 주요 페이지/섹션

1. **헤더**
   - 로고: "SANGREEN"
   - 언어 선택: KO / EN
   - 햄버거 메뉴

2. **히어로 섹션**
   - 배경: 호텔 외관 이미지
   - 텍스트: "The Day of Rest."
   - 예약 버튼

3. **객실 목록**
   - 101호 ~ 104호
   - 각 객실 이미지
   - "Detail >" 링크

4. **특별 시설**
   - 탭 메뉴: Swimming Pool, Fitness, Lounge, Roof Top Garden
   - 각 시설 상세 정보
   - 이미지 갤러리

5. **관광 정보**
   - 남이섬 소개
   - 주소 및 거리 정보
   - "Read More" 버튼

6. **푸터**
   - 회사 정보
   - 연락처
   - 이용약관 링크
   - SNS 링크 (Instagram, Facebook)

## 🔍 개발 시 주의사항

### 1. 폰트 관련
- 폰트 파일은 `src/styles/fonts.css`에서만 import
- 새로운 폰트 추가 시 이 파일만 수정

### 2. 이미지 관련
- Figma asset은 `figma:asset/...` 형식으로 import
- 새로운 이미지는 `/public` 폴더에 추가
- 최적화된 이미지 사용 권장 (WebP)

### 3. 컴포넌트 수정
- Figma 디자인 컴포넌트(`0메인디자인.tsx`)는 가급적 직접 수정하지 말 것
- 기능 추가는 새로운 컴포넌트를 만들어 사용

### 4. 스타일링
- Tailwind 유틸리티 클래스 우선 사용
- 커스텀 스타일은 `theme.css` 변수 활용

## 📈 배포 후 구조

빌드 후 생성되는 `dist` 폴더 구조:

```
dist/
├── index.html              # 메인 HTML
├── assets/                 # 번들된 JS/CSS
│   ├── index-[hash].js    # 애플리케이션 코드
│   ├── index-[hash].css   # 스타일
│   └── [hash].png         # 최적화된 이미지들
└── vite.svg               # 파비콘
```

## 🚀 개발 워크플로우

1. **로컬 개발**: `npm run dev`
2. **변경사항 확인**: 브라우저에서 실시간 확인
3. **빌드 테스트**: `npm run build`
4. **미리보기**: `npm run preview`
5. **Git 커밋**: `git commit -m "메시지"`
6. **배포**: Git push → 자동 배포 (Vercel/Netlify)

## 💾 데이터베이스

현재 이 프로젝트는 정적 웹사이트입니다. 예약 시스템 등을 추가하려면:
- Supabase
- Firebase
- MongoDB Atlas
등의 백엔드 서비스 연동 필요

## 🔐 환경 변수

현재 환경 변수가 필요하지 않습니다. API 연동 시 `.env` 파일 생성:

```env
VITE_API_URL=https://api.example.com
VITE_API_KEY=your_api_key_here
```

## 📱 반응형 디자인

현재 디자인은 데스크톱 기준으로 제작되었습니다.
모바일 최적화가 필요한 경우:
1. Tailwind 반응형 클래스 추가 (`md:`, `lg:` 등)
2. 미디어 쿼리 활용
3. 모바일 전용 컴포넌트 생성

## 🎨 색상 팔레트

주요 색상 (theme.css 참조):
- 배경: `#ffffff` (흰색)
- 텍스트: `#000000` (검정)
- 서브텍스트: `#555555` (회색)
- 강조: `#0a0a0a` (다크)
- 푸터: `#dddbdb` (라이트 그레이)

## 📚 참고 문서

- [React 문서](https://react.dev)
- [Vite 문서](https://vitejs.dev)
- [Tailwind CSS 문서](https://tailwindcss.com)
- [TypeScript 문서](https://www.typescriptlang.org)
