+++
title = 'PAW vs UAW'
date = 2025-11-16T11:14:26-05:00
draft = false
toc = false
categories = ['misc']
tags = ['personal finance']
series = ['']
+++

> Recently, I finished reading a book called 'The Millionaire Next Door'. Most of the content is talking about common sense, like how to live a frugal life, which most people have already done. It actually brings out an interesting formula about how to categorize your financial status.

```
Expected Net Worth = (Age x Annual Income) / 10
```

- If your actual net worth is **double than the expected number**, then you are a 'PAW (Prodigious accumulator of wealth)'.
- If your actual net worth is **less than half of the expected number**, then you are a 'UAW (Under accumulator of wealth)'.
- If you are something in between, like most people, you are an 'AAW (Average Accumulator of Wealth)'.

PAW means you live below your means-you are wealthy compared with your lifestyle. Obviously, you should try to be a 'PAW'.

In this book, the author indicates that most millionaires are very low-key-they don't live in mansions and drive fancy cars, they are among us. The difference is that when a financial crisis comes, they still live comfortably.

I recently moved to a lower-middle-class neighborhood. Before reading this book, I thought I was kind of rich here-I have a decent job in the city, while most of the people here are blue-collar. After living here for a while, I realized I was terribly wrong. Our building janitor, who lives next door, is a landlord of multiple houses, and he has his own business-he took this job just to kill time.

> I understand that living a frugal life is good for wealth growing, but I do want big houses and fancy cars, how do I get them?

I think the idea of this book is to distinguish between the actual rich and the fake rich. When a UAW purchases the latest iPhone, he/she lose the money for an iPhone. When a PAW purchases the same iPhone, his/her net worth might not be affected. Same idea with houses and cars.

I built a small tool to help you become a PAW, code is below.

---

```java
/* 
version: java 25.0.1

save this code into: 'Paw.java'
in terminal, run:
    javac Paw.java
    java Paw
*/
import java.util.*;

class Paw {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.printf("Your age: ");
        int age = sc.nextInt();
        System.out.printf("Your annual income: $");
        float annual_income = sc.nextFloat();
        System.out.printf("Your current net worth: $");
        float net_worth = sc.nextFloat();
        sc.close();
        float expected_net_worth = (age * annual_income) / 10;
        if (net_worth > (2 * expected_net_worth)) {
            System.out.println("Congrats! You are a PAW!");
        } else if (net_worth < (expected_net_worth / 2)) {
            System.out.println("Sorry, you are currently a UAW");
        } else {
            System.out.println("You are an AAW");
        }
    }
}
```