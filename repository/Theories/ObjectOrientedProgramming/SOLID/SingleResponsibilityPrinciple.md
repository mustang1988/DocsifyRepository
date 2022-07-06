# **S**ingleResponsibilityPrinciple - 单一职责原则

---

## 原则简述

一个类应该有且只有一个改变其实现的理由, 这意味着一个类应该只有一个单一的功能并且该功能应该由这个类完全封装起来.

## 原则的理解

例如, 有以下图形类:

```java
class Square {
    private double length;

    public Square(double length) {
        this.length = length;
    }
}

class Circle {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }
}
```

上述的Square类和Circle类都是符合单一职责原则的, 因为只有当需要修改类数据结构时才会对其进行修改

又比如有如下类

```java
class AreaCalculator {
    private Square square;

    public AreaCalculator(Square square) {
        this.square = square;
    }

    public getArea() {
        return square.length * square.length;
    }

    public printArea(){
        System.out.println("Square area: "+getArea());
    }
}
```

该类就不符合单一职责原则, 因为它有两个功能, 计算面积和打印面积, 当其面积计算公式发生改变, 或者打印输出的格式需要调整时, 都需要修改这个类.

改造上面的AreaCalculator类使其符合单一职责原则:

```java

class AreaPrinter {
    private double area;

    public AreaPrinter(double area) {
        this.area = area;
    }

    public printArea() {
        System.out.println(area);
    }
}

class AreaCalculator {
    private Square square;

    public AreaCalculator(Square square) {
        this.square = square;
    }

    public getArea() {
        return square.length * square.length;
    }
}

public class Demo {
    public static void main(String[] args) {
        Square square = new Square(2);
        AreaCalculator areaCalculator = new AreaCalculator(square);
        AreaPrinter areaPrinter = new AreaPrinter(areaCalculator.getArea());
        areaPrinter.printArea();
    }
}
```

将打印面积的功能从AreaCalculator类中拆分出去, 放在单独的类中, 这样当面积计算公式需要变更, 就只需要修改AreaCalculator类, 而当打印输出的格式需要调整时, 只需要修改AreaPrinter类. 每个类都只有一个修改其实现的理由, 这就符合了单一职责原则.

