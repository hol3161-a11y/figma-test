# 산그린호텔 웹사이트 배포 가이드

## 📋 배포 전 체크리스트

- [ ] Node.js 18 이상 설치 확인
- [ ] 프로젝트 의존성 설치 완료 (`pnpm install` 또는 `npm install`)
- [ ] 로컬에서 정상 작동 확인 (`pnpm dev`)
- [ ] 빌드 테스트 완료 (`pnpm build`)

## 🚀 추천 배포 방법

### 방법 1: Vercel (가장 쉬운 방법)

**장점:**
- 무료 플랜 제공
- 자동 HTTPS 적용
- Git 연동 자동 배포
- 빠른 CDN
- 한국어 지원

**배포 단계:**

1. **GitHub에 코드 업로드**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/사용자명/저장소명.git
   git push -u origin main
   ```

2. **Vercel 배포**
   - https://vercel.com 접속
   - "Sign Up" 후 GitHub 계정으로 로그인
   - "Add New Project" 클릭
   - GitHub 저장소 선택
   - Framework Preset: "Vite" 자동 선택됨
   - "Deploy" 클릭
   - 완료! 자동으로 URL 생성됨 (예: `https://sangreen-hotel.vercel.app`)

3. **커스텀 도메인 연결** (선택사항)
   - Vercel 프로젝트 설정 > Domains
   - 도메인 입력 (예: `sangreen.co.kr`)
   - DNS 설정 안내에 따라 도메인 제공업체에서 설정

### 방법 2: Netlify

**장점:**
- 무료 플랜 제공
- 간단한 설정
- 자동 배포

**배포 단계:**

1. GitHub에 코드 업로드 (위와 동일)

2. **Netlify 배포**
   - https://netlify.com 접속
   - "Sign Up" 후 로그인
   - "Add new site" > "Import an existing project"
   - GitHub 저장소 선택
   - Build settings는 자동으로 설정됨:
     - Build command: `npm run build`
     - Publish directory: `dist`
   - "Deploy site" 클릭
   - 완료! URL 생성됨 (예: `https://sangreen-hotel.netlify.app`)

### 방법 3: 카페24 호스팅 (FTP)

**카페24나 다른 한국 호스팅 서비스를 이용하는 경우:**

1. **빌드 파일 생성**
   ```bash
   pnpm build
   ```
   → `dist` 폴더가 생성됩니다.

2. **FTP로 업로드**
   - FTP 클라이언트 (FileZilla 등) 설치
   - 호스팅 업체에서 제공한 FTP 정보로 접속
   - `dist` 폴더 안의 **모든 파일**을 `public_html` 또는 `www` 폴더에 업로드

3. **.htaccess 파일 추가** (중요!)
   
   루트 디렉토리에 `.htaccess` 파일 생성:
   ```apache
   <IfModule mod_rewrite.c>
     RewriteEngine On
     RewriteBase /
     RewriteRule ^index\.html$ - [L]
     RewriteCond %{REQUEST_FILENAME} !-f
     RewriteCond %{REQUEST_FILENAME} !-d
     RewriteRule . /index.html [L]
   </IfModule>
   ```

### 방법 4: GitHub Pages (무료)

1. **저장소 설정**
   - GitHub에서 저장소 Settings > Pages
   - Source: "GitHub Actions" 선택

2. **워크플로우 파일 생성**
   
   `.github/workflows/deploy.yml` 파일 생성:
   ```yaml
   name: Deploy to GitHub Pages

   on:
     push:
       branches: ['main']

   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v4
         - uses: actions/setup-node@v4
           with:
             node-version: 18
             cache: 'npm'
         - run: npm install
         - run: npm run build
         - uses: actions/upload-pages-artifact@v3
           with:
             path: ./dist

     deploy:
       needs: build
       runs-on: ubuntu-latest
       permissions:
         pages: write
         id-token: write
       environment:
         name: github-pages
         url: ${{ steps.deployment.outputs.page_url }}
       steps:
         - uses: actions/deploy-pages@v4
           id: deployment
   ```

3. **vite.config.ts 수정**
   ```typescript
   export default defineConfig({
     base: '/저장소이름/',
     // ... 나머지 설정
   })
   ```

4. Push하면 자동 배포됨

## 🔧 배포 후 확인사항

- [ ] 웹사이트가 정상적으로 로드되는지 확인
- [ ] 모든 이미지가 표시되는지 확인
- [ ] 한글 폰트가 제대로 적용되는지 확인
- [ ] 모바일에서도 정상 작동하는지 확인
- [ ] 페이지 로딩 속도 확인

## 🌐 도메인 연결하기

### Vercel/Netlify에 도메인 연결

1. **DNS 설정** (가비아, 후이즈 등)
   - A 레코드 또는 CNAME 레코드 추가
   - Vercel/Netlify에서 제공하는 IP 또는 도메인 입력

2. **SSL 인증서**
   - Vercel/Netlify에서 자동으로 Let's Encrypt SSL 적용됨
   - 별도 설정 불필요

### 일반 호스팅에 도메인 연결

1. 호스팅 업체의 도메인 연결 가이드 참고
2. DNS 설정은 호스팅 업체에서 제공
3. SSL 인증서는 별도 구매 또는 Let's Encrypt 사용

## ⚡ 성능 최적화 팁

1. **이미지 최적화**
   - Figma에서 export할 때 WebP 포맷 사용
   - 이미지 크기 압축 (TinyPNG 등 사용)

2. **폰트 로딩 최적화**
   - 현재 Google Fonts 사용 중 (이미 최적화됨)
   - 필요시 서브셋 폰트 사용

3. **CDN 활용**
   - Vercel/Netlify는 자동으로 CDN 적용됨

## 🐛 문제 해결

### 문제: 페이지 새로고침 시 404 에러

**해결방법:**
- `.htaccess` 파일 추가 (Apache)
- `vercel.json` 또는 `netlify.toml` 설정 확인
- 서버 설정에서 모든 경로를 index.html로 리다이렉트

### 문제: 한글이 깨져 보임

**해결방법:**
- 파일이 UTF-8로 인코딩되어 있는지 확인
- HTML에 `<meta charset="UTF-8" />` 포함 확인

### 문제: 이미지가 안 보임

**해결방법:**
- 이미지 경로 확인 (상대 경로 사용)
- `public` 폴더에 이미지가 있는지 확인
- 빌드 후 `dist` 폴더에 이미지가 포함되었는지 확인

### 문제: 빌드 실패

**해결방법:**
```bash
# node_modules 삭제 후 재설치
rm -rf node_modules
pnpm install

# 캐시 삭제
pnpm store prune

# 다시 빌드
pnpm build
```

## 📞 도움이 필요하신가요?

문제가 계속되면 다음을 확인하세요:
- Node.js 버전 확인: `node -v` (18.0 이상 필요)
- pnpm 버전 확인: `pnpm -v`
- 에러 메시지 전체 내용 확인

## 📊 배포 체크리스트

### 최초 배포
- [ ] 코드 GitHub에 업로드
- [ ] Vercel/Netlify 계정 생성
- [ ] 프로젝트 배포
- [ ] 배포 URL 확인
- [ ] 모든 기능 테스트

### 업데이트 배포
- [ ] 로컬에서 변경사항 테스트
- [ ] Git commit & push
- [ ] 자동 배포 완료 대기 (Vercel/Netlify)
- [ ] 배포된 사이트에서 변경사항 확인

## 🎉 배포 완료!

축하합니다! 산그린호텔 웹사이트가 성공적으로 배포되었습니다.

배포된 사이트를 친구들과 공유하고, 피드백을 받아보세요!
