+++
title = "AWS+GO+Serverless 배포"
description = "빠르게 배포해보기"
tags = [
    "GO",
    "writing",
    "Serverless",
    "AWS",
]
date = "2024-02-04"
categories = [
    "Development",
    "writing",
]
menu = "main"
+++

# 2024년 2월
정신없이 흘러흘러 벌써 2월입니다. 듣거나 보거나 읽은 내용이 왕창 있는데 리뷰할 시간이 없어서 머리속 어딘가에 떠돌아다니는 기분이 듭니다.

예전에 일요일 저녁은 늘 밤을 샜던 기억이 있습니다. 월요일이 주로 논문 발표여서, 계속 미루다가ㅋㅋㅋ 일요일 저녁부터 시작해서 새벽에 끝나고 월요일에

랩 세미나를 가서 하루 종일 발표하고 질문 받고 답변하고, 기숙사 돌아가서 기절하는 날이라서. 이렇게 일요일 저녁에 몰아서 글을 쓰면 항상 그 때가 생각이 납니다.

아무튼, Go 행사에 참석해서 이런저런 세미나를 들었는데 가장 기억에 남았던 부분이 서버 없이 배포하는 파트입니다.

참석했던 go 행사의 핸즈온 세션 중에 서버 없이 배포하는 부분에 대해서 다시 한 번 정리할 겸 작성하겠습니다.



# 여러 가지 배포 방법 중에 Serverless 배포 방법
배포 방법에는 여러 가지가 있습니다.

로컬에서 작업해서 로컬 내에서만 확인하는 방법, 도커 이미지로 서버에 컨테이너 생성해서 배포하는 방법, 서버 내에서 직접 코드를 작성하는 방법 등이 있는데,

이 3가지 다 해본적이 있는데, serverless 프레임워크를 사용해서 배포하는 건 처음 해봤습니다. AWS lambda 방식도 안 해보긴 했죠,


# 1. Serverless Framework 란?

Serverless 프레임워크는 AWS Lambda, Azure Functions, Google Cloud Functions 등과 같은 다양한 서버리스 플랫폼에 코드를 배포하는 데 
사용되는 오픈 소스 도구입니다. 

이 프레임워크는 인프라를 코드(IaC) 방식으로 관리하여, 개발자가 인프라 설정에 드는 시간과 노력을 크게 줄여줍니다.


        serverless deploy


한 줄로 치켠 클라우드 환경에 배포됩니다. aws 뿐만 아니라. Azure 등에서도요. 

