# 프로젝트 담당업무
* Cross-Platform인 Kivy를 활용한 UI/UX 설계 및 구현
* 로봇에서 전송되는 정보를 활용한 빅데이터 시각화 설계 및 구현
* 아이들의 그림정보를 획득하여 AI분석을 위한 피쳐분석 설계 및 구현
* 관리자, 어린이, 부모용 로그인정보 DB설계 및 구현
* PySpark Linux 서버 시스템 Build
* PySpark를 활용한 정규표현식 기반의 정제 코드 빌드

# Kivy App

* ## 키비란
  1. 파이썬의 오픈소스 라이브러리로써 Multi-touch같은 유저인터페이스에 맞춰 설계된 어플리케이션 개발 툴이다  
  2. Flexible - 키비는 Android기반 스마트 폰 및 태블릿을 포함한 다양한 장치에서 실행될 수 있고 지원하는 모든 주요 운영 체제 (윈도우, 리눅스, OS X)에 빠르게 적응할 수 있습니다  
  3. Concentration - 키비는 몇 줄의 코드로 간단한 응용 프로그램을 작성할 수 있습니다. Kivy 프로그램은 파이썬 프로그래밍 언어를 사용하여 만들어 졌는데 , 정교한 사용자 인터페이스를 만들기 위해 자체 설명 언어 인 Kivy Language 를 제공합니다 이 언어를 사용하면 응용 프로그램 요소를 빠르게 설정, 연결 및 정렬 할 수 있습니다. 컴파일러 설정을 사용하는 것보다 응용 프로그램의 본질에 집중하게 해줍니다  
  
* ## Kivy의 레이아웃
  1. Kivy에는 자주쓰는 BoxLayout, GridLayout, FloatLayout등을 포함해 8개정도의 레이아웃을 가지고 있는데 각각 조금씩의 차이는 있지만 결국은 버튼이나 라벨등을 넣기위한 공간이라고 생각하면 됩니다 그리고 이 레이아웃들은 공간을 특정한 크기가 아니라 비율로 나타내게 되는데 이것으로 인해 위에서 언급한 Kivy의 Flexible한 특성을 살려 여러Android기계에 쉽게 호환됩니다

  2. __**앱을 개발할 때 GridLayout을 가장 많이 사용했고 레이아웃의 블록처럼 위젯을 쌓을 수 있는 기능을 이용해서, 완성된 앱의 GUI가 디바이스 화면 크기나 비율에 종속되지 않고 제가 만들고 생각했던 비율과 GUI가 구현 되었습니다**__

* ## 키비의 .kv 확장자 언어와 python 실행파일과의 교류
  1. 키비는 마치 HTML과 CSS처럼 논리적인 부분과 UI배치하는 부분을 python파일과 kv파일로 분리하여 작업하여 각각의 분야에 집중하여 개발할 수 있습니다

  2. 위에서 말한대로 Kivy의 버튼이 위치하는곳은 UI영역이고 버튼의 동작 함수들의 구현은 python 파일 내에서 이루어집니다 그렇다면 함수들이 구현되는 python 스크립트 내에서 GUI를 구성하는 kv확장자 내에 영향을 줄 수 있어야 했고 세가지정도 방법이 있는데 저는 위젯마다 id를 배당해서 python파일 내에서 kv파일 내의 id에 접근하고 원하는 위젯들을 통제 했습니다
  3. __**코드 길이가 길어지면서 파일을 소분해야 했는데 그때 내부적으로 id에 접근하기가 어려워졌습니다. 그래서 추가로 다른 방법이 필요해졌고 kivy에서 제공하는 위젯사이의 parent, children 속성을 이용해 모듈로 떨어져 있어도 원하는 위젯에 접근이 가능해졌습니다**__

# Docker & pyspark & hadoop
* ## Docker
 1. 도커는 컨테이너 기반의 오픈소스 가상화 플랫폼입니다.
다양한 프로그램, 실행환경을 컨테이너로 추상화하고 동일한 인터페이스를 제공하여 프로그램의 배포 및 관리를 단순하게 해줍니다. 백엔드 프로그램, 데이터베이스 서버, 메시지 큐등 어떤 프로그램도 컨테이너로 추상화할 수 있고 조립PC, AWS, Azure, Google cloud등 어디에서든 실행할 수 있습니다.  
 2. **도커를 이용해서 pyspark와 jupyter notebook을 연동해놓은 이미지를 pull 해서 -p 포트 명령어로 내 현재 OS를 도커 내부 컨테이너의 jupyter-notebook으로 연결하여 간단한 서버를 구축할수 있었습니다 이외에도 기본 명령어 -p 포트, -v 마운팅 --name 네이밍등 기본 명령어들을 익힐수 있었고 추후에 자기 프로젝트를 도커 이미지로 만들어 클라우드 서비스를 이용하여 호스팅 할 계획입니다**
 
* ## pyspark & hadoop
  1. 하둡은 대용량 데이터를 처리하는 새로운 패러다임이며
  그 핵심은 hdfs와 mapreduce이다
  2. hdfs란 Hadoop Distributed File System 의 약자로 여러 서버를 클러스터로 묶어 처리할 데이터를 분산 저장한다 또한 fault tolerance로써 데이터를 일정 단위로 쪼개어 클러스터에 첫번째 스토리지에 저장하고 첫 번째 스토리지는 동일한 데이터를 옆 서버의 스토리지에 저장하게 되어 특정 서버가 다운이 된다고 하더라도 데이터를 처리하는데 문제가 없게 합니다

  3. mapreduce란 분산저장과 비슷하게 데이터처리도 분산으로 하는 개념을 말합니다. map과 reduce과정을 나뉘어져 있으며 map은 데이터들을 key,value로 모으고 key를 기준으로 정렬하여 reduce에 넘기게 됩니다 그러면 reduce에서는 key기준으로 단 하나의 value가 남을 때까지 reduce를 계속하여 작업합니다
  4. spark는 하둡과 같이 사용할수 있는데 하둡과 다르게 메모리 기반으로 데이터를 처리하여 하둡보다 훨씬 나은 성능을 기대할 수 있습니다 

  5. **spark에서도 dataframe형태를 제공합니다 pandas의 dataframe과 형식이나 문법이 비슷해서 적응하기가 상대적으로 쉬웠고 또한 sql문을 섞어 쓸 수 있어서 기본적인 CRUD 개념이 어렵지 않게 다가 왔습니다  이번 프로젝트에서 하둡 클러스터링, master-node, worker-node등을 구축하지 못했는데 클라우드 시스템으로 하둡 시스템을 구축할 계획입니다**


# Reguler Expression
