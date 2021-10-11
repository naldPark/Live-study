

# 1. JVM
## 1.1. JVM이란?
JVM이란 Java Virtual Machine, 자바 가상 머신의 약자를 따서 줄여 부르는 용어이다.
JVM의 역할은 자바 애플리케이션을 클래스 로더를 통해 읽어 들여 자바 API와 함께 실행하는 것이다.  그리고 JVM은 JAVA와 OS사이에서 중개자 역할을 수행하여
JAVA가 OS에 구애받지 않고 재사용을 가능하게 해준다.
그리고 가장 중요한 메모리관리, Garbage collection을 수행한다. 

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
  
![image](https://user-images.githubusercontent.com/81441317/136736758-16dc037d-91d7-49f1-a0d5-0749f67e1af3.png)
