# 📘 Student Guide — 14 พ.ย. 2026: Decorators

> เปิดดูระหว่างทำได้เลย · แต่ละหัวข้อบอกว่าใช้กับ **Level ไหน**

---

## 1. function เป็น object → Level 1
| เขียน | ได้อะไร |
|---|---|
| `shout` | ตัว function (รีโมต) |
| `shout("hi")` | ผลจากการเรียก (กดปุ่ม) |

```python
panel = {"w": forward}        # เก็บ function ใน dict (ไม่มีวงเล็บ!)
panel["w"]()                  # ดึงออกมาแล้วเรียก
```

---

## 2. closure + `nonlocal` → Level 2
```python
def make_counter():
    count = 0
    def click():
        nonlocal count        # จะ "แก้" ค่าชั้นนอก ต้องประกาศ
        count += 1
        return count
    return click              # คืนตัว function
```
| อาการ | สาเหตุ |
|---|---|
| `UnboundLocalError` | ลืม `nonlocal` |
| ได้ `<function ...>` แทนผล | ลืมใส่ `()` ตอนเรียก |

---

## 3. decorator พื้นฐาน → Level 3
```python
def deco(func):
    def wrapper():
        # ทำอะไรก่อน
        result = func()       # ① เรียก function เดิม
        # ทำอะไรหลัง
        return result         # ② คืนผล
    return wrapper            # ③ คืนตัว wrapper (ไม่มีวงเล็บ)

@deco                         # = f = deco(f)
def f(): ...
```

---

## 4. ใช้ได้กับทุก function → Level 4
```python
from functools import wraps

def deco(func):
    @wraps(func)                       # ชื่อ function ไม่หาย
    def wrapper(*args, **kwargs):      # รับทุกแบบ
        return func(*args, **kwargs)   # ส่งต่อครบ
    return wrapper
```
- `*args` = tuple ของ argument ตามตำแหน่ง · `**kwargs` = dict ของ `ชื่อ=ค่า`
- `repr(x)` / `f"{x!r}"` → string มีเครื่องหมายคำพูด `'N'`

---

## 5. decorator ที่รับค่า (3 ชั้น) → Level 5, 6
```python
def repeat(times):                     # ชั้น 1: รับค่าตั้งค่า
    def decorator(func):               # ชั้น 2: รับ function
        @wraps(func)
        def wrapper(*args, **kwargs):  # ชั้น 3: ทำงานจริง
            ...
        return wrapper
    return decorator

@repeat(3)          # = f = repeat(3)(f)
def f(): ...
```
- wrapper **ไม่จำเป็นต้องเรียก** func เสมอ — ไม่ผ่านเงื่อนไขก็ return อย่างอื่นได้ (Level 5)

### ลองใหม่เมื่อพัง (Level 6)
```python
for attempt in range(1, times + 1):
    try:
        return func(*args, **kwargs)   # สำเร็จ → ออกทันที
    except ConnectionError as e:
        print(...)                     # ล้มเหลว → วนต่อ
return "❌ ยอมแพ้"                     # นอก loop
```

---

## 6. เช็กลิสต์ 5 บั๊ก → Level 7
1. wrapper รับ `*args, **kwargs`
2. **เรียก** `func(...)` ไม่ใช่แค่ `func`
3. **return** ผลลัพธ์
4. `@wraps(func)`
5. `return wrapper` ไม่ใช่ `return wrapper()`

---

## 7. ซ้อน + ใช้กับ method → Level 8
```python
@a
@b
def f(): ...        # = a(b(f)) → a ทำก่อน (บนสุด = นอกสุด)
```
- decorator บน method: wrapper ได้ **`self`** เป็น argument ตัวแรก → `def wrapper(self, *args, **kwargs):`
- `getattr(bolt, "scan")()` = `bolt.scan()`

---

## 🗂️ สรุป
| คำ | ความหมาย |
|---|---|
| decorator | function ที่รับ function แล้วคืน function ใหม่ที่ทำอะไรเพิ่ม |
| wrapper | function ใหม่ที่ห่อของเดิม |
| closure | function ข้างในที่จำตัวแปรชั้นนอกได้ |
| `@deco` | เขียนย่อของ `f = deco(f)` |

➡️ **สัปดาห์หน้า:** A05 Iterators & Generators 🏭
