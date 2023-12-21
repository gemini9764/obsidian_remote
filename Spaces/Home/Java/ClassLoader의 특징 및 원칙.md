ClassLoader에 대해 찾아보면 3가지 원칙에 대해서 나온다. 

- **Delegation**
    - 어떠한 클래스 파일을 로딩할 때, 해당 로딩 요청이 부모 클래스 로더들로 거슬러 올라가 BootstrapClassLoader(최상위 ClassLoader)에 다다른 후 그 밑으로 로딩 요청을 수행 

![Delegation Principle (출처 : https://homoefficio.github.io/2018/10/13/Java-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%A1%9C%EB%8D%94-%ED%9B%91%EC%96%B4%EB%B3%B4%EA%B8%B0/)](https://blog.kakaocdn.net/dn/c3KCKI/btrIy9VOAx4/AsKM6HMqQVQTGgq5EECzM1/img.png)

- **Visibility**
    - 상위 Class Loader를 먼저 참조하는것에 이어서, Class Loader는 일종의 scope rule을 제공하는데,   
        Child Class Loader는 Parent Class Loader의 Class를 Delegation load request를 이용하여 찾을 수 있지만,   
        그 반대로 Parent가 Child가 Loading한 Class를 사용할 수는 없다. 

- **Uniqueness**
    - 하위 클래스로더는 상위 클래스로더가 로딩한 클래스를 다시 로딩하지 않게 해서  
        로딩된 클래스의 유일성을 보장하는 것이다.  
        유일성을 식별하는 기준은 클래스의 binary name

해당 원칙 이외의 특징

- **Unload Impossibility**
    - 클래스 로더에 의해 로딩된 클래스들은 JVM 상에서 삭제할 수 없다  
        Unloading 기능을 우회적으로 구현하는 방법은 Class를 로드한 Class Loader 자체를 삭제하고,  
        새로운 Class Loader를 만들어서 다시 Class를 로드하면, reload 되는 것처럼 작동하는 것이 된다.

- **Hierarchical**
    - 계층적 구조를 가지도록 생성(부모-자식의 관계)  
        부모 클래스 로더에서 자식 클래스 로더를 가지는 형태


#### **Java8** 

![Delegation Principle (출처 : https://homoefficio.github.io/2018/10/13/Java-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%A1%9C%EB%8D%94-%ED%9B%91%EC%96%B4%EB%B3%B4%EA%B8%B0/)](https://blog.kakaocdn.net/dn/nx3Rj/btrIy9hakVL/2Zs56hAI7kMwtDQd8Ubaj1/img.png)

Bootstrap Class Loader (Primordial Class Loader)

- 자바의 기본 클래스로더 중 최상위 클래스로더로서 parent ClassLoader가 존재하지 않음
- ${JAVA_HOME}/jre/lib/rt.jar에 담긴 JDK 클래스 파일을 로딩(다만, 옵션 -Xbootclasspath 옵션으로 path 수정 가능)
- Native C로 구현돼 있어, String.class.getClassLoader()는 그냥 null을 반환 ( 자바 코드에 의해서 instance화 불가)

Extension Class Loader

- BootstrapClassLoader를 parent로 가지고 있음
- ${JAVA_HOME}/jre/lib/ext 폴더나 java.ext.dirs 환경 변수로 지정된 폴더에 있는 클래스 파일을 로딩
- 자바로 구현되어 있으며, sun.misc.Launcher$ExtClassLoader로 구현되어있고, URLClassLoader를 상속
- 사용자의 classpath를 수정하지 않고 확장으로 쉽게 갈 수 있는 기능을 제공

System Class Loader (Application Class Loader)

- 자바의 -classpath(또는 -cp) 옵션이나, jar 파일 안에 있는 Manifest 파일의 Class-Path 속성 값으로 지정된 폴더에 있는 클래스 로딩 
- 개발자가 애플리케이션 구동을 위해 직접 작성한 대부분의 클래스는 여기서 로딩됨 
- ClassLoader.getSystemClassLoader()를 통해서 얻을 수 있음


#### **Java9**

Java9에서는 모듈 시스템이 도입되어 그에 맞춰 ClassLoader의 범위, 구현 내용이 바뀌었다

Hierarchy는 그대로고, 로드하는 디렉토리의 위치, ClassLoader의 Name정도가 변경되었다

![Delegation Principle (출처 : https://homoefficio.github.io/2018/10/13/Java-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%A1%9C%EB%8D%94-%ED%9B%91%EC%96%B4%EB%B3%B4%EA%B8%B0/)](https://blog.kakaocdn.net/dn/cuuB3g/btrIK8ueuTk/5OKSrqIpMhOLDIvIox4TR1/img.jpg)

Bootstrap Class Loader

- 모듈화 시스템 도입으로 ${JAVA_HOME}/jre/lib/rt.jar가 없어짐에 따라 로딩하는 클래스의 범위가 전반적으로 축소
    - 기존에 parent를 BootstrapClassLoader로 가지고 있던 ClassLoader의 경우 parent에 대한 수정이 필요 

 Platform Class Loader

- ${JAVA_HOME}/jre/lib/ext 폴더나 java.ext.dirs 환경 변수를 지원하지 않음
- Java SE의 모든 클래스와 JDK-specific run-time 클래스들을 여기서 로딩
- URLClassLoader를 상속받지 않은 ClassLoaders 클래스의 내부 static 클래스로 구현됨

System Class Loader

- classpath, modulepath에 있는 클래스 로딩


### ClassLoader 로딩 단계

ClassLoader가 class 파일을 로드하는 단계에 대해서 정리해보도록 하겠다

우선, 크게 3가지 단계로 나눈다

![Delegation Principle (출처 : https://homoefficio.github.io/2018/10/13/Java-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%A1%9C%EB%8D%94-%ED%9B%91%EC%96%B4%EB%B3%B4%EA%B8%B0/)](https://blog.kakaocdn.net/dn/bFsZgs/btrIPYxFvTb/qxRiJRg3KuJP2Y20oA2stk/img.png)

classLoading단계

#### **Loading**

- .class 파일을 읽어 내용에 따라 적절한 바이너리 데이터를 생성하고, 메서드 영역에 저장
    - 메서드 영역: 추후에 jvm의 구성 중, 데이터 영역에서 다룰 내용으로 자세한 설명은 생략   
                        Type정보(class, interface, enum) Method, 변수, FQCN이 저장되는 영역 
- 앞에서 설명한, ClassLoader의 계층구조 및 Delegation원칙에 따라서 Root ClassLoader에서부터 load가 필요한 class를 찾는다
- 로딩이 끝나면, Type 정보로 저장된 Class Type Object를 생성하여 Heap 영역에 저장

#### **Linking**

로딩 단계로부터 생성된 바이너리 데이터를 JVM의 런타임 데이터로 합치는 과정

이 단계는 3가지 단계로 나뉜다 

- Verifying
    - .class 파일의 정확성을 보장하기 위한 단계
    - 파일이 적절한 포맷인지, 유효한 컴파일러에 의해 생성되었는지를 확인
    - 검증이 실패한 경우 런타임 에러 (java.lang.VerifyError) 발생
- Preparing
    - 클래스 변수(static 변수)와 기본값에 필요한 메모리를 준비하는 과정

- Resolving
    - 심볼릭 메모리 레퍼런스를 메모리 영역에 존재하는 실제 레퍼런스로 교체
    - optional 한 단계 ( 설정에 따라서 동작 유무가 정해짐)

#### **Initializing**

- 윗 단계인 Linking의 Preparing 단계에서 확보한 메모리 영역에 static 값을 할당
- 클래스의 static 값들을 할당

---

실제 위의 3가지 단계가 실행되는 java의 ClassLoader API

- loadClass() : 지정된 이름을 가지는 클래스를 로드
    - 해당 메서드 내부에서 findLoadedClass() 호출 - 이미 로드된 내역이 있는지 확인 
- findClass() : loadClass시 load 된 class가 없을 시, load 하고자 하는 class의 이름으로 클래스 파일 탐색
- defineClass() : 위의 findClass메서드에서 원하는 class파일을 찾은 경우 .class 파일로부터 바이트 배열을 class객체로 변환

![Delegation Principle (출처 : https://homoefficio.github.io/2018/10/13/Java-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%A1%9C%EB%8D%94-%ED%9B%91%EC%96%B4%EB%B3%B4%EA%B8%B0/)](https://blog.kakaocdn.net/dn/lpNrp/btrIOvJvShB/6SXG7BQdGp9khFNeEGtrKk/img.png)

classLoader API