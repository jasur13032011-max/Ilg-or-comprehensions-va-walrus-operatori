# Ilg-or-comprehensions-va-walrus-operatori
1. Noto'g'ri va to'g'ri ichma-ich sikl tartibi
Ichma-ich comprehension'da for sikllari oddiy ichma-ich for sikllari qanday yozilsa, aynan shunday ketma-ketlikda yoziladi (tashqi sikl birinchi, ichki sikl ikkinchi).

Noto'g'ri yozilish (SyntaxError yoki mantiqiy xato):
Python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# NOTO'G'RI: ichki sikl `x`ni ishlatmoqchi, lekin `x` keyingi tashqi siklda aniqlanmoqda
# flatten_wrong = [val for val in row for row in matrix]  # NameError: name 'row' is not defined
To'g'ri yozilish va tushuntirish:
Oddiy sikl ko'rinishi:

Python
for row in matrix:      # 1. Tashqi sikl
    for val in row:     # 2. Ichki sikl
        if val % 2 == 0: # 3. Shart (filtr)
            ...
Comprehension ko'rinishi ham aynan shu tartibni saqlaydi:

Python
[val for row in matrix for val in row if val % 2 == 0]
2. To'liq Kod Demo
Python
import time

# 2D matritsa
matrix = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12]
]

# ------------------------------------------------------------------
# 1. 2D matritsani tekislash (flatten) va faqat juft sonlarni saralash
# ------------------------------------------------------------------
even_numbers = [val for row in matrix for val in row if val % 2 == 0]
print("1. Juft sonlar ro'yxati (Flattened):")
print(even_numbers)
print("-" * 50)

# ------------------------------------------------------------------
# 2. Dict comprehension: Har bir qiymatni uning kvadratiga akslantirish
# ------------------------------------------------------------------
squares_dict = {val: val**2 for row in matrix for val in row if val % 2 == 0}
print("2. Juft sonlar va ularning kvadratlari (Dict):")
print(squares_dict)
print("-" * 50)

# ------------------------------------------------------------------
# 3. Set comprehension: Takrorlanuvchi elementlarni avtomatik takrorsizlantirish
# ------------------------------------------------------------------
duplicated_list = [1, 2, 2, 3, 4, 4, 4, 5, 6, 6, 7, 8, 8]
unique_evens_set = {x for x in duplicated_list if x % 2 == 0}
print("3. Takrorsiz juft sonlar to'plami (Set):")
print(unique_evens_set)
print("-" * 50)

# ------------------------------------------------------------------
# 4. Walrus operatori (`:=`) yordamida qimmat funksiyani 1 marta chaqirish
# ------------------------------------------------------------------
def expensive_computation(n):
    """Qimmat/sekin ishlaydigan funksiya simulyatsiyasi."""
    time.sleep(0.01)  # Kichik ushlanib qolish
    return n * 10

numbers = [1, 3, 5, 8, 11, 14, 15]

# Noto'g'ri (walrus-siz): expensive_computation(x) 2 marta chaqiriladi (shartda va qiymatda)
# [expensive_computation(x) for x in numbers if expensive_computation(x) > 50]

# To'g'ri (walrus bilan): funksiya faqat 1 marta chaqiriladi, natija `res` o'zgaruvchisiga saqlanadi
processed_values = [res for x in numbers if (res := expensive_computation(x)) > 50]

print("4. Walrus operatori natijasi (qimmat funksiya natijasi > 50):")
print(processed_values)
print("-" * 50)
Natija:
Plaintext
1. Juft sonlar ro'yxati (Flattened):
[2, 4, 6, 8, 10, 12]
--------------------------------------------------
2. Juft sonlar va ularning kvadratlari (Dict):
{2: 4, 4: 16, 6: 36, 8: 64, 10: 100, 12: 144}
--------------------------------------------------
3. Takrorsiz juft sonlar to'plami (Set):
{2, 4, 6, 8}
--------------------------------------------------
4. Walrus operatori natijasi (qimmat funksiya natijasi > 50):
[80, 110, 140, 150]
--------------------------------------------------
