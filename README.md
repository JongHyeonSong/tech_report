# 프로젝트명 : 우리아이 지킴이
* ### 목표 : 코로나 블루 대처를 위한 스마트 로봇 및 어플 개발  
최근에 전국 269만 초중고학생들이 학교에서 수업을 받고 있지만 10명 중 1명은 불안해서 또는 의심 증상이 있다는 이유로 학교에 가지 않고 있으며, 학교 전체가 등교를 미룬 곳도 800곳을 넘어서고 있다.  

이에 학부모의 불안이 고조되고 있는 현 상황에서 학부모들이 가정 및 직장에서 아이의 건강상태 및 심리상태를 비대면으로 모니터링을 하고, 아이들에게 친숙한 펭수로봇을 통해 질병관리본부에서 제작한 감염병예방수칙을 홍보하면서 아이들의 표정변화 등을 빅데이터 및 AI 기술을 적용한 시제품을 개발하기로했다.


<div>
<img src="https://user-images.githubusercontent.com/59993079/83984279-4e661b80-a96f-11ea-9b0f-1ec829fe85cb.jpg">
<img src="https://user-images.githubusercontent.com/59993079/83984286-558d2980-a96f-11ea-90f5-9332dd8d5cb5.jpg">
<img src="https://user-images.githubusercontent.com/59993079/83984291-5d4cce00-a96f-11ea-9ae8-1205f62aa0a3.jpg">
<img src="https://user-images.githubusercontent.com/59993079/83984292-6178eb80-a96f-11ea-8a10-7caabd9abf7e.jpg">
</div

------------------
# 프로젝트 담당업무
* Cross-Platform인 Kivy를 활용한 UI/UX 설계 및 구현
* 로봇에서 전송되는 정보를 활용한 빅데이터 시각화 설계 및 구현
* 아이들의 그림정보를 획득하여 AI분석을 위한 피쳐분석 설계 및 구현
* 관리자, 어린이, 부모용 로그인정보 DB설계 및 구현
* PySpark Linux 서버 시스템 Build
* PySpark를 활용한 정규표현식 기반의 정제 코드 빌드


  
#  Cross-Platform인 Kivy를 활용한 UI/UX 설계 및 구현 

* Kivy에는 자주쓰는 BoxLayout, GridLayout, FloatLayout등을 포함해 8개정도의 레이아웃을 가지고 있는데 각각 조금씩의 차이는 있지만 결국은 버튼이나 라벨등을 넣기위한 공간이라고 생각하면 됩니다.  
  그리고 이 레이아웃들은 공간을 특정한 크기가 아니라 비율로 나타내게 되는데 이것으로 인해 위에서 언급한 Kivy의 Flexible한 특성을 살려 여러Android기계에 쉽게 호환됩니다  
  
* Widget는 Kivy의 GUI 인터페이스의 기본 빌딩 블록으로써 Canvas화면에 그리는 데 사용할 수 있는 툴을 제공받았습니다. 이벤트를 수신하고 이에 동적으로 반응 하는데, 이때 다른 GUI 프로그램과 다르게 위치와 크기를 비율로 설정할 수 있어 어떤 장치에서든지 쉽게 호환되는 점이 마음에 들었습니다.   

<div><img src="https://user-images.githubusercontent.com/59993079/83984691-5626bf80-a971-11ea-8742-589022ae09ba.png"></div>  

* 여기서 widget의 크기가 0.5라고 되어있고, 이 말은 즉 부모 layer의 세로축 길이의 50%를 차지한다는 것이고 이는 widget의 크기를 static하지않고 dynamic하게 만들어 줬습니다.
* 응용 프로그램이 점점 복잡 해짐에 따라 widget 트리 구성과 Binding의 명시적인 선언이 상세하고 유지 관리가 어려운 것이 일반적인데 비해 kivy는 kv라는 자기만의 language를 제공해줍니다. 여기서 kivy는 각 widget마다 id를 지정하여 kv밖 python 파일에서 해당하는 widget을 컨트롤 할 수 있었고, 버튼 Call-Back 함수로 kv파일 외부에서도 kv파일을 컨트롤 할수 있었습니다
* 프로젝트 진행중 파일을 모듈화하던중에 파일을 분리하자 보통 root경로를 이용하여 python파일에서 작업하게 되는데 모듈이 떨어져 있으니 root경로가 원하는 경로로 설정되지 않았습니다. 처음에 내부클래스를 중첩으로 쌓아서 원하는 widget에 접근하려고했으나 실패했고, 그냥 단순하게 상위,하위 widget에 접근하고해야겠다는 생각이 들어 documentation을 보았고 kivy위젯의 parent, children 속성을 발견하고, 이용해 다시 id에 접근할수있었습니다
  
 
# 로봇에서 전송되는 정보를 정규식으로 parsing하기

