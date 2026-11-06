# 🏠 การบ้าน — 7 พ.ย. 2026

- 🆕 **ไม่ได้มา 31 ต.ค.:** ทำ `2026-10-31` ให้ถึง **Level 6** + การบ้าน DeliveryBot ของ 31 ต.ค.
- ✅ **มา 31 ต.ค.:** ทำ **Level 7–8** ของสัปดาห์นี้ให้เสร็จ (⭐ ท้าทาย ไม่บังคับ)
- ✍️ ทุกคน: อ่านโค้ดนี้แล้วทายผล ก่อนรันเช็ก
  ```python
  def shout(func):
      def wrapper():
          return func().upper() + "!"
      return wrapper

  @shout
  def hello():
      return "hello robot"

  print(hello())
  ```
  > 🎁 สัปดาห์หน้า: **Decorators** — เคยเรียนแล้ว มาทบทวนกันให้ลึกขึ้น
- commit + push ขึ้น branch ของสัปดาห์
