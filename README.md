<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تتبع المعاملات</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }
        .container {
            max-width: 400px;
            margin: 50px auto;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px gray;
        }
        input {
            width: 80%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        button {
            padding: 10px 20px;
            background: blue;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .status-box {
            margin-top: 20px;
            padding: 15px;
            background: #e3f2fd;
            border-radius: 5px;
        }
        .timeline {
            list-style: none;
            padding: 0;
        }
        .timeline li {
            background: #d1e7fd;
            padding: 10px;
            margin: 5px;
            border-radius: 5px;
        }
    </style>
</head>
<body>

    <div class="container">
        <h2>🔍 تتبع المعاملة</h2>
        <input type="text" id="trackingNumber" placeholder="أدخل رقم المعاملة">
        <button onclick="trackTransaction()">تتبع</button>

        <div id="statusContainer" class="status-box" style="display: none;">
            <h3>حالة المعاملة: <span id="status"></span></h3>
            <h4>المراحل:</h4>
            <ul id="historyList" class="timeline"></ul>
        </div>
    </div>

    <script>
        function trackTransaction() {
            let trackingNumber = document.getElementById("trackingNumber").value;
            
            if (trackingNumber === "") {
                alert("يرجى إدخال رقم المعاملة");
                return;
            }

            fetch("/track", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ tracking_number: trackingNumber })
            })
            .then(response => response.json())
            .then(data => {
                if (data.success) {
                    document.getElementById("statusContainer").style.display = "block";
                    document.getElementById("status").innerText = data.data.status;
                    
                    let historyList = document.getElementById("historyList");
                    historyList.innerHTML = "";
                    data.data.history.forEach(step => {
                        let li = document.createElement("li");
                        li.innerText = step;
                        historyList.appendChild(li);
                    });
                } else {
                    alert(data.message);
                }
            })
            .catch(error => console.log(error));
        }
    </script>

</body>
</html>
