# Flyweight Pattern
- 공통 자원을 공유해서 사용한다.
- 없으면 생성, 있으면 존재하는 객체를 참조한다.
- 싱글톤 패턴이 확장된거라고 생각하면 될 것 같다.
- 예) java의 String class
	- String str1 = "Hello"; String str2 = "Hello" => "Hello" 객체를 공유

## Example
```
class Fruit{
    private String name;

    Fruit(String name){
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

class FruitFactory{
    private static Map<String, Fruit> map = new HashMap<>();

    Fruit getFruit(String name){
        Fruit fruit = map.get(name);
        if(fruit == null){
            fruit = new Fruit(name);
            map.put(name, fruit);
            System.out.println("new fruit : " + name);
        }

        return fruit;
    }
}
...
public static void main(String[] args) {
	FruitFactory factory = new FruitFactory();
    System.out.println(factory.getFruit("apple").getName());
    System.out.println(factory.getFruit("apple").getName());
    System.out.println(factory.getFruit("banana").getName());
    System.out.println(factory.getFruit("banana").getName());
    System.out.println(factory.getFruit("apple").getName());
    //출력
    //new fruit : apple
	//apple
	//apple
	//new fruit : banana
	//banana
	//banana
	//apple
}
```
- apple과 banana를 처음 생성할때만 "new fruit"을 출력하고 나머지는 이미 생성된 객체를 참조한다.