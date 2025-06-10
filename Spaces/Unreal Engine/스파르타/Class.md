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
    - **public**
        - 외부에서 직접 접근 가능
        - 일반적으로 멤버 함수는 public
    - **private** (default)
        - 외부에서 직접 접근할 경우 컴파일 에러가 발생
        - 일반적으로 멤버 변수는 private

- getter와 setter
    - private에 있는 변수를 제어하기 위해 사용
    - 가져올 때 getter
    - 바꿀 때 setter
    - 어디서 값 변경을 했는지 명시적이다

```
#include <iostream>
#include <algorithm> //max 함수 사용
#include <string>

using namespace std;

class Student
{
public:
    //동작 정의(이를 멤버함수라고 합니다)
    double getAvg();
    int getMaxScore();

	void setMathScore(int math)
    {
        this->math = math;
    }
    void setEngScore(int eng)
    {
        this->eng = eng;
  
    }
    void setKorScore(int kor)
    {
        this->kor = kor;
    }

    int  getMathScore() { return math; }
    int  getEngScore() { return eng; }
    int  getKorScore() { return kor; }

private:
    //데이터 정의(이를 멤버변수라고 합니다.)
    int kor;
    int eng;
    int math;
};

double Student::getAvg()
{
    return (kor + eng + math) / 3.0;
}

int Student::getMaxScore()
{
    return max(max(kor, eng), math);
}

int main()
{
    Student s;

    s.setEngScore(32);
    s.setKorScore(52);
    s.setMathScore(74);

    //평균 최대점수 출력
    cout << s.getAvg() << endl;
    cout << s.getMaxScore() << endl;

    return 0;
}
```

- **생성자**
    - 객체를 생성할 때, 한 번 자동으로 호출되는 특별한 멤버 함수
    - 필요한 멤버 변수를 초기화하거나 객체가 동작할 준비를 하기 위해 사용
    - 반환형을 명시하지 않고, class 이름과 동일한 이름을 가진 함수

>정의된 class를 변수로 선언하면 해당 객체가 메모리에 올라간다<br>
>이를 **인스턴스화**라고 한다
{. prompt-info}

>객체가 생성될 때, 멤버 변수를 포함해서 필요한 정보들이 메모리에 올라간다<br>
>이 작업이 완료되면 생성자가 호출된다
{. prompt-info}

