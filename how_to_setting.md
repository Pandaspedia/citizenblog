# 로컬에 환경 설정하기

- CSS 관련
    - node 및 npm이 설치되어 있다는 것을 전제로 합니다
    - `assets/css/style.css`를 직접 수정하지 마세요! 
        - `assets/scss/` 아래의 파일들을 수정한 뒤 gulp를 통해서 처리해주면 됩니다
    - 로컬에 지킬이 설치되어 있지 않다면 `gulp sass` 로 전처리기만 실행시켜주세요
- Jekyll 관련
    - RVM 설치 후 원하는 루비 버전을 설치하고 지킬을 설치해주세요
    - github 페이지로만 작업하실거라면 굳이 지킬을 세팅할 필요는 없습니다!
    - 현재 gulp task는 지킬 build 하는 과정까지 포함되어 있습니다

```
# (Global) gulp 설치
npm install gulp -g

# 프로젝트 폴더에 gulp 설치
npm install gulp --save-dev

# gulp-sass 를 설치하는 과정에서 python2 를 찾지 못해 에러가 발생함
# conda로 python2 가상환경을 세팅
conda create -n python27 python=2.7
source activate python27

# 지킬 프로젝트 폴더 내부에 정의된 package.json 설치
npm install

# 전체 gulp task를 실행시킬 경우 (gulpfile.js 파일이 존재하는 위치에서)
# 현재 사용중인 테마는 jekyll 까지 integration 되어있음..
gulp

# 특정 gulp task를 실행시킬 경우
# gulp-taskname
# sass만 수행하자
gulp sass
```