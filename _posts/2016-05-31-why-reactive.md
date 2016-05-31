---
layout: post
title: ReactiveX vs Rule Engine
modified:
categories: 
excerpt:
tags: []
image:
  feature:
date: 2016-05-31T17:40:26+09:00
---

# "ReactiveX" vs "Rule Engine"

이벤트를 처리하는데 이전까지는 "Rule Engine"을 주로 사용하였습니다. Open Source Project인 "Drools Fusion"을 사용하여 CEP(Complex Event Processing)이 쉽게 가능하였습니다. 그런데 이번에 "ReactiveX"를 도입하게 되었습니다. Java Base 코드이기 때문에 "RxJava"를 사용하게 되었습니다.

둘 다 이벤트 스트림 처리를 도와주는 프레임워크입니다. 굳이 둘을 동시에 사용할 필요가 있는가라는 생각도 들었습니다. 그것도 한순간. "ReactiveX" 프레임워크와  CEP 엔진의 특징을 이해하고 적절한 곳에 써야 한다는 결론에 이르렀습니다.

# Event Processing

먼저 이벤트 프로세싱에 대해서 정확한 정의가 필요합니다. 서버에서 이벤트를 사용하는 작업을 나열해보면 다음과 같습니다.

- CEP
- Monitoring
- Analysis
- Logging(Audit)
- Excuting a command

서버는 위에 나열된 작업들은 다양한 소스에서 이벤트를 받아서 이를 분석/모니터링하다가 특정한 조건/패턴을 찾습니다. 그리고 조건이 발견되면 사전에 정의된 액션을 실행하게 되는 것입니다.

이를 고려해보면 다음과 같이 크게 2가지 작업을 하고 있다고 정리할 수 있습니다.

- 이벤트 탬색 작업
    + CEP
    + Monitoring
    + Analysus
- 액션
    + Excuting a command
        * Logging
        * Audit


