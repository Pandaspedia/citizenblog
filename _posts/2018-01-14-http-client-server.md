---
layout: post
title: "HTTP 이해하기"
date: 2018-01-14
author: "박태민"
---

# HTTP 이해하기

HTTP란 무엇일까요?  저는 웹 개발을 처음 공부할 때 컴퓨터 네트워크에 대한 지식이 전혀 없었습니다. 모든 것은 HTTP라는 것 위에서 돌아간다고 하는데, 도대체 HTTP란 무엇일지가 너무 궁금했습니다. Google에서 HTTP라고 검색했을 때 가장 위에 나오는 것은 위키백과에 나오는 글입니다. 글의 서두를 한 번 가져와 보겠습니다.



> **HTTP**(**H**yper**T**ext **T**ransfer **P**rotocol, [문화어](https://ko.wikipedia.org/wiki/%EB%AC%B8%ED%99%94%EC%96%B4): 초본문전송규약, 하이퍼본문전송규약)는 [WWW](https://ko.wikipedia.org/wiki/WWW) 상에서 정보를 주고받을 수 있는 [프로토콜](https://ko.wikipedia.org/wiki/%ED%86%B5%EC%8B%A0_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)이다. 주로 [HTML](https://ko.wikipedia.org/wiki/HTML) 문서를 주고받는 데에 쓰인다. [TCP](https://ko.wikipedia.org/wiki/%EC%A0%84%EC%86%A1_%EC%A0%9C%EC%96%B4_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)와 [UDP](https://ko.wikipedia.org/wiki/%EC%82%AC%EC%9A%A9%EC%9E%90_%EB%8D%B0%EC%9D%B4%ED%84%B0%EA%B7%B8%EB%9E%A8_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)를 사용하며, 80번 포트를 사용한다. [1996년](https://ko.wikipedia.org/wiki/1996%EB%85%84) 버전 1.0, 그리고 [1999년](https://ko.wikipedia.org/wiki/1999%EB%85%84) 1.1이 각각 발표되었다.
>
> HTTP는 [클라이언트](https://ko.wikipedia.org/wiki/%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8)와 [서버](https://ko.wikipedia.org/wiki/%EC%84%9C%EB%B2%84) 사이에 이루어지는 요청/응답(request/response) 프로토콜이다. 예를 들면, 클라이언트인 [웹 브라우저](https://ko.wikipedia.org/wiki/%EC%9B%B9_%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80)가 HTTP를 통하여 서버로부터 웹페이지나 그림 정보를 요청하면, 서버는 이 요청에 응답하여 필요한 정보를 해당 사용자에게 전달하게 된다. 이 정보가 모니터와 같은 출력 장치를 통해 사용자에게 나타나는 것이다.



위의 글은 물론 HTTP가 무엇인지를 매우 잘 요악하고 있습니다. 그런데 이제 막 웹 개발을 공부하기 시작하기 시작한 사람들에게 위의 글은 그리 친절한 말이 아닐것입니다. 이 글에선 위의 글에 나온 몇몇 개념어들을 최대한 쉽게 풀어나가며 HTTP가 무엇인지 쉽게 알아보도록 하겠습니다.



## 프로토콜

HTTP는 웹 브라우저와 웹 서버가 서로 통신을 하기 위한 표준 프로토콜입니다. 여기서 프로토콜이란 말은 무엇일까요?  프로토콜이란 말을 사전에서 한 번 검색해보겠습니다.



> <컴퓨터> **컴퓨터와 컴퓨터 사이, 또는 한 장치와 다른 장치 사이에서 데이터를 원활히 주고받기 위하여 약속한 여러 가지 규약(規約). 이 규약에는 신호 송신의 순서, 데이터의 표현법, 오류 검출법 따위가 있다. [비슷한 말] 통신 규약.**



프로토콜이란 말은 곧 통신 규약이란 말입니다. 컴퓨터 네트워크에서 컴퓨터와 컴퓨터가 통신하기 위한 규약입니다. 아직 조금 모호한 것 같으니 조금 더 구체적으로 표현해보겠습니다. HTTP라는 프로토콜은 구체적으로 아래와 같은 내용을 담고 있습니다.

- 클라이언트와 서버가 연결을 맺는 방법
- 클라이언트가 서버에게 데이터를 요청하는 방법
- 서버가 요청에 응답하는 방법
- 연결을 종료하는 방법

조금은 명확해졌을까요? 컴퓨터 네트워크에서 HTTP라는 프로토콜이란 말은 구체적으로 위와 같은 것들을 담고 있다고 생각하시면 됩니다.



## 클라이언트 서버 모델

클라이언트와 서버 모델에 대해 기초적인 수준에서 가장 이해하기 쉽게 설명하는 것은 [생활코딩에 있는 이고잉님의 설명](https://opentutorials.org/course/1688/9408)이라고 생각합니다. 아직 클라이언트 서버 모델이라는 말을 처음 듣거나 아직 익숙하지 않으신 분은 먼저 링크를 참고하시어 설명을 한 번 듣는 것을 추천드립니다. 앞의 부분 6분 정도를 들으시면 됩니다.



![클라이언트 서버 모델](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c9/Client-server-model.svg/500px-Client-server-model.svg.png)



위의 그림은 클라이언트 서버 모델을 간단히 도식화해놓은 것입니다. 클라이언트 서버 모델이란 말은 클라이언트와 서버로 네트워크 아키텍쳐를 나누어 표현해놓은 것입니다. 

클라이언트는 고객이라는 뜻처럼 무언가 **요청(request)**을 하는 주체를 말합니다. 클라이언트가 브라우저라면 화면에 보여줄 자원들을 요청할 것이고 게임 클라이언트라면 게임의 진행을 위해 필요한 자원들을 요청할 것입니다. 

서버는 클라이언트가 보낸 요청에 대한 **응답(response)**을 제공하는 주체를 말합니다. 홈페이지를 운영하기 위한 서버이고 브라우저가 요청을 보냈다면 홈페이지를 화면에 보여주기 위한 자원들을 갖고 있다가 요청을 보낸 클라이언트에게 전달할 것입니다. 마찬가지로 게임을 운영하기 위한 서버라면 게임의 진행을 위해 필요한 자원들을 보관하고 있다가 요청을 보낸 클라이언트에게 전달할 것입니다. 



![클라이언트 서버 모델2](http://www.terms.co.kr/clientserver.gif)



예를 들어 위의 그림과 같은 상황을 가정해봅시다. 그림에서 고객은 자신의 거래 정보를 조회하기 자신의 PC에 있는 클라이언트 프로그램을 통하여 거래 서버에 조회 **요청(request)**을 보냅니다. 거래 서버 자체는 클라이언트의 거래 정보를 저장하고 있지 않습니다. 때문에 거래 서버는 거래 정보를 가져오기 위해 이를 저장하고 있는 데이터베이스 서버와 통신을 해 거래 정보를 가져 옵니다. 그리고 거래 서버는 이 정보를 **응답(response)**을 통해 고객의 클라이언트 프로그램에 전달함으로써 고객은 자신의 PC 화면에서 자신의 거래 정보를 볼 수 있습니다. 위의 자료는 오래된 자료이긴 하나 현대의 웹 서비스 아키텍쳐 또한 크게 다르지 않습니다.



# 다시 HTTP란?

간단히 프로토콜이라는 말과 클라이언트/서버라는 말에 대하여 알아보았습니다. 위키백과에서 나온 글을 다시 한 번 볼까요?



> **HTTP**(**H**yper**T**ext **T**ransfer **P**rotocol, [문화어](https://ko.wikipedia.org/wiki/%EB%AC%B8%ED%99%94%EC%96%B4): 초본문전송규약, 하이퍼본문전송규약)는 [WWW](https://ko.wikipedia.org/wiki/WWW) 상에서 정보를 주고받을 수 있는 [프로토콜](https://ko.wikipedia.org/wiki/%ED%86%B5%EC%8B%A0_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)이다. 주로 [HTML](https://ko.wikipedia.org/wiki/HTML) 문서를 주고받는 데에 쓰인다. [TCP](https://ko.wikipedia.org/wiki/%EC%A0%84%EC%86%A1_%EC%A0%9C%EC%96%B4_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)와 [UDP](https://ko.wikipedia.org/wiki/%EC%82%AC%EC%9A%A9%EC%9E%90_%EB%8D%B0%EC%9D%B4%ED%84%B0%EA%B7%B8%EB%9E%A8_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)를 사용하며, 80번 포트를 사용한다. [1996년](https://ko.wikipedia.org/wiki/1996%EB%85%84) 버전 1.0, 그리고 [1999년](https://ko.wikipedia.org/wiki/1999%EB%85%84) 1.1이 각각 발표되었다.
>
> HTTP는 [클라이언트](https://ko.wikipedia.org/wiki/%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8)와 [서버](https://ko.wikipedia.org/wiki/%EC%84%9C%EB%B2%84) 사이에 이루어지는 요청/응답(request/response) 프로토콜이다. 예를 들면, 클라이언트인 [웹 브라우저](https://ko.wikipedia.org/wiki/%EC%9B%B9_%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80)가 HTTP를 통하여 서버로부터 웹페이지나 그림 정보를 요청하면, 서버는 이 요청에 응답하여 필요한 정보를 해당 사용자에게 전달하게 된다. 이 정보가 모니터와 같은 출력 장치를 통해 사용자에게 나타나는 것이다.



아까보다는 위 글에 대해 조금 더 잘 이해가 될 것이라고 생각합니다. 



![HTTP](https://mdn.mozillademos.org/files/13673/HTTP%20&%20layers.png)



HTTP란 결국 HTML 문서와 같은 자원(resource) 들을 가져올 수 있게 해주는 프로토콜입니다. 클라이언트-서버 모델 상에서 모든 데이터 교환의 기초로 위의 그림 에서와 같이 위치합니다. 네트워크 용어로 말하면 응용 계층(Application Layer)에 속하는 프로토콜입니다.

이 문서에서 TCP, UDP 등 컴퓨터 네트워크에 관한 자세한 것을 다루기에는 무리가 있습니다. 이와 관련된 것은 컴퓨터 네트워크와 관련된 별도의 자료를 참고해주시길 바랍니다. 

이제 실제 HTTP 연결이 어떻게 이루어지는지, HTTP라는 것은 요청/응답(request/response) 프로토콜이라고 했는데 요청과 응답은 무엇인지 알아보도록 하겠습니다.



## HTTP 연결

그럼 실제로 HTTP 연결이 어떤 과정을 통해 이루어지는지 알아보겠습니다. HTTP 연결은 데이터 전송을 위해 TCP/IP 라는 네트워크 프로토콜을 이용합니다. 클라이언트가 서버로 보내는 각 요청은 아래의 4단계를 거칩니다.

1. 클라이언트가 서버의 HTTP 기본 포트 80에 대해 TCP 연결을 연다. 다른 포트 사용시 URL에 명시한다.
2. 클라이언트가 특정 경로에 위치한 리소스를 요청하는 메시지를 서버로 보낸다. 요청에는 헤더와 선택적으로 (요청의 성격에 따라 다르다) 빈 줄로 구분된 데이터가 포함된다.
3. 서버는 클라이언트에게 응답을 보낸다. 응답은 응답 코드로 시작하며, 메타데이터의 전체 헤더와 빈 줄 그리고 요청된 문서 또는 에러 메시지가 뒤따라온다.
4. 서버는 클라이언트와 연결을 종료한다.



## 요청(Request)

모든 요청과 응답은 기본적으로 같은 구조로 되어있습니다. 헤더 라인(header line)과 메타 데이터를 포함한 HTTP 헤더, 빈 줄, 그리고 메세지 본문으로 구성되어 있습니다. 일반적인 클라이언트의 요청을 하나 보도록 하겠습니다.

```
GET /index.html HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.8; rv:20.0)
 Gecko/20100101 Firefox/20.0
Host: en.wikipedia.org
Connection: keep-alive
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8

```

위의 요청은 HTTP GET의 요청입니다. 여기서 GET이란 것은 HTTP 메소드 중 하나이며 HTTP 메소드에 대해서는 Rest API를 다루는 글에서 자세히 설명하도록 하겠습니다. 이와 같은 GET 요청의 특징은 메시지의 본문이 없다는 것입니다. 마지막의 빈 줄로 요청의 끝을 나타냅니다. 그럼 한 줄 한줄 조금 더 자세히 살펴보도록 하겠습니다.

요청의 첫 줄 `GET /index.html HTTP/1.1` 은 요청 라인(request line)이라고 부르며 순서대로 HTTP 메소드, 리소스의 경로, HTTP 버전 정보를 담고 있습니다. 여기서 메소드는 요청 방식을 말합니다. GET은 일반적으로 자원(resource)의 반환을 요청할 때 사용하는 메소드입니다. /index.html은 서버에 요청된 자원의 경로를 나타내고 HTTP/1.1은 클라이언트가 지원하는 프로토콜의 버전을 의미합니다.

다음에 오는 것들이 헤더입니다. 헤더 각각에 대한 내용은 다루지 않고 헤더가 어떻게 구성되는 지에 대해 알아보도록 하겠습니다. GET 방식의 HTTP 요청은 요청 라인만 있어도 충분하지만, 일반적으로 클라이언트는 헤더에 추가 정보들을 담아서 서버에 요청합니다. 각 라인은 위에서 보이는 바와 같이 `Keyword: Value` 형식으로 되어있습니다. 키워드(Keyword)는 대소문자를 구분하지 않습니다. 그러나 값(Value)는 경우에 따라 대소문자를 구분하기도 합니다. 키워드와 값 둘 모두 아스키만 허용하며, 값이 너무 긴 경우 다음 줄의 시작 위치에 스페이스나 탭을 입력한 뒤 계속해서 입력할 수 있습니다. 헤더의 각 `Keyword: Value` 는 캐리지리턴과 라인피드의 쌍(\r\n)으로 끝납니다.

요청의 끝은 하나의 빈 줄로 끝납니다. 즉, 두 번의 캐리지리턴, 파인피드 쌍(\r\n\r\n)으로 끝납니다.



HTTP GET 요청 외에 PUT, POST 등의 메소드도 있습니다. 이 메소드들의 경우 GET과 달리 아래의 네 가지 항목을 순서대로 보냅니다.

1. 메소드, 경로 그리고 쿼리 문자열과 HTTP 버전을 포함하고 있는 시작 라인
2. HTTP 헤더
3. 빈 줄(두 번의 연속적인 캐리지리턴/라인피드 쌍)
4. 본문

일반적인 POST 요청을 하나 보도록 하겠습니다.

```
POST /cgi-bin/register.pl HTTP 1.0
Date: Sun, 27 Apr 2013 12:32:36
Host: www.cafeaulait.org
Content-type: application/x-www-form-urlencoded
Content-length: 54

username=Elliotte+Harold&email=elharo%40ibiblio.org

```

중간에 빈줄 뒤에 요청 본문이 있는 것을 확인할 수 있습니다.



요청(request)을 그림으로 다시 한 번 정리해보며 요청에 대한 글을 마치겠습니다.

![요청](https://mdn.mozillademos.org/files/13687/HTTP_Request.png)



## 응답(Response)

요청을 받은 서버는 마지막 빈 줄(두 번의 캐리지 리턴, 라인피드 쌍)을 확인하는 즉시, 동일한 연결을 통해 클라이언트에게 응답을 보내기 시작합니다. 응답은 상태 라인(status line)으로 시작하고 이어서 요청 헤더와 동일한 `Keyword: Value` 구문을 사용하여 응답을 설명하는 헤더가 옵니다. 그리고 하나의 빈 줄과 요청된 리소스가 옵니다. 일반적으로 요청이 성공하였을 경우엔 아래와 같은 응답을 클라이언트에게 보내게 됩니다.

```
HTTP/1.1 200 OK
Date: Sun, 21 Apr 2013 15:12:46 GMT
Server: Apache
Connection: close
Content-Type: text/html; charset=ISO-8859-1
Content-length: 115

<html>
<head>
<title>
A Sample HTML file
</title>
</head>
<body>
The rest of the document goes here
</body>
</html>

```

첫 번째 줄은 `HTTP/1.1 200 OK` 서버가 사용하는 프로토콜과 응답 코드를 나타냅니다. 200 OK는 가장 일반적인 응답 코드이며, 요청이 성공적으로 처리되었음을 의미합니다. 다른 헤더는 각각 Keyword에 맞는 Value들을 나타냅니다. 그리고 빈 줄이 온 뒤에 요청한 html 문서가 있음을 볼 수 있습니다.

응답 코드는 각각이 의미가 있으며 자세한 내용은 참고 자료를 찾아보셔야 합니다. 단, HTTP 버전에 관계없이 응답 코드 맨 앞의 숫자에 해당하는 의미가 있습니다. 

- 100에서 199까지의 응답 코드는 항상 정보를 제공하는 용도로 사용됩니다. 
- 200에서 299까지는 항상 성공을 의미합니다.
- 300에서 399까지는 항상 전송 방향을 바꾸는(redirection) 용도로 사용됩니다.
- 400에서 499까지는 항상 클라이언트의 요청 에러를 나타냅니다.
- 500에서 599까지는 서버 에러를 나타냅니다.

응답(response)을 그림으로 다시 한 번 정리해보며 응답에 대한 글을 마치겠습니다.

![응답](https://mdn.mozillademos.org/files/13691/HTTP_Response.png)



# 마무리

이 글에선 HTTP에 대한 개념적인 이해를 하기 위해 반드시 필요한 개념을 설명해보려 했고 HTTP 자체에 대해 이해해보려 했습니다. 당연히 이 짧은 글로 HTTP 라는 프로토콜을 모두 담을 수는 없습니다. 당장 다루지 못한 주제들만 해도 HTTP 메소드, 쿠키, 세션, 캐시 등 매우 많습니다. 앞으로의 글을 통해 다룰 수 있는 주제들은 다루어보도록 하겠습니다.

HTTP에 대해 조금 더 나아가기 위한 자료로는 [MDN 문서](https://developer.mozilla.org/ko/docs/Web/HTTP) 의 튜토리얼 및 레퍼런스 자료들을 추천드립니다.



# 참고 자료 

- 위키백과, "HTTP", https://ko.wikipedia.org/wiki/HTTP 
- 네이버 사전, 프로토콜, http://krdic.naver.com/detail.nhn?docid=41018500
- 위키백과, "클라이언트 서버 모델", https://ko.wikipedia.org/wiki/%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8_%EC%84%9C%EB%B2%84_%EB%AA%A8%EB%8D%B8
- 텀즈, client/server ; 클라이언트/서버, http://www.terms.co.kr/clientserver.htm
- 앨리엇 러스티 해럴드 지음, 자바 네트워크 프로그래밍, 강성용 옮김, p211-p232
- MDN web docs, HTTP 개요, https://developer.mozilla.org/ko/docs/Web/HTTP/Overview

