# Garbage Collection

## **Garbage Collection이란?**

사용자가 동적으로 할당한 메모리를 할당 해제해주는 것

## **동작 방식**

Heap 영역은 young, old 영역이 있고, 그 안에 에덴(1ea)과 서바이벌(2ea) 영역으로 나눠져있다. 메모리를 동적으로 할당하게 되면 에덴 영역에 할당이 되고, 에덴 영역이 일정 이상 차게 되면 GC가 일어나게 되어 모든 스레드가 Stop the world 발생하면서 작업이 멈추게 된다. 그리고 에덴 영역에 있는 참조 되지 않은 메모리를 할당 해제 해준 뒤 서바이벌 영역을 이동 시킨다. 이런 과정이 반복되어 서바이벌 영역도 꽉 차게 되면 Minor GC가 발생하게 되고 참조되고 있는 메모리들은 다시 old 영역으로 이동 시킵니다. 이 과정(Copy & Scavage)을 반복하며 GC가 동작하게 된다.

---

## **GC 동작 알고리즘**

## **Parallel GC**

- 자바는 멀티 스레드 환경을 지원하지만, 하나의 CPU에서는 동시에 하나의 스레드 밖에 수행할 수 없어서 예전에는 하나의 CPU에서만 GC를 수행하였지만 후에 하나의 CPU에서 동시에 여러 개의 스레드를 실행할 수 있는 하이퍼스레딩 기술이나 여러개의 CPU를 동시에 장착한 하드웨어의 보급으로 하나의 하드웨어에서 동시에 여러 개의 스레드를 수행할 수 있게 되었다.
- Parallel GC에는 크게 두 가지 종류의 옵션을 가지고 있는데, Low-pause 방식과 Throughput 방식이 있다.
- Low-pause 방식은 GC가 일어날 때 애플리케이션이 멈추는 현상을 최소화하는데 역점을 두었다.
- Throughput 방식의 Parallel GC는 마이너 GC가 발생하였을 때 되도록이면 신속하게 수행하도록 throughput에 중점을 두었다.

## **Concurrent GC**

- Full GC 즉, Old 영역을 GC하는데 시간이 길고 애플리케이션이 순간적으로 멈춰버리므로, 애플리케이션이 멈추는 현상을 최소화 하는 GC 방식이다.
- Full GC에 소요되는 작업을 애플리케이션을 멈추고 진행하는 것이 아니라, 일부는 애플리케이션이 돌아가는 단계에서 수행하고 최소한의 작업만을 애플리케이션이 멈췄을 때 수행하는 방식이다.

## **Incremental GC(Train GC)**

- Train GC라고도 불리는 GC 방식은 의도는 Full GC에서 의해서 애플리케이션이 멈추는 시간을 줄이기 위한 것이다.
- 작동은 Minor GC가 일어날 때마다 Old 영역을 조금씩 GC 해서 Full GC가 발생하는 횟수나 시간을 줄이는 방식이다.
- Incremental GC는 많은 자원을 소모하고 Minor GC를 자주 일으켜서, 그리고 Incremental GC를 사용한다고 Full GC가 없어지거나 그 횟수가 획기적으로 줄어드는 것이 아니다. 오히려 느려지는 경우가 많으므로 반드시 테스트를 거치고 사용해야한다.

---

## **JVM GC 튜닝**

**1. 어플리케이션의 종류 및 튜닝 목표값 설정**

- JVM 튜닝을 할 때 가장 중요한 것은 튜닝의 목표를 설정하는 것이다.
- 메모리를 적게 사용하는 것이 목표인지, GC 횟수를 줄이는 것이 목표인지, GC에 걸리는 시간이 문제인지, 애플리케이션의 성능(Throughput or Response Time) 향상이 목표인지를 먼저 정하고 나서 목표치에 근접하도록 JVM 파라미터를 조정하는 것이 필요하다.

**2. Heap 크기 및 Perm 크기 설정**

- -ms, -mx 옵션을 이용해서 힙 크기를 정한다. 일반적으로 서버 애플리케이션은 ms와 mx크기를 같게 하는 것이 메모리의 Growing와 Shrinking에 의한 불필요한 로드를 막을 수 있다.
- ms와 mx 크기를 다르게 하는 경우는 애플리케이션의 시간대별 메모리 사용량이 급격하게 변화가 있는 애플리케이션에 효과적이다.

**3. 테스트와 로그 분석**

- JVM 옵션에 GC로그를 수집하기 위한 -verbosegc 옵션을 적용한다.
- nGrinder와 같은 스트레스 테스트 도구로 애플리케이션에 스트레스를 주어서, 그 로그를 수집한다.
- 튜닝에 있어서 가장 중요한 것은 목표 산정이지만, 그만큼이나 중요한 것은 실제 튜닝한 파라미터가 애플리케이션에 어떤 영향을 주는지를 테스트 하는 것이다.

**4. Perm 크기 조정**

**5. GC 수행 시간 분석**

- Full GC가 일어나는 횟수가 많아서 Old 영역을 늘려주면, Full GC 가 일어나는 횟수가 줄어들 것이고, 반대로 Full GC 수행 시간은 늘어날 것이다.
- 특히 서버 애플리케이션은 Full GC가 일어날 때는 JVM 자체가 멈춰버리기 때문에 일정 시간동안 응답을 못하는 상태가 된다.
- 서버 애플리케이션에서 Full GC가 적게 일어나게 하고, Full GC 시간을 양쪽 다 줄이려면 Old 영역의 메모리를 줄이고 여러 개의 인스턴스를 동시에 띄워서 로드 밸런싱을 해주면 부하가 분산된다.
- 그렇게 되면, Full GC가 일어나는 횟수가 줄어들게 되며 Old 영역을 줄였기 때문에 Full GC가 수행되는 시간 또한 줄어든다.
- 그리고 하나의 서버 인스턴스가 멈춰있는 동안 로드 밸런싱이 되는 다른 서버가 응답하고 있기 때문에 Full GC로 인하여 애플리케이션이 멈추는 상황에서 받을 영향을 최소화 할 수 있다.

**6. 파라미터 변경**

- 각 영역의 허용 범위를 기준으로, Old 영역과 New 영역을 적절하게 조절한다.
- Perm 크기와 New 영역의 배분(Eden, Survivor) 영역을 조정한다.
- 가장 중요한 것은 Old 영역과 New 영역의 비율을 어떻게 조정하는가이다.
