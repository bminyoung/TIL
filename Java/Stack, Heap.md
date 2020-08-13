# Stack / Heap

### Stack
- primitive 타입이 저장된다. (실제 값과 함께 저장)
- heap에 저장된 변수의 레퍼런스가 저장된다.
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

### Heap
- Object 타입이 저장된다. (Object를 상속하는 String, List 등)
- 스레드 개수와 상관없이 heap영역은 하나다.
- stack에서 참조하지 않는 값은 GC에서 정리한다.
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
- [Immutable](./Immutable,%20Mutable.md)
- 위에서 2의 값을 가지는 Integer 객체는 GC에 의해 수집된다.