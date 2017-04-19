## Overerving

Laten we starten met een klasse Pet. Deze moet kunnen eten, slapen en praten.

```java
public class Pet {

    int age;
    float weight;
    float height;
    String color;

    public void sleep(){
        System.out.println("Slaapwel!");
    }

    public void eat(){
        System.out.println("Zo een honger! Laat ik snel een biefstuk eten!");
    }

    public String talk(String word){
        String petResponse = "OK!! OK!! " + word;
        return petResponse;
    }
}
```

![](/assets/friendlymonster1.png)



