[基本信息](#基本信息)    
​	​	[描述](#描述)    
​	​	[环境](#环境)    
​	​	[使用](#使用)    
​	​	[角色](#角色1)    
​	​	[流程](#流程1)    
[普通建造者模式](#普通建造者模式)    
​	​	[拼魔方的流程](#拼魔方的流程)    
​	​	[角色](#角色2)    
​	​	[流程](#流程2)    
​	​	[代码](#代码)    
​	​	​	​	[产品](#产品)    
​	​	​	​	[抽象建造者](#抽象建造者)    
​	​	​	​	[具体建造者](#具体建造者)    
​	​	​	​	[导演者](#导演者)    
​	​	​	​	[客户端](#客户端)    
​	​	​	​	[总结](#总结)    


# 基本信息

## 描述

建造模式可以将一个产品的内部表象与产品的生成过程分割开来， 从而可以使一个建造过程生成具有不同的内部表象的产品对象。 

## 环境

1.  **一个对象会有一些重要的性质， 在它们没有恰当的值之前， 对象不能作为一个完整的产品使用。** 比如， 一个电子邮件有发件人地址、 收件人地址、 主题、 内容、附录等部分， 而在最起码的收件人地址得到赋值之前， 这个电子邮件不能发出
2.  **一个对象的一些性质必须按照某个顺序赋值才有意义 。 在某个性质没有赋值之前， 另一个性质则无法赋值**。  

## 使用

1.  这时候， 此对象相当于一个有待建造的产品， 而对象的这些性质相当于产品的零件 建造产品的过程是建造零件的过程。 由于建造零件的过程很复杂， 因此， 这些零件的建造过程往往被“外部化” 到另外一个称做建造者的对象里， 建造者对象返还给客户端的是一个全部零件都建造完毕的产品对象。  
2.  **建造模式利用一个导演者对象和具体建造者对象一个--个地建造出所有的零件， 从而建造出完整的产品对象。****建造模式利用一个导演者对象和具体建造者对象一个--个地建造出所有的零件， 从而建造出完整的产品对象。**
3.  建造者模式**将产品的结构和产品的零件建造过程对客户端隐藏起来**， 把对建造过程进行指挥的责任和具体建造者零件的责任分割开来， 达到责任划分和封装的目的 

## <a id='角色1'>角色</a>

1.  **抽象建造者 ( Builder) 角色： 给出一个抽象接口， 以规范产品对象的各个组成成分的建造。** 利用建造方法生产零件,一般来说,有多少零件， 就有多少相应的建造方法[^类似于工厂方法的抽象类] 
2.  具体建造者 ( Concrete Builder ) 角色： 担任这个角色的是与应用程序紧密相关的一些类， 它们在应用程序调用下创建产品的实例。  [^类似于工厂方法] 
    1.  这个角色要完成的任务包括：
        ①实现抽象建造者 Builder 所声明的接口， 给出一步一步地完成创建产品实例的操作。
        ②在建造过程完成后， 提供产品的实例。 
3.  导演者（Director) 角色： 担任这个角色的类调用具体建造者角色以创建产品对象。[^就是依据零件生产流程来调用零件的建造方法来生产产品] 
4.  产品（Product ) 角色： 产品（Product ) 便是建造中的复杂对象。 一般来说， 一个系统中会有多于 •个的产品类， 而且这些产品类并不一定有共同的接口， 而完全可以是不相关联的。 


## <a id='流程1'>流程</a>

客户端调用`Director`来生产产品,`Director` 通过具体建造者( ` ConCreateBuilder`)的流程来建造产品(`Produce`),具体建造者的流程是由抽象建造者(`Builder`)来规定

# 普通建造者模式

## 拼魔方的流程

这个是我自己想出来的,我只学过初级魔方,觉得很符合建造者模式流程,需要每个步骤有一定的流程才能完成拼图

## <a id='角色2'>角色</a>
 产品 : 完整的魔方
 建造者 : 魔方公式
 导演者 : 人 
## <a id='流程2'>流程</a>

客户端(`Client` )通过人(`people`)来得到拼好的魔方(`MagicCube`)，人按照拼魔方的公式(`ConcreateSpell`)来拼魔方

## 代码

### 产品

```java
package com.fei.main.part3.section19_1Builder.part4;

/**
 * 产品 魔方
 * @author xurunfei
 * @date 2017/12/15.
 */
public class MagicCube {
    /** 魔方的完成度 */
    private int completeDegree;
    /** 魔方完成了几面 */
    private int completeSide;

    public int getCompleteDegree() {
        return completeDegree;
    }

    public void setCompleteDegree(int completeDegree) {
        this.completeDegree = completeDegree;
    }

    public int getCompleteSide() {
        return completeSide;
    }

    public void setCompleteSide(int completeSide) {
        this.completeSide = completeSide;
    }
}

```

### 抽象建造者

```java
package com.fei.main.part3.section19_1Builder.part4;

/**
 * 抽象建造方法
 * @author xurunfei
 * @date 2017/12/15.
 */
public abstract class Spell {

    protected MagicCube magicCube;
    /**
     * 拼成底部十字
     * @author xurunfei
     * @date 2017/12/15 16:30
     */
    public abstract void  spellButtomCross();

    /**
     * 拼成底部
     * @author xurunfei
     * @date 2017/12/15 16:31
     */
    public abstract void spellButtomSide();

    /**
     * 拼成部分四周的图形
     * @author xurunfei
     * @date 2017/12/15 16:32
     */
    public abstract void spellPartOfAround();
    
    /**
     * 拼成顶部
     * @author xurunfei
     * @date 2017/12/15 16:33
     */
    public abstract void spellTopSide();
    
    /**
     * 完成周围图形
     * @author xurunfei
     * @date 2017/12/15 16:38
     */
    public abstract void spellAllAround();

    /**
     * 完成产品
     * @author xurunfei
     * @date 2017/12/15 16:38
     */
    public abstract MagicCube complete();
}

```

### 具体建造者

```java
package com.fei.main.part3.section19_1Builder.part4;

/**
 * 具体魔方的方法
 * @author xurunfei
 * @date 2017/12/15.
 */
public class ConcreteSpell extends Spell {
    @Override
    public void spellButtomCross() {
        magicCube.setCompleteDegree(20);
        magicCube.setCompleteSide(1);
    }

    @Override
    public void spellButtomSide() {
        magicCube.setCompleteSide(magicCube.getCompleteDegree()+20);
    }

    @Override
    public void spellPartOfAround() {
        magicCube.setCompleteSide(magicCube.getCompleteDegree()+20);

    }

    @Override
    public void spellTopSide() {
        magicCube.setCompleteSide(magicCube.getCompleteDegree()+20);
        magicCube.setCompleteSide(magicCube.getCompleteSide()+1);
    }

    @Override
    public void spellAllAround() {
        magicCube.setCompleteSide(magicCube.getCompleteDegree()+20);
        magicCube.setCompleteSide(magicCube.getCompleteSide()+4);
    }

    @Override
    public MagicCube complete() {
        return magicCube;
    }
}

```

### 导演者 

```java
package com.fei.main.part3.section19_1Builder.part4;

/**
 * 导演者角色
 * @author xurunfei
 * @date 2017/12/15.
 */
public class People {
    private Spell spell;

    public People(Spell spell) {
        this.spell = spell;
    }

    /**
     * 拼魔方
     * @author xurunfei
     * @date 2017/12/15 16:54
     */
    public MagicCube spellMagicCube(){
        spell.spellButtomCross();
        spell.spellButtomSide();
        spell.spellPartOfAround();
        spell.spellTopSide();
        spell.spellAllAround();
        return spell.complete();
    }
}

```

### 客户端 

```java
package com.fei.main.part3.section19_1Builder.part4;

/**
 * @author xurunfei
 * @date 2017/12/15.
 */
public class Client {
    public static void main(String[] args) {
        Spell spell = new ConcreteSpell();//拼魔方公式
        People people = new People(spell);//拼魔方的人
        MagicCube magicCube = people.spellMagicCube();//开始拼魔方,得到完整的魔方
    }
}

```

### 总结

建造者模式把拼魔方的流程对客户端隐藏,客户端只需要像人请求,要把这个魔方拼好得到就行,人必须按照魔方的流程一步一步才能将魔方拼好,一步没完成就会影响下一步,当全部流程走完,魔方才能拼完整
