# 프론트엔드 배포 파이프라인
![public/aws-jw.drawio.png](public/aws-jw.drawio.png)

## 배포 인프라 구성
- GitHub Actions: CI/CD 파이프라인 실행
- IAM: AWS 리소스 접근 제어
- Amazon S3: 정적 웹사이트 호스팅
- CloudFront: CDN을 통한 전세계 콘텐츠 전송

## 배포 프로세스
1. main 브랜치에 코드가 push되면 GitHub Actions 워크플로우가 시작됩니다.
2. Node.js 환경에서 의존성을 설치하고 프로젝트를 빌드합니다.
3. AWS 인증 후 빌드된 산출물을 S3 버킷에 업로드합니다.
4. CloudFront를 통해 S3의 콘텐츠가 전세계 사용자에게 제공됩니다.
5. 배포 완료 시 CloudFront 캐시가 자동으로 갱신됩니다.


## 주요 링크

- S3 버킷 웹사이트 엔드포인트: http://aws-jw.s3-website-us-east-1.amazonaws.com/
- CloudFrount 배포 도메인 이름: https://d3oszvpz3ia0lt.cloudfront.net/

## 주요 개념

- `GitHub Actions과 CI/CD 도구`: GitHub에서 제공하는 자동화 도구로, 코드 변경사항이 발생할 때마다 자동으로 빌드, 테스트, 배포를 수행합니다. CI(지속적 통합)와 CD(지속적 배포)를 통해 개발 프로세스를 자동화합니다.
- `S3와 스토리지`: Amazon S3는 확장 가능한 클라우드 스토리지 서비스입니다. 이 프로젝트에서는 빌드된 정적 웹사이트 파일들을 호스팅하는 용도로 사용됩니다.
- `CloudFront와 CDN`:  CloudFront는 AWS의 CDN(콘텐츠 전송 네트워크) 서비스입니다. 전 세계 엣지 로케이션을 통해 S3에 저장된 콘텐츠를 사용자와 가까운 위치에서 빠르게 제공합니다.
- `캐시 무효화(Cache Invalidation)`: CloudFront는 성능 향상을 위해 콘텐츠를 캐싱합니다. 새로운 배포 시 이전 캐시를 삭제하여 사용자가 항상 최신 버전의 웹사이트를 볼 수 있도록 합니다.
- `Repository secret과 환경변수`: GitHub Repository에 안전하게 저장되는 민감한 설정 값들(AWS 인증 정보 등)입니다. 워크플로우 실행 시 이 값들을 환경변수로 사용하여 AWS 서비스에 접근합니다.