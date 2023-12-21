### **Dataview 플러그인 사용법**

앞서 Dataview를 소개하는 곳에서 쿼리문 예시를 보여드려서 이해하실 수도 있겠지만, 조금 더 자세하게 Dataview를 사용하는 방법에 대해서 알아보도록 하겠습니다.

#### **쿼리문의 구성**

````
```dataview
TABLE|LIST|TASK <field> [AS "Column Name"], <field>, ..., <field>
FROM <source> (like #tag or "folder")
WHERE <expression> (like 'field = value')
SORT <expression> [ASC/DESC] (like 'field ASC') 
```
Copy
````

1. 어떤 타입으로 무엇을?
2. 어디서?
3. 어떤 조건을?
4. 어떤 순으로?(옵션)

#### **3가지 표현 방식**

쿼리문 구성 중 **어떤 타입으로?**에 해당하는 3가지 표현방식입니다. Dataview 쿼리문의 첫번째 줄에는 반드시 3가지 타입 중 한개를 명시해야합니다.

1. TABLE
2. LIST
3. TASK

**TABLE 방식**

습관트래커에서도 보여드렸던 방식으로 표 형식입니다. 아래에서 다룰 Annotation에 따라서 어떤 컬럼을 보여줄지 Field를 선택합니다.

![](https://blog.kakaocdn.net/dn/bumQPT/btrpBDe8tXH/3qXBvziW3OEuWjhnY9kHmk/img.png)

````
```dataview
TABLE time-played, length, rating
FROM "games"
SORT rating desc
```
````

**LIST 형식**

리스트 형식은 어디에서?(`FROM`) 에 해당하는 보관함 내의 모든 노트를 조회해서 가져옵니다. 아래 쿼리문은 `#game/moba` 또는 `#game/crpg`라는 태그를 가지고 있는 모든 노트를 리스트 형식으로 가져옵니다.

````
```dataview
list from #game/moba or #game/crpg
```
````

![](Pasted image 20211129200230.png)

**TASK 형식**

Task 형식은 어디에서(`FROM`) 에 해당하는 노트 내에 존재하는 모든 체크박스들을 조회해서 가져옵니다. 아래 쿼리문은 즉 `#projects/active` 라고 되어 있는 노트 내의 모든 체크박스를 가져오는 것입니다.

````
```dataview
task from #projects/active
```
Copy
````

Dataview 플러그인은 DQL 이라는 dataview query language라는 쿼리 언어(그렇게 특별하게 다르지는 않습니다.)를 통해서 보관함내에 있는 노트에 접근을 해서 데이터를 가져오는 플러그인입니다. 따라서 **Dataview** 플러그인을 잘 사용하게 된다면 다른 툴을 사용하지 않고도 보관함 내의 우리가 작성한 정보를 잘 정리해줄 수 있는 것입니다.