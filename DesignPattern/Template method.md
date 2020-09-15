# Template method Pattern
- 어떤 작업 수행 과정에서 공통되지 않은 부분을 따로 처리할 수 있다.
- 전체적인 흐름은 상위 클래스에서 제어할 수 있다.

## Example
```
abstract class Kimbap{
    abstract void doSomething();

    void cook(){
        System.out.println("=======");
        System.out.println("김");
        System.out.println("밥");
        System.out.println("단무지");
        doSomething();
        System.out.println("말기");
        System.out.println("=======");
    }
}

class TunaKimbap extends Kimbap{
    @Override
    void doSomething() {
        System.out.println("**참치**");
    }
}

class KimchiKimbap extends Kimbap{
    @Override
    void doSomething() {
        System.out.println("**김치**");
    }
}
...
public static void main(String[] args) {
    Kimbap kimbap = new TunaKimbap();
    kimbap.cook();
    
    kimbap = new KimchiKimbap();
    kimbap.cook();

    //=======
    //김
    //밥
    //단무지
    //**참치**
    //말기
    //=======
    //=======
    //김
    //밥
    //단무지
    //**김치**
    //말기
    //=======
```
- 김, 밥, 단무지, 말기 는 공통이므로 상위클래스에서 제어하고 공통되지 않은 부분(**)은 하위클래스에서 제어한다.