* 로봇에서 json 형태로 데이터가 날아오고 처음에는 list를 다루듯이 split함수와 join, 그리고 조건문을 사용하여 데이터를 parse하려고 시도하였으나 모든 예외 사항을 기술할 수 없었고 python의 Regular Expression을 이용하여 주민등록번호를 추출하기로 했습니다.  

첫째로 주민등록번호 앞6자리 생년월일을 기술하고 싶어서 숫자에 관한 정규식 표현을 찾아보았고 두가지 표현이 가능 했습니다. 첫째는 ‘\d’ 로 digit의 약자 즉 0~9의 숫자를 표현 하는것이었습니다. d앞에 \가 붙은 이유는 영문자 그대로의d와 메타문자로써 쓰고싶은 d를 구분하고 싶기 때문입니다. 이는 파이썬에서 경로를 따올 때 역슬래쉬가 붙은 경로를 일일이 수정한 경험이 있어서 받아들이는데 어렵지 않았습니다.  
  숫자의 두 번째 표현방법은 [0\~9]입니다. 여기는 두가지 정규식 개념이 섞어있는데 하나는 ‘[]’와 또하나는 ‘~’입니다 대괄호는 [ab] 괄호 안의 문자가 여럿중 아무거나 와도 된다는 의미고 0~9는 0부터9까지 연속되는 숫자의 모음이라는 의미입니다. 고로[0~9]는 0~9까지숫자중 하나의 숫자, 즉 숫자 하나를 의미합니다.  
  
* 생년월일의 태어난 연도는 \d\d로 표현할수 있고 \d{2}로 표현할 수도있는데 뒤의 {}표현은 바로 앞에 나온 패턴, 즉 숫자하나가 나오는 패턴을 2번 반복하겠다는 의미로써 자주 다뤄보게 되었습니다.      
태어난 달을 구하기 위해서는 (0[1-9]|1[0-2]) 패턴을 쓰게 되는됩니다. 왼쪽 오른쪽 패턴이 | 표현으로 나뉘어져 있는데 이는 ‘또는’을 위미하는 ‘OR’로써 0[1~9]는 01~09월 OR 1[0~2]는 10~12월로 ‘|’ 구분자로 01~12까지 명시적으로 가능한 달만 뽑아낼수 있었습니다. 같은 방식을 적용하여 다음의 정규식을 짰고  
‘^\d{2}(0[1-9]|1[0-2])(0[1-9]|[12][0-9]|[3][01])-[1][0-9]{6}$'  
이 정규식 표현으로 대량의 데이터에서 원하는 정보만을 뽑을 수 있었습니다.



# 로봇에서 전송되는 정보를 활용한 빅데이터 시각화 설계 및 구현


* 전송되는 데이터를 통해 시간 시각화의 한 종류인 막대그래프를 그리기로 했습니다. 시간에 따라 바뀌는 체온을 나타내고 싶었기에 정규식으로 체온 패턴을 ‘\d{2}\.\d'로 뽑아냈습니다. 그다음 pyspark sql 쿼리를 이용해 시간데이터를 시간단위로 groupby함수를 썼습니다.groupby 함수를 쓰게되면 groupby['컬럼명']으로 나머지 컬럼중 numeric한 자료들의 평균,합산등을 구할수있고, 이 프로젝트에서는 mean()함수를 통해 체온을 평균을 내주어서 각 x축을 시간단위, y축을 시간단위로 mean()하여 평균체온을 뽑아내 막대그래프를 그릴수 있었습니다


# 아이들의 그림정보를 획득하여 AI분석을 위한 피쳐분석 설계 및 구현

* OpenCV는 모듈 식 구조로 되어있어 패키지에 여러 개의 공유 라이브러리가 포함되어 있습니다. 모션 추정, 배경 감산 및 object 추적 알고리즘을 포함하는 비디오 분석 모듈인 Video 모듈을 통해 아이들의 그림으로부터 opencv 라이브러리를 통해 contour를 추출합니다. coutour란 동일한 색 또는 동일한 Color Intensity를 가진 부위의 가장자리 경계를 연결한 선입니다. 뽑아낸 contour중 점처럼 작은 contour는 if 조건문으로 제외하고 의미있는 크기를 가진 contour를 rentangle 함수로 좌표를 찾아 시각화고 특징 추출해서 그림 내에서 특정 피쳐를 뽑아낼 수 있었습니다.


