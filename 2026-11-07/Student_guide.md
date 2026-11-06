# 📘 Student Guide — 7 พ.ย. 2026: OOP ภาค 2 (Level 7–8)

> เนื้อหา Level 1–6 (class, `__init__`, `self`, inheritance, polymorphism) อยู่ใน `../2026-10-31/Student_guide.md`

---

## 1. class ที่เก็บ object อื่น → Level 7
```python
class RobotTeam:
    def __init__(self, name):
        self.name = name
        self.robots = []              # attribute เป็น list ได้!

    def add(self, robot):
        self.robots.append(robot)
```
> ท่า loop / ตัวสะสม / หาค่าน้อยสุด **เหมือนเดิมทุกอย่าง** แค่เปลี่ยน `robots` ➜ `self.robots`

| ฟังก์ชันลอย ๆ (Level 4) | method ของทีม (Level 7) |
|---|---|
| `total_battery(team)` | `team.total_battery()` |
| `weakest(team)` | `team.weakest()` |

### เช็กชื่อซ้ำ = ท่าค้นหา
```python
for r in self.robots:
    if r.name == robot.name:
        return False            # เจอซ้ำ → จบ
self.robots.append(robot)       # วนครบไม่เจอ → เพิ่ม
return True
```

---

## 2. object เรียก method ของ object อื่น → Level 8
```python
def attack(self, target):
    target.take_hit(self.power)     # สั่ง "อีกตัว" ให้ทำงาน
```
- `self` = ตัวที่โจมตี · `target` = ตัวที่โดน

### override แล้วเรียกของแม่ด้วย `super()`
```python
class ShieldBot(FighterBot):
    def take_hit(self, damage):
        super().take_hit(damage // 2)     # ใช้ของแม่ แต่ส่งค่าครึ่งเดียว
```

### 🎭 polymorphism ข้าม object
`attack()` ไม่รู้ว่า target เป็น class ไหน → เรียก `target.take_hit()` → Python เลือก `take_hit` ของ class นั้นให้เอง

---

## 🆘 จุดพลาดบ่อย
| อาการ | สาเหตุ |
|---|---|
| `AttributeError: 'RobotTeam' object has no attribute 'robots'` | ลืม `self.robots = []` ใน `__init__` |
| ทีมทุกทีมใช้ list ร่วมกัน | ประกาศ `robots = []` ไว้นอก `__init__` → ต้องเป็น `self.robots` ใน `__init__` |
| แบตติดลบ | ลืม `max(..., 0)` |
| ShieldBot โดนเต็ม | override ชื่อผิด (`take_hit` ต้องสะกดเหมือนแม่) |
