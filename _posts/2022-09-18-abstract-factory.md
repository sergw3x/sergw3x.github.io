---
layout: post title: Abstract Factory in Go and PHP 
category: Abstract Factory go golang php 
tags: Abstract Factory go golang php
---
Abstract Factory is a creation design pattern, which solves the problem of creating entire product families without
specifying their concrete classes.

# Golang

<pre>
  <code class="language-go">

    type ISportsFactory interface {
        makeShoe() IShoe
    }
    
    func GetSportsFactory(brand string) (ISportsFactory, error) {
        if brand == "adidas" {
            return &Adidas{}, nil
        }
    
        if brand == "nike" {
            return &Nike{}, nil
        }
    
        return nil, fmt.Errorf("Wrong brand type passed")
    }

    type IShoe interface {
        getSize() int
    }

    type Adidas struct {
    }

    func (a *Adidas) makeShoe() IShoe {
        return &AdidasShoe{
            Shoe: Shoe{
                size: 14,
            },
        }
    }

    func main() {
        adidasFactory, _ := GetSportsFactory("adidas")
        nikeFactory, _ := GetSportsFactory("nike")
    
        nikeShoe := nikeFactory.makeShoe()
        nikeShirt := nikeFactory.makeShirt()
    }

  </code>
</pre>

# PHP

<pre>

  <code class="language-php">

    interface AbstractFactory
    {
        public function createProductA(): AbstractProductA;
    
        public function createProductB(): AbstractProductB;
    }

    class ConcreteFactory1 implements AbstractFactory
    {
        public function createProductA(): AbstractProductA
        {
            return new ConcreteProductA1();
        }
    
        public function createProductB(): AbstractProductB
        {
            return new ConcreteProductB1();
        }
    }

    class ConcreteFactory2 implements AbstractFactory
    {
        public function createProductA(): AbstractProductA
        {
            return new ConcreteProductA2();
        }
    
        public function createProductB(): AbstractProductB
        {
            return new ConcreteProductB2();
        }
    }

    interface AbstractProductA
    {
        public function usefulFunctionA(): string;
    }

    class ConcreteProductA1 implements AbstractProductA
    {
        public function usefulFunctionA(): string
        {
            return "The result of the product A1.";
        }
    }
    
    class ConcreteProductA2 implements AbstractProductA
    {
        public function usefulFunctionA(): string
        {
            return "The result of the product A2.";
        }
    }

    interface AbstractProductB
    {
        public function usefulFunctionB(): string;

        public function anotherUsefulFunctionB(AbstractProductA $collaborator): string;
    }

    class ConcreteProductB1 implements AbstractProductB
    {
        public function usefulFunctionB(): string
        {
            return "The result of the product B1.";
        }

        public function anotherUsefulFunctionB(AbstractProductA $collaborator): string
        {
            $result = $collaborator->usefulFunctionA();
    
            return "The result of the B1 collaborating with the ({$result})";
        }
    }


    function clientCode(AbstractFactory $factory)
    {
        $productA = $factory->createProductA();
        $productB = $factory->createProductB();
    
        echo $productB->usefulFunctionB() . "\n";
        echo $productB->anotherUsefulFunctionB($productA) . "\n";
    }
    
    clientCode(new ConcreteFactory1());

    clientCode(new ConcreteFactory2());

  </code>
</pre>