# CAT검사와 비슷한 단어분석검사를 이용한 AI분석을 위한 피쳐분석 설계 및 구현 
* Word2Vec방법을 이용하였습니다. Word2Vec은 의미공간이라는 고차원 공간에 각 단어의 좌표값을 부여하는데 이 공간에서 각 좌표값의 숫자는 의미를 지니지 않습니다. 예를 들어 2차원 평면에서 비슷한 의미를 가지는 단어들은 비슷한 위치에 뭉쳐 있을것입니다. 이런 방법을 응용하여 10차원 혹은 그 이상의 벡터값을 로봇으로부터 받은 데이터의 단어로부터 추출하여 벡터공간에 모든 단어들을 입력합니다. 그러면 긍정적 의미를 지닌 단어들은 비슷한 의미를 지닌 단어들과 뭉쳐있을 것입니다. 그 벡터공간을 분석해서 지금 단어 벡터공간에서 가장 밀도가 높은 부분을 현재 아이의 감정상태로 추정 할 수 있습니다.


# docker image를 이용한 서버구축
*  Docker 이미지는 여러 계층으로 구성된 파일로 Docker 컨테이너에서 코드를 실행하는 데 사용됩니다. Docker 사용자가 이미지를 실행하면 그 이미지를 기반으로 컨테이너가 실행됩니다  

이미지를 컨테이너로 띄우면 컨테이너 내부에서 8888번으로 주피터 노트북을 호스팅 하고 있었는데 따로 포트포워딩을 해야 한다는 사실을 처음에 이해하지 못했습니다. 그래서 netstat -nap으로 내부 포트도 확인하고 외부 공유기 서버에도 접근하여 접속을 시도했지만 실패했고, 그 이후에 포트포워딩 개념을 공부하여 컨테이너를 run을 사용하여 실행할 때 -p옵션으로 제 호스트와 도커 컨테이너를 포트포워딩 할수있었습니다. 그 외에도 -it, --name, -v 같이 쉘이 접속하기, 컨테이너 이름정하기, 폴더마운팅하기 명령어를 익혔습니다



# PySpark를 기반으로 관리자, 어린이, 부모용 로그인정보 DB설계 및 구현
* pyspark RDD는 Resilient Distributed DataSet의 약자로 클러스터의 여러 시스템에 분산 된 데이터 요소의 분산 모음으로 Spark Core에서는 RDD는 변경할 수 없는(Immutable) 데이터의 집합으로 cluster 내의 여러 노드에 분산되있는 자료로써 최근까지 자주 쓰였던 스파크의 데이터 형식이었습니다. 하지만최근에는 pyspark dataFrame을 더 자주 사용해서 저도 dataframe을 이용하기로 했습니다. dataframe이 SparkSQL를 사용할수 있고 Schema로 구성된 분산 된 데이터 모음이기 때문입니다. 명명 된 열에 관리자, 어린이 등의 속성들을 정의하여 DB를 구축하고 DB를 다룰수 있도록 SPARK SQL을 제공해주어서 기본적으로 알고있는 sql구문을 적용하기가 수월했습니다.


# Hadoop, PySpark를 활용한 데이터 레이크 및 데이터 웨어하우스 설계 및 구현

* SparkSession은 Spark의 기초가 되는 function 들과 상호작용할 수 있게 해주는 접촉이으로써 DataFrame 과 Dataset APIs 를 사용하여 Spark 프로그래밍을 할 수 있도록 해 주는데 전송받은 데이터( dataStreaming,,json, sql, csv)를 스파크dataframe으로 처리하고 하둡의 HDFS 분산처리 시스템을 이용하여 저장합니다. hdfs는 Hadoop Distrebuted File System의 약자로 데이터를 분산저장하는데 데이터 덩어리를 일정 크기로 쪼개어 첫 번쨰 worker-node에 저장합니다. 그러면 첫 번째 node는 자신에게 저장된 데이터를 복제하여 옆 노드에게 넘겨주게되고 이 과정에서 하나의 노드가 down 되더라도 다른 노드에서 데이터를 받아올수 있도록 Fault tolerance를 설계할수있습니다


