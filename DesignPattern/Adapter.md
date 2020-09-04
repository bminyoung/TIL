# Adapter Pattern
- 클래스의 인터페이스를 다른 인터페이스로 변환시킬 수 있다.
- 호환성 때문에 같이 사용할 수 없는 클래스를 연결시킬 수 있다.
- 기존의 클래스를 변경하지 않고, 문제가 발생하면 어댑터 클래스만 수정하면 된다.

## Example
#### 1. 객체(인스턴스) 어댑터
```
interface Aclass{
    void Afunc();
}

interface Bclass{
    void Bfunc();
}

class AclassImpl implements Aclass{
    @Override
    public void Afunc() {
        System.out.println("function of Aclass");
    }
}

class BclassImpl implements  Bclass{
    @Override
    public void Bfunc() {
        System.out.println("function of Bclass");
    }
}

// Bclass -> Aclass
class Adapter implements Aclass {
    Bclass bClass;
    Adapter(Bclass bClass){
        this.bClass = bClass;
    }

    @Override
    public void Afunc() {
	System.out.print("Using Adapter : ");
        bClass.Bfunc();
    }
}

...

public static void main(String[] arg){
    //use Aclass
    Aclass a = new AclassImpl();
    a.Afunc();

    //use Bclass
    Bclass b = new BclassImpl();
    b.Bfunc();

    //Bclass -> Aclass
    Aclass useAdapter = new Adapter(b);
    useAdapter.Afunc();

    /* 결과
    function of Aclass
    function of Bclass
    Using Adapter : function of Bclass
    */
}
```

#### 2. 클래스 어댑터 (상속을 이용)
```
interface Aclass{
    void Afunc();
}

// 1. interface -> abstract class
abstract class Bclass{
    abstract void Bfunc();
}

class AclassImpl implements Aclass{
    @Override
    public void Afunc() {
        System.out.println("function of Aclass");
    }
}

class BclassImpl extends Bclass{
    @Override
    public void Bfunc() {
        System.out.println("function of Bclass");
    }
}

// 2. extends BclassImpl
class Adapter extends BclassImpl implements Aclass {
    @Override
    public void Afunc() {
        System.out.print("Using Adapter : ");
        Bfunc(); // 3. use function of Bclass
    }
}

...

public static void main(String[] arg){
    //use Aclass
    Aclass a = new AclassImpl();
    a.Afunc();

    //use Bclass
    Bclass b = new BclassImpl();
    b.Bfunc();

    //Bclass -> Aclass
    Aclass useAdapter = new Adapter();
    useAdapter.Afunc();

    /* 결과
    function of Aclass
    function of Bclass
    Using Adapter : function of Bclass
    */
}
```

1. Bclass 인터페이스 -> 추상클래스로 변경
2. 어댑터 클래스가 Bclass, Aclass 모두를 상속하도록 변경
3. Bclass의 함수 사용