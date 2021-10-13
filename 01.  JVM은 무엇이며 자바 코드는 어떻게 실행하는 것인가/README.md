

# 1. JVM
## 1.1. JVM이란?
JVM이란 Java Virtual Machine, 자바 가상 머신의 약자를 따서 줄여 부르는 용어이다.   
JVM의 역할은 자바 애플리케이션을 클래스 로더를 통해 읽어 들여 자바 API와 함께 실행하는 것이다.  그리고 JVM은 JAVA와 OS사이에서 중개자 역할을 수행하여 JAVA가 OS에 구애받지 않고 재사용을 가능하게 해준다.   
그리고 가장 중요한 메모리관리, Garbage collection을 수행한다. 
[간단요약]


## 1.2. 가상머신
### 1.2.1. 자바프로그램의 실행과정
	1. 프로그램이 실행되면 JVM은 OS로부터 이 프로그램이 필요로 하는 메모리를 할당받는다.
	   JVM은 이 메모리를 용도에 따라 여러 영역으로 나누어 관리한다.
	2. 자바 컴파일러(javac)가 자바 소스코드(.java)를 읽어들여 자바 바이트코드(.class)로 변환시킨다.
	3. Class Loader를 통해 class파일들을 JVM으로 로딩한다.
	4. 로딩된 class파일들은 Execution engine을 통해 해석된다.
	5. 해석된 바이트코드는 Runtime Data Areas에 배치되어 실질적인 수행이 이루어지게 된다.
	6. 이러한 실행과정 속에서 JVM은 필요에 따라 Thread Synchronization과 GC같은 관리작업을 수행한다.
	-------------------------------------------------------------------------------------------------
	[쉬운설명]
	1. 즉 코드 (.java 확장자 파일) 를 짠다 => 명령어를 나열한다
	2. .java 파일을 Java Compiler가 Java Byte Code인 .class 파일로 변환한다.
	3. .class를 가지고 JVM이 설치된 운영체제(리눅스, 윈도우 등)에 맞게 해석하고 실행한다.
	- 컴퓨터는 0과1(바이너리코드)밖에 모르는 바보다. 그래서 1차적으로 .class파일로 컴파일 하고 JVM을 통해 바이너리코드로 변환한다.
	- C언어의 경우 운영체제 별로 컴파일러가 있지만 Java는 JVM이 있기 떄문에 운영체제에 맞게 번역해 줌
	- C / C++은 컴파일 플랫폼과 타겟 플랫폼이 다를 경우, 프로그램이 동작하지 않는다. 그래서 크로스 컴파일이 필요
          크로스 컴파일 ( Cross Compile ) : 다른 환경으로 컴파일 하는 것 (리눅스 환경에서 윈도우로 컴파일)
  
