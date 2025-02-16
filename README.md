import random

class Human: def init(self, name, house, car=None, job=None): self.name = name self.house = house self.car = car self.job = job self.money = 1000 self.gladness = 50

def shoping(self):
    if self.car is None:
        print("Ідем в магазин пішки")
    else:
        self.car.drive(random.randint(10, 50))
    self.money -= random.randint(5, 15)
    self.house.food += random.randint(1, 5)

def work(self):
    if self.job:
        salary = self.job.salary
        self.money += salary
        print(f"Сьогодні працюємо. Заробили {salary}$")
    else:
        print("Безробітний, треба знайти роботу!")

def eat(self):
    self.gladness += 5
    food = random.randint(1, 5)
    if self.house.food - food > 0:
        self.house.food -= food
        print("Ми трошки поїли")
    else:
        print("Поїсти не вдалося, холодильник пустий")

def chill(self):
    print("Сьогодні ми відпочиваємо")
    self.money -= random.randint(5, 10)
    self.house.pollution += random.randint(1, 5)
    self.gladness += random.randint(5, 10)

def cleaning(self):
    percent = random.randint(1, 5)
    if percent == 5:
        print("Сьогодні генеральне прибирання")
        self.house.pollution = 0
    else:
        print("Сьогодні тільки повитирали пилюку")
        self.house.pollution = max(0, self.house.pollution - random.randint(1, 3))

def buy_car(self):
    if self.money >= 5000:
        self.money -= 5000
        self.car = Car("Toyota")
        print("Купили машину!")

def refuel(self):
    if self.car and self.car.fuel < 10:
        cost = 60 - self.car.fuel
        if self.money >= cost:
            self.money -= cost
            self.car.add_fuel(cost)
        else:
            print("Недостатньо грошей на заправку!")

def info(self):
    print(f"Гроші - {self.money}$")
    print(f"Задоволення - {self.gladness}")
    print(self.house)
    if self.car is not None:
        print(self.car)

def live(self, day):
    print(f" ---- День №{day} ----")
    self.work()
    self.shoping()
    self.eat()
    self.chill()
    if self.money >= 6000 and self.car is None:
        self.buy_car()
    if self.car and self.car.fuel < 10:
        self.refuel()
    if day % 5 == 0:
        self.cleaning()
    self.info()
    print()

def is_alive(self):
    return self.money >= 0

class Car: def init(self, model): self.model = model self.fuel = 60 self.state = 100

def drive(self, length):
    rashod = length * 0.1
    if self.fuel - rashod < 0:
        print("Подорож на авто не можлива, не вистачає пального, треба йти пішки")
    else:
        self.fuel -= rashod
        self.state -= length * 0.01
        print(f"Ми проїхали {length} км, витратили {rashod:.1f} л пального")

def add_fuel(self, fuel):
    self.fuel = min(60, self.fuel + fuel)
    print(f"Ми заправили {fuel} л пального")

def str(self):
    return f"Авто: {self.model}, пальне - {self.fuel}л, справність - {self.state}%"

class Job: def init(self, name, salary): self.name = name self.salary = salary

def str(self):
    return f"Робота: {self.name}, зарплатня - {self.salary}$"

class House: def init(self): self.pollution = 0 self.food = 0

def str(self):
    return f"Будинок: запас їжі - {self.food}, забрудненність - {self.pollution}"

human = Human("Vasya", job=Job("Програміст", 1000), house=House()) for day in range(1, 366): if not human.is_alive(): print("Гроші закінчилися! Гра закінчена.") break human.live(day)
