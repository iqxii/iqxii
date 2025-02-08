rom flask import Flask, render_template, request, jsonify

app = Flask(_name_)

# بيانات وهمية (يمكن استبدالها بقاعدة بيانات حقيقية)
transactions = {
    "12345": {"status": "قيد التدقيق", "history": ["تم الإرسال", "قيد التدقيق"]},
    "67890": {"status": "مكتمل", "history": ["تم الإرسال", "قيد التدقيق", "الموافقة الأولية", "مكتمل"]},
    "54321": {"status": "تحت الإجراء", "history": ["تم الإرسال", "قيد التدقيق", "الموافقة الأولية", "تحت الإجراء"]}
}

@app.route("/")
def home():
    return render_template("index.html")

@app.route("/track", methods=["POST"])
def track():
    data = request.get_json()
    tracking_number = data.get("tracking_number")

    if tracking_number in transactions:
        return jsonify({"success": True, "data": transactions[tracking_number]})
    else:
        return jsonify({"success": False, "message": "رقم المعاملة غير موجود!"})

if _name_ == "_main_":
    app.run(debug=True
