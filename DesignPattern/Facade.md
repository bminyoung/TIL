# Facade Pattern
- 여러 클래스의 인터페이스를 쉽게 이용하기 위해 하나의 통합된 인터페이스를 만든다.
- 기존의 인터페이스를 쉽게 이용할 수 있다.

## Example
```
class TV{
    private boolean isTurnedOn;
    public void turnOn(){
        isTurnedOn = true;
        System.out.println("--- Turn on TV ---");
    }
    public void turnOff(){
        isTurnedOn = false;
        System.out.println("--- Turn off TV ---");
    }
}

class Computer{
    private boolean isOn;
    public void on(){
        isOn = true;
        System.out.println("--- Turn on Computer ---");
    }
    public void off(){
        isOn = false;
        System.out.println("--- Turn off Computer ---");
    }
}

class Home{
    private TV tv;
    private Computer computer;

    public Home(TV tv, Computer computer) {
        this.tv = tv;
        this.computer = computer;
    }

    public void comeBackHome(){
        tv.turnOn();
        computer.on();
    }
}

...

public static void main(String[] args) {
    TV tv = new TV();
    Computer computer = new Computer();

    //기존 코드
    System.out.println("--- come back home ---");
    tv.turnOn();
    computer.on();

    System.out.println("--- go outside ---");
    tv.turnOff();
    computer.off();
    
    // Facade Pattern 적용
    Home home = new Home(tv, computer);
    System.out.println("--- come back home ---");
    home.comeBackHome();

    System.out.println("--- go outside ---");
    home.goOutside();
}
```

- Facade 패턴을 적용하지 않으면 집에 돌아올때마다 tv, 컴퓨터를 일일이 켜야한다.
 	- tv, 컴퓨터 뿐 아니라 home의 다른 컴포넌트들이 추가된다면?
- Facade 패턴 적용 후에는 home의 함수만 수정해주면 된다.
- TV나 Computer 클래스를 정의하지 않고 Home 클래스 안에 포함시킨다면
	- TV나 Computer 클래스를 Home이 아닌 Office나 Shop 등 다른 클래스에서 재사용할 경우 불편하다.