![image](https://user-images.githubusercontent.com/81441317/136736758-16dc037d-91d7-49f1-a0d5-0749f67e1af3.png)

### 1.2.2. 자바 개발 환경
JVM은 사용자의 입장인지 개발자의 입장인지에 따라 설치범위가 다름 (사용자도 설치해야함)   
JRE - Java Runtime Environment(사용자) : 컴파일된 자바 프로그램을 실행시킬 수 있는 자바 환경 (라이브러리 파일 등)
JDK - Java Development Kit (개발자) : 자바 프로그래밍시 필요한 컴파일러 등 포함 (javac, java등)   

![image](https://user-images.githubusercontent.com/81441317/136776310-8e37e48b-a5d3-47f1-ae23-320cca814e50.png)

### 1.2.3. 자바 버전
Java SE : Java Standard Edition _ 웹개발과 무관한 버젼    
Java EE : Java EnterPrise Edition _ 웹개발에 필요한 버전

### 1.2.4. JDK 종류  
Oracle : 오라클에서 만든 JDK, 개인에게 무료, 기업용은 유료   
OpenJDK : Oracle JDK와 비슷한 성능, 언제나 무료   
참고: JAVA 8 부터 람다 지원 / LTS(Long Time Support)은 장기간에 걸처 지원하는 버전으로 안정적임 


## 1.3. JVM의 구조
### 1.3.1. JVM의 구성요소
![image](https://user-images.githubusercontent.com/81441317/137052829-2951af7c-e6d5-41d3-9d13-62e564c2b442.png)

### 1.3.2. [참고] 컴파일 단계

![image](https://user-images.githubusercontent.com/81441317/137052851-bd39f94e-36d3-4c97-90c1-c6ff8dc3b917.png)

### 1.3.3. Class Loader 로딩과정
![image](https://user-images.githubusercontent.com/81441317/137052870-0f75fb0b-9449-4c89-bff3-0e0ca45f512c.png)

### 1.3.4. Class Loader 계층구조
![image](https://user-images.githubusercontent.com/81441317/137052908-bb175d20-5da5-4533-84b6-66c494665015.png)

### 1.3.5. Runtime Data Areas
![image](https://user-images.githubusercontent.com/81441317/137052927-0d3df9ea-7f5a-4772-b5b4-073d5117a38f.png)
```
Method Area : 클래스 로더가 클래스파일을 읽어오면 클래스 정보를 파싱해서 해당 영역에 저장   
            (클래스 정보, 변수정보,  stati으로 선언한 변수가 저장)   	    
Heap : 프로그램을 실행하면서 생성한 모든 객체를 저장 ( ex. String, new연산으로 생성된 객체 등 )   
          GC (unreachable Object)의 대상이 되는 공간   	  
Stack: 지역변수, 메서드의 매개변수, 임시적인 변수, 메서드의 정보 저장   
PC Register: 스레드가 어떤 부분을 어떤 명령어로 수행할 지 저장   
Native Method Stacks: Java ByteCode가 아닌 다른언어로 작성된 메서드 ( c/c++ 등 성능향상을 목적으로 사용하는 경우가 있음 )

```
![image](https://user-images.githubusercontent.com/81441317/137053381-3ce59dd7-6582-4e07-a0f2-643f05cc16ca.png)


### 1.3.6. Heap (GC가 수행되는 영역)
![image](https://user-images.githubusercontent.com/81441317/137052944-6047d12c-85ff-4b47-a663-922dd2f891c5.png)
```
Young Generation :  
	  Eden: Object(객체)가 최초로 Heap에 할당되는 장소. Eden 영역이 가득 찼다면   
		Object의 참조 여부를 파악하고 Live Object는 Survivor 영역으로 이동.      
       		그리고 참조가 사라진 Garbage Object이면 남겨 놓고 
		모든 Live Object가 Survivor 영역으로 넘어가면 Eden 영역을 모두 청소.   

	Survivor:  Survivor0과 Survivor1로 구성. Eden 영역에 살아 남은 Object들이 잠시 머무르는 곳으로   
        	   Live Object들은 하나의 Survivor 영역만 사용하게 되며 이러한 과정을 Minor GC라고 함   

Old Generation :
	새로 Heap에 할당된 Object가 들어오는 것이 아닌, Survivor 영역에서 살아남아 오랫동안 참조 되었고 앞으로도 사용될 확률이 높은 Object들을 저장하는 영역.    
	Old Generation의 메모리가 충분하지 않으면 해당 영역에서 GC가 발생하는데 이를 Major GC라고 한다.(Tenured 영역에서 발행한 GC)   

Perm:
	Class Meta 정보나 Method의 메타 정보, static 변수와 상수 정보들이 저장되는 공간.   
        JAVA8 부터 Native Memory (Metaspace *) 영역으로 이동됨   
	* Metaspace 영역은 클래스 메타 데이터를 native 메모리에 저장하고 메모리가 부족할 경우 이를 자동으로 늘려주는 공간으로 Heap이 아닌 Native 메모리 영역으로 취급   
	(Heap 영역은 JVM에 의해 관리된 영역이며, Native 메모리는 OS 레벨에서 관리하는 영역으로 구분)
```


### 1.3.7. Execution Engine
![image](https://user-images.githubusercontent.com/81441317/137052953-81698032-47f5-4dee-a240-97cfa5c7841c.png)
*****
Interpreter : 명령어를 한줄한줄 해석하면서 실행   
JIT Complier : (Just In Time) 인터프리터의 단점을 보완하기 위한 것으로 프로그램을 실행하는 시점에서 필요한 부분만 컴파일하는 방식    
Native Method Interface (JNI) : JVM에 실행되는 코드 중 네이티브로 실행하는 것이 있다면 해당 네이티브 코드를 호출하거나 호출될 수 있도록 만든 프레임워크   
Native Method Libraries :  네이티브 메소드 실행에 필요한 라이브러리   
*****





