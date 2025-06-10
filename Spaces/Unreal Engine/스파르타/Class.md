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