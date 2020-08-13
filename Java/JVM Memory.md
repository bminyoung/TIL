# Java JVM Memory

- JVM 메모리 영역은 크게 다음과 같이 나눈다
	- Static(method) / Stack / Heap / PC Register / Native Method Stack

### Static 영역
- 런타임 상수 풀, Static 변수, 클래스와 메서드 정보 등을 저장한다.
- 스레드 개수와 상관없이 Static영역은 하나다.

### PC Register
- 스레드가 생성될 때 마다  생성되는 영역이다.
- 스레드가 실행되는 부분의 주소, 명령을 저장한다.

### Native method Stack
- 자바 외 언어의 메서드가 저장된다.

### Stack 영역
- primitive 타입이 저장된다. (실제 값과 함께 저장)
- Heap에 저장된 변수의 레퍼런스가 저장된다.
- 각 스레드마다 Stack을 갖는다.
```
int number = 10;
String str = "hello";

///// Stack /////      //////// Heap ///////////
/////////////////      /////////////////////////
//     str ----//----- //--> String : "hello" //
// number = 10 //      //                     //
/////////////////      /////////////////////////
```
- 해당 변수를 포함한 함수가 종료되면 Stack에 저장된 변수는 pop되어 해제된다.

### Heap 영역
- Object 타입이 저장된다. (Object를 상속하는 String, List 등)
- 스레드 개수와 상관없이 Heap영역은 하나다.
- Stack에서 참조하지 않는 값은 GC에서 정리한다.
- [String 예제](./String%20vs%20StringBuilder%20vs%20StringBuffer.md)

### Wrapper 클래스, String 이용 시 주의사항
```
void main(){
	List<Integer> list = new ArrayList<>();
	add(list, 1);
	// result : list = [1]
}
void add(List<Integer> list, int num){
	list.add(num);
}
```
- add 함수에서 수행한 내용이 main 함수의 list 객체에 적용이 된다

```
void main(){
	Integer number = 1;
	add(number, 1);
	// result : number = 1; (2가 아니다)
}
void add(Integer var, int num){
	var += num;
}
```
- add 함수에서 수행한 내용이 main 함수의 Integer 객체에 적용이 되지 않는다
```
///// Stack /////      //////// Heap ///////////
/////////////////      /////////////////////////
//             //      //                     //
//    number --//----- //-->   Integer : 1    //
/////////////////      /////////////////////////

<add 함수 실행 시>
///// Stack /////      //////// Heap ///////////
/////////////////      /////////////////////////
//     var   --//----- //-->   Integer : 2    //
//    number --//----- //-->   Integer : 1    //
/////////////////      /////////////////////////

<add 함수 종료 시> : var 변수가 pop 된다.
///// Stack /////      //////// Heap ///////////
/////////////////      /////////////////////////
//             //      //      Integer : 2    //
//    number --//----- //-->   Integer : 1    //
/////////////////      /////////////////////////
```
- Integer와 같은 Wrapper나 String 클래스는 Immutable이기 때문에 해당 객체의 값을 변경하는 것이 아니라 새로운 객체를 만든 후 레퍼런스를 변경하는 식이다.
- [Immutable](./Immutable%2C%20Mutable.md)
- 위에서 2의 값을 가지는 Integer 객체는 GC에 의해 수집된다.