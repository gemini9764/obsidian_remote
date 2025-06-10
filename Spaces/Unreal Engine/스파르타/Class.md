# Class

- class 멤버함수 구현(클래스 내부)

```
#include <iostream>
    #include <algorithm> //max 함수 사용
    #include <string>
    using namespace std;
    class Student
    {
        //동작 정의(이를 멤버함수라고 합니다)
        double getAvg()
        {
            return (kor + eng + math ) / 3.0; 
        }
        int getMax()
        {
            return max(max(kor, eng), math); 
        }
        
        //데이터 정의(이를 멤버변수라고 합니다.)
        int kor;
        int eng;
        int math;
    };
```

- class 멤버함수 구현(클래스 외부)

```
#include <iostream>
    #include <algorithm> //max 함수 사용
    #include <string>
    using namespace std;
    class Student
    {
        //동작 정의(이를 멤버함수라고 합니다)
        double getAvg();
        int getMaxNum();
        //데이터 정의(이를 멤버변수라고 합니다.)
        int kor;
        int eng;
        int math;
    };
    
    double Student::getAvg()
    {
        return (kor + eng + math) / 3.0;
    }
    int Student::getMaxNum()
    {
        return max(max(kor, eng), math);
        // 다른 방법 return max({ kor, eng, math });
    }
```

- 접근제어
    - 클래스의 멤버 함수나 변수에 접근할 때에, 객체 뒤에 멤버 접근 연산자 `.`을 사용한다