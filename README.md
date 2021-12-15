# honest_calc
from operator import add, sub, mul, truediv

messages = [
    "Enter an equation",
    "Do you even know what numbers are? Stay focused!",
    "Yes ... an interesting math operation. You've slept through all classes, haven't you?",
    "Yeah... division by zero. Smart move...",
    "Do you want to store the result? (y / n):",
    "Do you want to continue calculations? (y / n):",
    " ... lazy", " ... very lazy", " ... very, very lazy",
    "You are", "Are you sure? It is only one digit! (y / n)",
    "Don't be silly! It's just one number! Add to the memory? (y / n)",
    "Last chance! Do you really want to embarrass yourself? (y / n)"]


def chk(a, b, op):
    msg = ""
    if one_d(a) and one_d(b):
        msg += messages[6]
    if (a == 1 or b == 1) and op == '*':
        msg += messages[7]
    if (a == 0 or b == 0) and (op == '*' or op == '+' or op == '-'):
        msg += messages[8]
    if msg != "":
        msg = messages[9] + msg
        print(msg)


def one_d(v):
    if -10 < v < 10 and v % 1 == 0:
        return True
    else:
        return False


operations = {"+": add, "-": sub, "*": mul, "/": truediv}
memory = 0.0
while True:
    print(messages[0])
    calc = input()
    equation = calc.split()
    x, oper, y = equation[0], equation[1], equation[2]
    if x == "M":
        x = memory
    if y == "M":
        y = memory
    try:
        x = float(x)
        y = float(y)
    except ValueError:
        print(messages[1])
        continue
    else:
        if oper in operations:
            chk(x, y, oper)
            try:
                result = operations[oper](x, y)
                print(result)
                if input(messages[4]) == 'y':
                    if one_d(result):
                        if input(messages[10]) == 'y':
                            if input(messages[11]) == 'y':
                                if input(messages[12]) == 'y':
                                    memory = result
                    else:
                        memory = result
                    print(messages[5])
                else:
                    memory = result
                    print(messages[5])
                answer2 = input()
                if answer2 == "y":
                    continue
                else:
                    break
            except ZeroDivisionError:
                print(messages[3])
                continue
        else:
            print(messages[2])
