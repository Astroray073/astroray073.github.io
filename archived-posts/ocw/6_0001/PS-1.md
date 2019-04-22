---
title: "Problem Set 1"
excerpt: "Solving problem set 1"
last_modified_at: 2017-06-20 16:15:17
sidebar:
 nav: "ocw_6_0001"
---

{% include toc %}

[Problem Download](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-0001-introduction-to-computer-science-and-programming-in-python-fall-2016/assignments/MIT6_0001F16_ps1.pdf)

## Part A: House Hunting

연봉을 가지고 몇 퍼센트씩 저축할 때 해당 집의 착수금을 몇개월만에 모을 수 있는지 알아내는 프로그램 작성.

### Test Cases

```python
Test Case 1
Enter your annual salary: 120000 
Enter the percent of your salary to save, as a decimal: .10 
Enter the cost of your dream home: 1000000 Number of months: 183 

Test Case 2 
Enter your annual salary: 80000 
Enter the percent of your salary to save, as a decimal: .15 
Enter the cost of your dream home: 500000 Number of months: 105
```

### Solve

```python
annual_salary = float(input("Enter your annual salary: "))
portion_saved = float(input("Enter the percent of your salary, as a decimal: "))
total_cost = float(input("Enter the cost of your dream home: "))

monthly_salary = annual_salary / 12
portion_down_payment = 0.25

months = 0
r = 0.04
current_savings = 0.0
cost_for_down_payment = total_cost * portion_down_payment
savings_per_month = monthly_salary * portion_saved

while current_savings < cost_for_down_payment:
    current_savings *= 1 + r/12 # Additional savings for investment
    current_savings += savings_per_month #Adds savings for this month
    months += 1

print("Number of months: ", months)
```

주제가 생소해서 단어때문에 조금 헷갈린다. Python에는 `i++`과 같은 증감연산자가 없다.

## Part B: Saving, with a raise

Part A 의 해답을 가지고 조금 변형한 문제. 6개월마다 연봉을 올려준다.

### Test Cases

```python
Test Case 1 
Enter your starting annual salary: 120000 
Enter the percent of your salary to save, as a decimal: .05 
Enter the cost of your dream home: 500000 
Enter the semiannual raise, as a decimal: .03 
Number of months: 142

Test Case 2
Enter your starting annual salary: 80000 
Enter the percent of your salary to save, as a decimal: .1 
Enter the cost of your dream home: 800000 
Enter the semiannual raise, as a decimal: .03 
Number of months: 159 

Test Case 3 
Enter your starting annual salary: 75000 
Enter the percent of your salary to save, as a decimal: . 05 
Enter the cost of your dream home: 1500000 
Enter the semiannual raise, as a decimal: .05 
Number of months: 261
```

### Solve

```python
annual_salary = float(input("Enter your annual salary: "))
portion_saved = float(input("Enter the percent of your salary, as a decimal: "))
total_cost = float(input("Enter the cost of your dream home: "))
semi_annual_raise = float(input("Enter the semi-annual raise, as a decimal: "))

monthly_salary = annual_salary / 12
portion_down_payment = 0.25

months = 0
r = 0.04
current_savings = 0.0
cost_for_down_payment = total_cost * portion_down_payment
savings_per_month = monthly_salary * portion_saved

while current_savings < cost_for_down_payment:
    current_savings *= 1 + r/12 # Additional savings for investment
    current_savings += savings_per_month #Adds savings for this month
    months += 1
    if months % 6 == 0:
        savings_per_month *= 1 + semi_annual_raise

print("Number of months: ", months)
```

연봉을 올려주나 이달의 저축금의 비율을 올려주나 같기때문에 이대로 작성함. 더 좋은 코드 방법이라면 연봉을 올려줘서 로직이 드러나게끔 하는 것이 좋겠지만 연습이기에 그대로 두었다.

## Part C: Finding the right amount to save away

이전에 인풋으로 받던 값이 고정이고 저축률을 구하는 프로그램 작성. 추론 과정은 `Bisection Search`기법을 사용하도록 명시되어 있다.

### Test Cases

```python
Test Case 1
Enter the starting salary: 150000 
Best savings rate: 0.4411 
Steps in bisection search: 12

Test Case 2
Enter the starting salary: 300000 
Best savings rate: 0.2206 
Steps in bisection search: 9

Test Case 3
Enter the starting salary: 10000 
It is not possible to pay the down payment in three years.
```

### Solve

```python
starting_salary = float(input("Enter the starting salary: "))

semi_anuual_raise = 0.07
annual_return = 0.04
cost_for_down_payment = 1000000 * 0.25
epsilon = cost_for_down_payment * 0.0001

# Copied from ps1b.py
def getSavingsAfterThreeYears(saving_rate):
    portion_saved = saving_rate / 10000
    savings_per_month = starting_salary * portion_saved / 12
    current_savings = 0
    for i in range(36):
        current_savings *= 1 + annual_return/12 # Additional savings for investment
        current_savings += savings_per_month #Adds savings for this month
        if i % 6 == 0:
            savings_per_month *= 1 + semi_anuual_raise
    return current_savings
    
def searchForBestSavingRate():
    low = int(0)
    high = int(10000)
    
    if getSavingsAfterThreeYears(high) < cost_for_down_payment:
        print("It is not possible to pay the down payment in three years.")
        return
    
    best_saving_rate = int((low + high) / 2)
    steps = 0

    while True:
        steps += 1
        total_savings = getSavingsAfterThreeYears(best_saving_rate)
        if abs(cost_for_down_payment - total_savings) <= epsilon:
            break
        elif cost_for_down_payment - total_savings > 0:
            low = best_saving_rate
        else:
            high = best_saving_rate
        best_saving_rate = int((low + high) / 2)
    
    print("Best savings rate: ", best_saving_rate / 10000)
    print("Steps in bisection search: ", steps)
    
searchForBestSavingRate()
```

결과값이 조금 다른데 이는 `Bisection Search`시 epsilon 산정 값의 차이로 보인다.