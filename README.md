# Kivy App

* 키비란
  *파이썬의 오픈소스 라이브러리로써 Multi-touch같은 유저인터페이스에 맞춰 설계된 어플리케이션 개발 툴이다
  *Flexible - 키비는 Android기반 스마트 폰 및 태블릿을 포함한 다양한 장치에서 실행될 수 있고 지원하는 모든 주요 운영 체제 (윈도우, 리눅스, OS X)에   빠르게 적응할 수 있습니다
  *Concentration - 키비는 몇 줄의 코드로 간단한 응용 프로그램을 작성할 수 있습니다. Kivy 프로그램은 파이썬 프로그래밍 언어를 사용하여 만들어 졌는데 , 정교한 사용자 인터페이스를 만들기 위해 자체 설명 언어 인 Kivy Language 를 제공합니다 이 언어를 사용하면 응용 프로그램 요소를 빠르게 설정, 연결 및 정렬 할 수 있습니다. 컴파일러 설정을 사용하는 것보다 응용 프로그램의 본질에 집중하게 해줍니다
  
2. Kivy의 레이아웃
#Kivy에는 자주쓰는 BoxLayout, GridLayout, FloatLayout등을 포함해 8개정도의 레이아웃을 가지고 있는데 각각 조금씩의 차이는 있지만 결국은 버튼이나 라벨등을 넣기위한 공간이라고 생각하면 됩니다 그리고 이 레이아웃들은 공간을 특정한 크기가 아니라 비율로 나타내게 되는데 이것으로 인해 위에서 언급한 Kivy의 Flexible한 특성을 살려 여러Android기계에 쉽게 호환됩니다

#앱을 개발할 때 GridLayout을 가장 많이 사용했고 레이아웃의 블록처럼 위젯을 쌓을 수 있는 기능을 이용해서, 완성된 앱의 GUI가 디바이스 화면 크기나 비율에 종속되지 않고 제가 만들고 생각했던 비율과 GUI가 구현 되었습니다

3. 키비의 .kv 확장자 언어와 python 실행파일과의 교류
#키비는 마치 HTML과 CSS처럼 논리적인 부분과 UI배치하는 부분을 python파일과 kv파일로 분리하여 작업하여 각각의 분야에 집중하여 개발할 수 있습니다

#위에서 말한대로 Kivy의 버튼이 위치하는곳은 UI영역이고 버튼의 동작 함수들의 구현은 python 파일 내에서 이루어집니다 그렇다면 함수들이 구현되는 python 스크립트 내에서 GUI를 구성하는 kv확장자 내에 영향을 줄 수 있어야 했고 세가지정도 방법이 있는데 저는 위젯마다 id를 배당해서 python파일 내에서 kv파일 내의 id에 접근하고 원하는 위젯들을 통제 했습니다
#코드 길이가 길어지면서 파일을 소분해야 했는데 그때 내부적으로 id에 접근하기가 어려워졌습니다. 그래서 추가로 다른 방법이 필요해졌고 kivy에서 제공하는 위젯사이의 parent, children 속성을 이용해 모듈로 떨어져 있어도 원하는 위젯에 접근이 가능해졌습니다
