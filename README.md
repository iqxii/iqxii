import matplotlib.pyplot as plt

# إنشاء تصميم أولي بسيط للواجهة المقترحة
fig, ax = plt.subplots(figsize=(6, 10))
ax.set_xlim(0, 6)
ax.set_ylim(0, 10)
ax.axis("off")

# عناوين الواجهة
ax.text(3, 9.5, "🔍 تتبع المعاملة", fontsize=16, fontweight="bold", ha="center")

# شريط البحث
ax.add_patch(plt.Rectangle((0.5, 8.5), 5, 0.5, edgecolor="black", facecolor="lightgray"))
ax.text(3, 8.75, "أدخل رقم المعاملة...", fontsize=12, ha="center", color="gray")

# حالة الطلب
ax.text(3, 7.8, "📍 حالة المعاملة: تحت المراجعة", fontsize=12, fontweight="bold", ha="center")

# مراحل العملية
stages = [
    ("📂 تم الإرسال", 7),
    ("📤 قيد التدقيق", 6),
    ("✅ الموافقة الأولية", 5),
    ("📌 تحت الإجراء", 4),
    ("✔ مكتمل", 3)
]

# رسم الخط الزمني للمعاملة
for i, (text, y) in enumerate(stages):
    ax.add_patch(plt.Circle((3, y), 0.3, color="blue" if i < 2 else "gray"))
    ax.text(3.5, y, text, fontsize=12, verticalalignment="center")

# زر العودة
ax.add_patch(plt.Rectangle((2, 0.5), 2, 0.8, edgecolor="black", facecolor="blue"))
ax.text(3, 0.9, "🔙 رجوع", fontsize=12, color="white", ha="center")

# عرض التصميم الأولي
plt.show()
