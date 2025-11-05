# 파일작성
## 1. docker yml작성
## 2. ssl 폴더 생성
    mkdir -p ssl
## 3. 자체 서명 인증서 생성
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout ssl/key.pem \
    -out ssl/cert.pem \
    -subj "/C=KR/ST=Seoul/L=Seoul/O=MyCompany/CN=localhost"

(또는 sudo certbot certonly --standalone -d your-domain.com)

## 4. nginx.conf 작성

# 실행
## 1. 프로젝트 구조 확인
jenkins-docker/
├── docker-compose.yml
├── nginx.conf
└── ssl/  (HTTPS 사용 시)
    ├── cert.pem
    └── key.pem

## 2. Jenkins 시작
docker-compose up -d

## 3. 로그 확인
docker-compose logs -f

## 4. 초기 비밀번호 확인
docker-compose exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
