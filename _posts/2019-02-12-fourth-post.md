---
title : "주피터 노트북 파일 import 하는 방법"
date : 2019-02-12 21:58
categories : jekyll update
---
<br/>
주피터 노트북의 장점 중 하나는 cell 별로 실행해서 결과를 볼 수 있다는 것이다.<br/>
그런데 데이터 분석 과정 중 실행 결과를 눈으로 확인해야 하는 작업이 많기 때문에,<br/>
노트북 파일 cell 수가 너무 많아져 전체적인 가독성이 떨어질 때가 많다.<br/>
<br/>
이에 따라, 일반적인 에디터에서 다른 .py 파일을 import 해서 사용하는 것처럼<br/>
.ipynb 파일도 import를 할 수 있으면 좋겠다는 생각을 했다.<br/>
그렇게 할 경우 class와 method를 하나의 .ipynb 파일에 모아놓고,<br/>
분석을 진행하는 .ipynb 와 분리시킬 수 있으므로 훨씬 편리할 것이다.<br/>
구글링을 통해 간편하고 좋은 방법을 찾아냈고, 이를 활용해 새로 코드를 작성해 테스트 해봤다.<br/>
아래에 그 내용을 정리한다.<br/>
<br/>

1. 먼저, 다른 곳에서 import 해 가져올 .ipynb 파일을 만든다. 본 예제에서는 간단한 Class 하나를 작성했다.
![target_class](https://github.com/muketer/muketer.github.io/blob/master/_posts/images/fourth_post/target_class.jpg?raw=true)

2. .ipynb 파일은 json 형식으로 구성돼 있다.(메모장 혹은 기타 에디터에서 .ipynb 파일을 열어보면 확인할 수 있다.)<br/>
import 할 .ipynb 파일을 json 형식으로 읽어들인다.<br/>
그리고 전체 cell('cells' key의 value 안에 code들이 담겨있다.) 중 'cell_type' key의 value가 'code'인 것들을 찾아 그 속에서 'source' key의 value를 string으로 변환( ''.join ), list에 저장한다.<br/>
이제 list에 저장된 각각의 code들 사이에 줄바꿈 문자('\n')를 넣어 하나의 string으로 묶고, 실행한다.
![import_exec](https://github.com/muketer/muketer.github.io/blob/master/_posts/images/fourth_post/import_exec.jpg?raw=true)

3. 이렇게 하면 불러온 .ipynb 파일 속의 코드들을 활용할 수 있게 되는데, import 한 .ipynb 파일 속 'Target' class가 정상적으로 저장된 것을 아래 그림과 같이 확인할 수 있다.
![import_whos](https://github.com/muketer/muketer.github.io/blob/master/_posts/images/fourth_post/import_whos.jpg?raw=true)

4. 이 class의 객체를 만들어 class variable 변수와 method call을 확인한 결과, 정상적으로 작동하는 것을 볼 수 있었다.
![import_check](https://github.com/muketer/muketer.github.io/blob/master/_posts/images/fourth_post/import_check.jpg?raw=true)

<hr />
- 참고
### [blog 'frhyme.code'](https://frhyme.github.io/other/import_ipynb/)