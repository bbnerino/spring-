# Collections Framework

Collections Framework 가 무엇인지 알아보기에 앞서 우리가 익숙한 리스트 배열을 어떻게 사용할 수 있는지 알아보도록 하자

#### ArrayList

---

원래 배열은 크기가 지정되어 있다. 그래서 이 크기를 벗어나면 오류가 생길 수 있다.
이 불편함을 컬렉션즈 프레임워크를 사용하면 줄어든다.

- 선언
  `ArrayList al = new ArrayList();`

- add : 추가 하기
  `al.add("one")`

- size : 배열의 개수

- get : al[1] 대신에 al.get(1)을 사용해야 한다.

- for 사용하기

```java
for (int a = 0; i<al.size(); i++ ){
  System.out.println(al.get(i)); => "one"
}
```

value를 따로 변수로 담아서 출력을 해보자

```java
for (int a = 0; i<al.size(); i++ ){
  String value = al.get(i); => 에러
  System.out.println(value);
}
```

왜 에러가 날까 ? =>
add 라는 메서드는 어떤 형태의 인자라도 넣을 수 있는데 사실 Object이다(Object가 모든 자료형의 시초이기 떄문)
그래서 `al.get(i)`는 Object 형태이기 때문에 이 값을 String으로 형변환을 해줘야한다.

```java
for (int a = 0; i<al.size(); i++ ){
  String value = (String)al.get(i);
  System.out.println(value);
}
```

`(String)al.get(i)` 이렇게 사용하면 안정성이 떨어진다.

그래서 요즘은 제네릭을 이용해서 ArrayList 자체의 형태를 지정한다.

#### 제네릭 지정

```java
ArrayList<String> al = new ArrayList<String>();
```

# Collections Framework

---

Collections Framework 아래에는 두가지의 카테고리가 있다.

#### Collection

- Set (중복 불가)

  - HashSet
  - LinkedHashSet
  - TreeSet

- List

  - ArrayList
  - Vector
  - LinkedList

- Queue
  - PriorityQueue

#### Map

key,value 가 있는 형식

- SortedMap
  - TreeMap
- HashTable
- LinkedHashMap
- HashMap

## Set,List의 차이점

---

- Set 선언 (HashSet)

```java
HashSet<Integer> hs = new HashSet<Integer>();
hs.add(1)
hs.add(1)
hs.add(2)
```

hs => 1,2

set은 중복 값이 포함이 되지 않는다는 특징이 있다.

#### Set

set은 집합이라는 의미로 집합과 관련된 메서드들이 있다.

`A.containsAll(B)` : B의 모든 값이 A에 포함된다 (부분집합)

`A.addAll(B)` : A와 B를 합쳐서 A를 만든다 (합집합)

`A.retainAll(B)` : A에도 있고 B에도 있는 값 (교집합)

`A.removeAll(B)` : A에서 B를 뺀다 (차집합)

## iterator()

list,set 둘 다 사용 가능
둘 다 Collection 인터페이스를 사용하고 있어서 iterator 를 사용할 수 있다.
반복자 : 컨테이너의 값들을 하나하나 반복하며 작업을 할 수 있게 해준다

Ex)

```java
HashSet<Integer> A = new HashSet<Integer>();
A.add(1);
A.add(2);
A.add(3);
Iterator hi = A.iterator();
while(hi.hasNext()){
  Sysout.out.println(hi.next());
}
```

Iterator 는 반복자로 A를 복사해왔다라는 느낌으로 받아드리면 되겠다.

- `hasNext()` = Iterator의 내용이 있는지 확인
- `next()` => pop이랑 비슷한 느낌으로 한개를 빼고 return 해준다.

# Map

key와 value 가 존재하는 형식
key 값은 중복되면 안되고, value는 중복되어도 된다.

Ex)

```java
HashMap<String,Integer> a = new HashMap<String,Integer> ();
a.put("one",1);
a.put("two",2);
a.put("three",3);
System.out.println(a.get("one"));
```

## Map for 문

`entrySet`을 이용해서 Map을 Set 형태로 만든다.
Set에 for를 사용하는데 , 여기서도 방법이 특이하기 때문에 주의한다.

```java
Set<Map.Entry<String,Integer>> entries = map.entrySet();
for(Map.Entry<String,Integer> entry:entries){
  System.out.println(entry.getKey()+entry.getValue())
}
```

Set 을 만드는데 `Map.Entry` 의 클래스 형태이다. 이 클래스 형태는 HashMap을 만들 때와 형식이 같다. 
- `for( something : somethings ){}`
  for는 앞이 단수형 뒤가 복수형이다. 
- `getKey()`,`getValue()`
  key와 value의 값을 찾는 메서드 

## 정렬 (sort)

`Collections.sort()`
sort는 list 형식의 데이터만 정렬해준다. 
  
하지만 그냥 list에 되는 것이 아니다.
`Comparable` 인터페이스이 구현된 클래스 형식에서만 사용이 가능하다.
`Comparable`는 compareTo 메서드를 구현하게 강제되고 있다. 

```java
class Computer implements Comparable{
  int serial;
  String owner;
  public int compareTo(Object o){
    return this.serial - ((Computer)o).serial;
  }
}
```
`compareTo`의 결과로는 양수 / 0 / 음수가 return 되고 이 값들을 토대로 정렬을 하게 된다. 