* PySpark는 다양한 소스로부터 실시간 스트리밍 데이터 처리가 가능한데 python의 TCP socketTextStream 통신을 이용해서 lambda 아키텍쳐를 구성합니다. lambda 아키텍쳐란 대량의 데이터를 실시간으로 분석하기 어려우니 batch로 미리 만든 데이터와 실시간 데이터를 혼합해서 사용하는 방식으로 batch로 일정주기마다 배치 뷰를 만들어 냅니다. 그리고 동일한 데이터를 실시간 데이터 처릴 통해 real-time 뷰를 만들다. 그리고 이 두개를 혼합해 분석을 할때 실시간 데이터가 반영된 분석을 할 수 있습니다.   
batch view를 만들어 내는곳은 Hadoop/HDFS, MR로 데이터를 저장하고 mapReduce로 데이터를 분석해서 batch view를 생성하고, real-time view를 생성하는 곳은 실시간 데이터에서 view를 생성하여 두 view를 비교할 수 있습니다.






# flask 웹앱 코딩파일을 클라우드 서버에 올리기
* 안드로이드앱과 연동되는 웹앱을 구현하기 위해서 파이썬의 웹 프레임워크중 하나인 flask를 이용하기로 했습니다. 플라스크의 가볍지만 커스텀이 가능한 특성 때문에 프로젝트에 더 잘 어울릴거라고 생각했고 서버로는 GCP클라우드를 이용하기로 결정했습니다.
작성한 파일을 클라우드 서버에 전송하기위해 filzilla를 이용하기로 했는데 여기서는 SSH 통신 개념을 이용해서 public key와 private key를 생성하고 public키는 통신하고자 하는 서버에 등록하고 자신이 클라이언트가 되어 private key를 가지고 서버와 통신합니다. 저는 
putty를 통해 공개키/비밀키를 생성하고 우분투서버와 통신해서 python 실행 파일을 옮겼습니다

# lask 서버를 호스팅하고 외부에서 접속하기
* flask 서버를 호스팅 했지만 외부 ip로 접속이 잘 되지 않았습니다. 처음에는 내부 포트포워딩이 문제인줄 알고 사설ip에서 공인ip 로 접근하여 내부 위부 포트 포워딩을 하려고 준비했으나 리눅스 명령어에 익숙하지 않아 성공하지 못했고, 이후 관련 Guide를 보니 클라우드 방화벽 설정을 필요로 하였고 flask의 default-port 인 5000번 포트를 열고나서 외부에서도 접근할 수 있는 웹서버 호스팅에 성공했습니다


# Docker & pyspark & hadoop
* ## Docker
   1. 도커는 컨테이너 기반의 오픈소스 가상화 플랫폼입니다.
  다양한 프로그램, 실행환경을 컨테이너로 추상화하고 동일한 인터페이스를 제공하여 프로그램의 배포 및 관리를 단순하게 해줍니다.  
  백엔드 프로그램, 데이터베이스 서버, 메시지 큐등 어떤 프로그램도 컨테이너로 추상화할 수 있고 조립PC, AWS, Azure, Google cloud등 어디에서든 실행할 수 있습니다.  
   2. **도커를 이용해서 pyspark와 jupyter notebook을 연동해놓은 이미지를 pull 해서 -p 포트 명령어로 내 현재 OS를 도커 내부 컨테이너의 jupyter-notebook으로 연결하여 간단한 서버를 구축할수 있었습니다. 특히 -p 포트 포워딩부분이 개념정리가 힘들었습니다. 이외에도 기본 명령어, -v 마운팅 --name 네이밍등 기본 명령어들을 익힐수 있었고 추후에 자기 프로젝트를 도커 이미지로 만들어 클라우드 서비스를 이용하여 호스팅 할 계획입니다**
 
