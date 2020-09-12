# Strategy Pattern
- 기능(알고리즘)을 캡슐화하여 교환해서 쓸 수 있도록 한다.
- 예) java의 Arrays.sort: 정렬방식에 따라 Comparator를 정의해서 쓴다.


## Example
```
class Person{
    private Hobby hobby;
    void setHobby(Hobby hobby){
        this.hobby = hobby;
    }

	//play함수 실행 -> hobby.doSomething 함수로 권한 위임
    void play(){
        if(hobby == null) System.out.println("has no hobby");
        else hobby.doSomething();
    }
}

interface Hobby {
    void doSomething();
}

class Game implements Hobby{
    @Override
    public void doSomething() {
        System.out.println("play game");
    }
}

class Exercise implements Hobby{
    @Override
    public void doSomething() {
        System.out.println("do exercise");
    }
}
...
public static void main(String[] args) {
    Person p = new Person();
    p.setHobby(new Game());
    p.play();

    p.setHobby(new Exercise());
    p.play();

	//출력
	//play game
	//do exercise
	/* 같은 play 함수를 실행시켰지만 결과가 다르다 */
	
}
```