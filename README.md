## GC - Garbage Collector
JVM에서 불필요한 메모리를 자동으로 정리해주는 기능  

* __Stop-the-world__  
GC를 실행하기 위해 JVM이 어플리케이션의 작동을 멈추는 행동.  
GC튜닝이란 Stop-the-world의 시간을 줄이는 것.  

* __Generational Gc__
  >대부분의 객체는 금방 접근 불가능 상태가 된다.  
  >오래된 객체에서 젊은 객체로의 참조는 아주 적게 존재한다.  
이 두 가지 가설을 바탕으로 GC를 효율적으로 동작하기 위해 HotSpot JVM에서는 메모리를 2개의 물리적 공간으로 나누었다.  
이 2개의 영역은 Young/Old 영역이다. 이러한 방식을 Generational GC라고 한다.

* __Heap Structure__