* ## pyspark & hadoop
  1. 하둡은 대용량 데이터를 처리하는 새로운 패러다임이며
  그 핵심은 hdfs와 mapreduce이다
  2. hdfs란 Hadoop Distributed File System 의 약자로 여러 서버를 클러스터로 묶어 처리할 데이터를 분산 저장한다 또한 fault tolerance로써 데이터를 일정 단위로 쪼개어 클러스터에 첫번째 스토리지에 저장하고 첫 번째 스토리지는 동일한 데이터를 옆 서버의 스토리지에 저장하게 되어 특정 서버가 다운이 된다고 하더라도 데이터를 처리하는데 문제가 없게 합니다

  3. mapreduce란 분산저장과 비슷하게 데이터처리도 분산으로 하는 개념을 말합니다. map과 reduce과정으로 나뉘어져 있으며 map은 데이터들을 key,value로 모으고 key를 기준으로 정렬하여 reduce에 넘기게 됩니다 그러면 reduce에서는 key기준으로 단 하나의 value가 남을 때까지 reduce를 계속하여 작업합니다    
    **key를 아동 이름으로하고 value값을 체온이라고 놔뒀을때 key값을 기준으로 정렬한뒤에 reduce에서 value값이 하나가 남을때까지 평균치를 구해주면 마지막에 key,value값이 아동이름과 체온값1개로 reduce되어집니다**
  
  4. spark는 하둡과 같이 사용할수 있는데 하둡과 다르게 메모리 기반으로 데이터를 처리하여 하둡보다 훨씬 나은 성능을 기대할 수 있습니다 
  
 
  5. 
      spark에서도 dataframe형태를 제공합니다 pandas의 dataframe과 형식이나 문법이 비슷해서 적응하기가 상대적으로 쉬웠습니다.       
     평균 데이터를 구할일이 많아서 groupby함수와 mean()으로 groupby인자로 '시간데이터'를 주고 mean()함수로 평균온도를 구하여 시각화를 하려고 했습니다. 또한 sql문을 섞어 쓸 수 있어서 기본적인 CRUD 개념이 어렵지 않게 다가 왔습니다.    
     **sql문에서도 똑같이 groupby와 avg()함수로 원하는 데이터를 뽑을수 있었습니다 이번 프로젝트에서 하둡 클러스터링, master-node, worker-node등을 구축하지 못했는데 클라우드 시스템으로 하둡 시스템을 구축할 계획입니다**


# Reguler Expression

* 정규표현식의 사전적인 의미로는 특정한 규칙을 가진 문자열의 집합을 표현하는데 사용하는 형식 언어입니다.   
주로 Programming Language나 Text Editor 등 에서 문자열의 검색과 치환을 위한 용도로 쓰이고 있습니다.   
입력한 문자열에서 특정한 조건을 표현할 경우 일반적인 조건문으로는 다소 복잡할 수도 있지만, 정규표현식을 이용하면 매우 간단하게 표현 할 수 있습니다. 하지만 코드가 간단한 만큼 가독성이 떨어져서 표현식을 숙지하지 않으면 이해하기 힘들다는 문제점이 있습니다.

* #### 데이터에 적용하기
  * **정규식으로 아이들 체온데이터 찾아내기**  
  체온을 나타내는 데이터 형식이 36.8 이라고 하면 여기서 찾아낼 수 있는 정규표현식 패턴은 '\d{2}\.\d'로 데이터 내에서 모든 체온데이터를 찾을수 있습니다.
    \d는 digit으로써 0~9까지 숫자를 의미하고 {}안의 숫자는 바로앞 패턴이 몇번 반복되는가를 나타냅니다 그리고 소수점 '.'앞에 \가 붙은 이유는 소수점 자체가 정규표현식에서 특별한 의미(무슨 문자던지 다받는 joker같은 성질)를 가지고 있기 때문에 \.을 해주면 소수점 그대로를 찾아냅니다
  
  
  
  * **정규식으로 아이들 주민등록번호 찾아내기**  

      주민등록번호구성은 대부분 다음과 같습니다  
      
      123456 - 1234567  
      
      
      앞의 여섯자리는 차례대로 출생년도, 월, 일입니다 그리고 뒷자리 첫 번째 숫자는 성별을 나타냅니다.  
      월을 01-12월로 제한하고 일날짜를 01-31로 제한한다음 남자성별인 1만 찾아보도록 하겠습니다

      ‘^\d{2}(0[1-9]|1[0-2])(0[1-9]|[12][0-9]|[3][01])-[1][0-9]{6}$'

      맨 앞의 ‘^’는 패턴의 시작을 말하고 맨뒤의 ‘$’는 패턴의 끝을 의미합니다

      \d{2}는 출생년도를 찾기위한 패턴이고 \d라는 0~9를 의미하는 숫자가 {2}로 두 번 반복됩니다

      (0[1-9]|1[0-2])에서 0[1-9]는 01~09 월을 나타내고 바로 뒤에있는 ‘|’는 or을 나타내는 구분자입니다.  
      그리고 1[0-2]를 이용해서 출생월을 01-09 or 10-12로 한정 지을 수 있었습니다.  

      (0[1-9]|[12][0-9]|[3][01])에서는 위와 같은 방식으로 01-31일 이라는 특정한 날짜를 찾을수 있습니다.  

      -[1][0-9]{6} 부분은 주민등록번호 뒷자리로써 남자아이인 1을 찾기로 했으므로 1을 적었고 뒤에 나올 패턴은 아무숫자나6개가 나오면 됨으로 {6}을 써서 바로앞 패턴을 반복하였습니다.
