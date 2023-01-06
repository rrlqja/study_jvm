## GC - Garbage Collector
Jvm(Java Virtual Machine)에서 불필요한 메모리를 자동으로 정리해주는 기능  

* __Stop-the-world__  
GC 를 실행하기 위해 Jvm이 어플리케이션의 작동을 멈추는 행동.  
GC 튜닝이란 Stop-the-world 의 시간을 줄이는 것.  

* __Generational G__ 
  >대부분의 객체는 금방 접근 불가능 상태가 된다.  
  >오래된 객체에서 젊은 객체로의 참조는 아주 적게 존재한다.  

  이 두 가지 가설을 바탕으로 GC 를 효율적으로 동작하기 위해 HotSpot Jvm 에서는 메모리를 2개의 물리적 공간으로 나누었다.  
  이 2개의 영역은 Young/Old 영역이다. 이러한 방식을 Generational GC 라고 한다.  

* __Hotspot Heap Structure__  
Hotspot Jvm 의 Heap 메모리는 Young Generation 과 Old Generation 으로 나누어져있다.  
  
  * _Young Generation_  
  생성된지 얼마 안된 객체들이 저장되는 장소. Minor GC 로 사용되지 않는 객체가 제거된다.  
    
    * Eden  
    객체가 최초로 Heap 영역에 할당되는 장소.  
    
    * Survivor 0, Survivor 1  
    Eden 영역에서 살아남은 객체들이 저장되는 장소.  
  
  * _Old Generation_  
  생성된지 오래된 객체들이 저장되는 장소. Young Generation 에서 살아남은 객체가 옮겨온다. Full GC 로 사용되지 않는 객체가 제거된다. 
  
  * _Perm_  
  클래스의 메타정보, 메서드의 메타정보, Static 변 등이 저장되는 장소. Perm 영역이 일정수치 이상 가득 차면 OOM(Out Of Memory) 에러가 발생한다.  

* __Card Table__  
Old 영역의 객체가 Young 영역의 객체를 참조할 경우 Old 영역에있는 Card Table 에 표시한다. Minor GC 를 수행할 때 Old 영역의 모든 객체의 참조를 확인하지 않고 Card Table을 확인한다. 

* __Minor GC__  
Young 영역에 GC 가 발생하는 것.  
Micor GC 가 발생하면 Eden 과 Survivor 0 에서 사용되고 있는 객체를 Survivor 1 에 복사한다. 이후 Eden 과 Survivor 0 을 정리한다.  
다음 Minor GC 가 발생하면 Eden 과 Survivor 1 에서 살아있는 객체를 Survivor 0 에 복사하고 Eden 과 Survivor1을 정리한다.  
두 Survivor 영역중 한 곳은 반드시 비어있어야 한다. 
Minor GC 도 Stop-the-world 가 발생한다. 

* __Full GC__  
Old 영역에 GC 가 발생하는 것.  
Full GC 를 수행하는 여러 알고리즘이 존재한다.  
Full GC 는 속도가 매우 느리고 Stop-the-world가 발생한다.  
Full GC 는 성능과 안정성에 큰 영향을 끼친다. 

* __GC 파라미터__ 
  * _Heap 사이즈 조절_  
  Xms: 최소 Heap 사이즈, Xmx: 최대 Heap 사이즈  
  Xms 와 Xmx를 동일한 사이즈로 설정하면 일정한 크기의 힙 사이즈를 유지한다.  
  
  * _Perm 사이즈 조절_  
  어플리케이션에서 Out Of Memory 에러가 발생할 경우 Perm 사이즈를 의심해야된다. 
  
  * _New/Old 영역 크기 비율 조절_  
  
  * _Survivor 영역 조절_  
  
  * _Server/Client 옵션_  
  Server: 서버용 어플리케이션에 적합한 Jvm 옵션. 서버의 경우 New 객체들이 많이 발생한다. 따라서 상대적으로 Old 영역이 Young 영역보다 작다. 
  Client: 클라이언트용 어플리케이션에 적합한 Jvm 옵션. 하나의 클라이언트에서는 객체가 상대적으로 오래 살아남는다. 따라서 상대적으로 Old 영역이 Young 영역보다 크다.  
  
  * _GC 알고리즘 선택_  

