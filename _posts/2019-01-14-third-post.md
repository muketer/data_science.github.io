---
title : "머신러닝 병렬 처리 - sklearn&ipyparallel&joblib"
date : 2019-01-14 16:35
categories : jekyll update
---

머신러닝을 하다보니 병렬 처리의 필요성이 느껴졌다.<br/>
그렇게 오래 걸릴 작업이 아닌 것 같은데 CPU Core를 하나만 쓰는 경우가 있었기 때문.<br/>
<br/>
아래에 간단한 병렬 처리 방법을 정리해 본다.<br/>
<br/>
1. install libraries
- <code>pip install ipyparallel</code>
- <code>pip install joblib</code>

2. start ipcluster engine
![ipcluster_start](https://github.com/muketer/muketer.github.io/blob/master/_posts/images/ipcluster_start.png?raw=true){: width="150%" height="150%"}

3. import class, module
![class&module_import](https://github.com/muketer/muketer.github.io/blob/master/_posts/images/class&module_import.png?raw=true){: width="150%" height="150%"}

4. apply codes
![apply_codes](https://github.com/muketer/muketer.github.io/blob/master/_posts/images/parallel_execute_code.png?raw=true){: width="150%" height="150%"}

5. verify cpu working
![cpu_status](https://github.com/muketer/muketer.github.io/blob/master/_posts/images/cpu_status.png?raw=true){: width="100%" height="100%"}
<br/>
분명 CPU의 코어들이 동시에 동작하는 것이 확인되긴 하지만,<br/>
솔직히 이 병렬 처리를 통해서 성능이 개선되는지에 대해서는 아직 의문이다.<br/>
CPU를 동작만 시키고 실제 연산을 Core들이 분담하지는 않는 건가 싶기도 하다...<br/>
다른 방법들을 더 알아봐야겠다.<br/>
<font color="red" size="5">
	* 정정<br/>
</font>
<font color="red" size="5">
	병렬 처리가 잘 되는 듯 하다.<br/>
	위 방법을 적용해 GradientBoostingRegressor 모델 성능을 cross validation 하는 코드를 실행한 결과,<br/>
	병렬 처리를 적용하기 전보다 약 1/2~1/4 정도 가량의 시간 단축 효과를 봤다.<br/>
</font>
<br/>
<hr />
- 참고
### [stack overflow](https://stackoverflow.com/questions/38601026/easy-way-to-use-parallel-options-of-scikit-learn-functions-on-hpc)
### [ipyparallel doc](https://ipyparallel.readthedocs.io/en/latest/process.html#parallel-process)