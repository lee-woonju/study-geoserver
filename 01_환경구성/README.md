# 환경 구성
## 목적 
GeoServer 설치를 위한 Docker + CentOS7 환경 구성

## 사용 명령어
```bash
docker run -it --name geoserver -p 8080:8080 centos:7 /bin/bash
```

## java 설치
```bash
yum install -y java-aa-openjdk-devel
# 설치 확인
java -version
```

## 필수 패키지 설치
```bash
# 다운로드 도구, 압축 해제 도구 설치
yum install -y wget unzip
```

## GeoServer 다운로드
```bash
wget https://sourceforge.net/projects/geoserver/files/GeoServer/2.24.2/geoserver-2.24.2-bin.zip

# 압축해제
unzip geoserver-2.24.2-bin.zip -d /opt/geoserver
```

## 실행
```bash
cd /opt/geoserver/geoserver-2.24.2/bin
./startup.sh
```

## 실행 확인
localhost:8080/geoserver 
- 아이디 : admin
- 비밀번호 : geoserver (기본값, 운영 서버에서는 반드시 변경!)

## 트러블슈팅

### CentOS7 yum 미러 오류
**원인** : CentOS7이 2024년 6월 EOL로 공식 미러 서버 폐쇄
- EOL : End Of Life 수명종료

**오류 메세지**
"Could not resolve host: mirrorlist.centos.org; Unknown error"

**해결방법** 
- vault 아카이브 서버로 변경
```bash
sed -i 's/mirrorlist=/#mirrorlist=/g' /etc/yum.repos.d/CentOS-Base.repo
sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-Base.repo
```

