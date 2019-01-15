---
title : "머신러닝 병렬 처리 - sklearn&ipyparallel&joblib"
date : 2019-01-14 16:35
categories : jekyll update
---

머신러닝을 하다보니 병렬 처리의 필요성이 느껴졌다.
그렇게 오래 걸릴 작업이 아닌 것 같은데 CPU Core를 하나만 쓰는 경우가 있었기 때문.

아래에 간단한 병렬 처리 방법을 정리해 본다.


1. install libraries
- > <code>pip install ipyparallel</code>
- > <code>pip install joblib</code>


2. start ipcluster engine
![ipcluster_start](https://github.com/muketer/muketer.github.io/blob/master/_posts/images/ipcluster_start.png?raw=true){: width="150%" height="150%"}

3. import class, module
![class&module_import](https://github.com/muketer/muketer.github.io/blob/master/_posts/images/class&module_import.png?raw=true){: width="150%" height="150%"}

4. apply codes
![apply_codes](https://github.com/muketer/muketer.github.io/blob/master/_posts/images/parallel_execute_code.png?raw=true){: width="150%" height="150%"}

5. verify cpu working
![cpu_status](https://github.com/muketer/muketer.github.io/blob/master/_posts/images/cpu_status.png?raw=true){: width="100%" height="100%"}


분명 CPU의 코어들이 동시에 동작하는 것이 확인되긴 하지만,
솔직히 이 병렬 처리를 통해서 성능이 개선되는지에 대해서는 아직 의문이다.
CPU를 동작만 시키고 실제 연산을 Core들이 분담하지는 않는 건가 싶기도 하다...
다른 방법들을 더 알아봐야겠다.


<hr />

- 참고
### [stack overflow](https://stackoverflow.com/questions/38601026/easy-way-to-use-parallel-options-of-scikit-learn-functions-on-hpc)
### [ipyparallel doc](https://ipyparallel.readthedocs.io/en/latest/process.html#parallel-process)