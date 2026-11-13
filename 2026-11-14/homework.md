# 📝 การบ้าน A04: Robot Upgrades

## ข้อ 1 ⭐ ทายผล
```python
def deco(func):
    def wrapper(*args):
        print("before", args)
        r = func(*args)
        print("after", r)
        return r + 1
    return wrapper

@deco
def add(a, b):
    return a + b

print(add(2, 3))
```

## ข้อ 2 ⭐ `@timer`
เขียน decorator จับเวลาการทำงาน (ใช้ `time.perf_counter()`) แสดง `<ชื่อ> ใช้เวลา 0.0123 วินาที` แล้วทดสอบกับ function ที่หาผลรวม 1 ถึง 10 ล้าน

## ข้อ 3 ⭐⭐ `@validate_positive`
ถ้ามี argument ตัวเลขใดติดลบ ให้ `raise ValueError` พร้อมข้อความบอกตำแหน่ง

## ข้อ 4 ⭐⭐ `@memo` ทำเอง
สร้าง cache เองด้วย dict (ไม่ใช้ `functools.cache`) แล้วใช้กับ fibonacci เทียบเวลา

## ข้อ 5 ⭐⭐⭐ `@rate_limit(n)`
อนุญาตให้เรียก function ได้ไม่เกิน n ครั้ง ครั้งต่อไป return `"🚫 เกินโควตา"` และมีวิธีรีเซ็ตโควตา (ใบ้: เพิ่ม attribute ให้ wrapper เช่น `wrapper.reset = ...`)

## ข้อ 6 ⭐⭐⭐ สำรวจ decorator ของ class
ค้นหาและเขียนตัวอย่างใช้ `@property`, `@staticmethod`, `@classmethod` กับ class `Robot` อธิบายว่าแต่ละตัวต่างกันยังไง