google map 관련해서도 예제가 있었는데(https://github.com/serverless/examples/tree/v3/aws-golang-googlemap) 이 부분도 좀 더 파고 싶었습니다.

 go, node.js, python, java, c#, Ruby, Swift, Kotlin, PHP, Scala 등을 지원합니다.

요약하면, Code와 인프라를 한번에 배포하는 게 특징인 프레임워크입니다.


# 2. Serverless + GO

를 사용하는 이유는 속도입니다.

정적 컴파일 언어인 GO는 실행이 매우 빠릅니다. go 사용하시는 분이 장점으로는 속도를 꼽죠.

에러를 컴파일 시점에서 발견할 수 있어서, 코드의 정확성을 유지하는데 도움이 되고, 운영 환경에서 사용하기에 적합하기 때문에

go와 serverless 를 사용하는 이유는 안전성과 속도라고 합니다.


# 사용 방법

사전에 go & npm 을 설치해야 합니다.
npm을 설치하는 방법은

    curl -qL https://www.npmjs.com/install.sh | sh

를 치면 됩니다.

- serverless 를 npm을 통해 설치합니다
  

    npm install -g serverless


    **에러가 난다면**


    sudo npm install -g serverless


    를 쳐서 권한을 sudo 권한으로 줍니다.

-  이제 serverless 프로젝트를 생성하면 됩니다.
예시 코드를 받아서 생성하고, AWS 인증 정보를 입력했었습니다.


      serverless create -t aws-go-mod -p myservice


1. serverless create: 이것은 Serverless 프레임워크의 'create' 명령을 호출합니다. 이 명령은 새로운 Serverless 서비스나 애플리케이션을 초기화하는 데 사용됩니다.

2. -t aws-go-mod: 여기서 -t는 'template'의 약자로, 사용할 템플릿을 지정합니다. aws-go-mod는 AWS Lambda를 위한 Go 언어를 사용하는 프로젝트 템플릿을 의미합니다. aws-go-mod 템플릿은 Go 모듈을 사용하는 AWS Lambda 함수를 위해 사전 구성된 파일과 설정을 포함하고 있습니다.

3. -p myservice: -p는 'path'의 약자로, 생성되는 서비스의 디렉토리 이름을 지정합니다. 이 경우, myservice라는 이름의 폴더가 생성되며, 그 안에 Serverless 프로젝트와 관련된 파일들이 위치하게 됩니다.

요약하자면, 

serverless create -t aws-go-mod -p myservice 명령은 

'myservice'라는 이름으로 새 Serverless 서비스를 생성하고, 

이 서비스는 AWS Lambda에서 Go 언어를 사용하는 템플릿을 기반으로 설정됩니다. 

이 명령을 실행한 후에는 생성된 'myservice' 디렉토리로 이동하여 개발을 시작할 수 있습니다.

그 다음 해당 폴더로 이동해줍니다.


      cd myservice
      make



추가로 aws-lamda-go 모듈을 다운로드 했습니다. 


      go mod download github.com/aws/aws-lambda-go



1. go mod: 이것은 Go 언어의 모듈 관리 시스템을 사용하는 명령입니다. Go 1.11 버전 이후로 도입된 이 시스템은 Go 프로젝트의 의존성 관리를 단순화하고 표준화합니다.

2. download: 이 부분은 go mod 시스템에게 특정 모듈을 다운로드하라는 지시를 합니다. 이 명령은 지정된 모듈의 소스 코드를 로컬 시스템에 다운로드하며, 의존성 트리에 있는 다른 필요한 모듈들도 함께 다운로드합니다.

3. github.com/aws/aws-lambda-go: 이것은 다운로드할 모듈의 경로입니다. github.com/aws/aws-lambda-go는 AWS Lambda를 위한 Go 언어 라이브러리이며, AWS Lambda에서 Go 언어로 작성된 함수를 개발할 때 필요한 여러 도구와 유틸리티를 제공합니다.

이 명령을 실행하면, Go의 모듈 시스템은 aws-lambda-go 라이브러리를 로컬 시스템에 다운로드하고, 프로젝트의 go.mod 파일에 이 의존성을 기록합니다. 이렇게 함으로써 Go 프로젝트가 AWS Lambda 환경에서 필요로 하는 기능들을 사용할 수 있게 됩니다.

AWS Lambda를 위한 Go 언어 라이브러리는 AWS에서 Lambda 함수를 쉽게 작성하고 배포할 수 있도록 도와주는 다양한 기능들을 포함하고 있어, AWS Lambda 환경에서 Go 언어를 사용하는 개발자에게 매우 유용합니다
  
-  배포


        make
        sls deply


- 참고로 중간에 AWS credential 인증도 해야 합니다. aws 설정에 들어가서 확인할 수 있습니다.

다음의 에러가 난다면 해당 사이트로 들어가세요

        [~][myservice][%][24-02-04][19:07] serverless deploy
    
        Deploying myservice to stage dev (us-east-1)
        
        ✖ Stack myservice-dev failed to deploy (2s)
        Environment: darwin, node 18.16.0, framework 3.38.0, plugin 7.2.0, SDK 4.5.1
        Docs:        docs.serverless.com
        Support:     forum.serverless.com
        Bugs:        github.com/serverless/serverless/issues
        
        Error:
        AWS provider credentials not found. Learn how to set up AWS provider credentials in our docs here: <http://slss.io/aws-creds-setup>.

특정 함수만 빠르게 배포하고 싶다면

        make
        sls deploy function --function 함수 이름


- 호출

        # Endpoint 호출
        curl -XGET $endpoint
        curl -XPOST $endpoint -H "Content-Type: text/plain" -d '$입력할 내용'


참고로 테스트한 go 파일은 하단 serverless 배포를 발표해주신 발표자 분의 깃허브 링크에 있습니다.
https://github.com/da-head0/aws-go-handson/blob/main/hello/main.go


# 마무리

Deep Learning 이나 Machine Learning을 쓰려고 했는데 go 언어 AWS 배포하는 걸 쓰게 됩니다...

Deep Learning 은... 뭔가 좀 막히는 부분이 있는데, 좀 막힌다 싶으면 좀 더 새로운 언어 등을 배우면서 환기를 하는 편입니다. (이열치열!)

그리고 go 언어와 서버리스 배포는 잘 쓰면 꽤 유용할 듯하여서 작성해보았습니다.

다음 주는 곧 설날 연휴입니다. 연휴에 연차 붙여서 쉬면서 또 이것 저것 할 것 같은 느낌적인 느낌이 듭니다.

새해 복 많이받으세🐉!
