# MINT
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Recommended Papers and CFPs</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f4;
        }
        .container {
            max-width: 800px;
            margin: auto;
            background: white;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        h1, h2 {
            color: #333;
        }
        ul {
            list-style-type: none;
            padding: 0;
        }
        li {
            margin-bottom: 10px;
            padding: 10px;
            background-color: #f9f9f9;
            border-radius: 3px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Recommended Papers and CFPs</h1>
        <h2>Papers</h2>
        <ul id="papers-list"></ul>
        <h2>Call for Papers</h2>
        <ul id="cfps-list"></ul>
    </div>

    <script>
        // Sample data (replace this with your actual data or fetch from an API)
        const data = {
            papers: [
                { title: "Example Paper 1", date: "2024-09-15" },
                { title: "Example Paper 2", date: "2024-07-01" },
                { title: "Example Paper 3", date: "2024-03-20" }
            ],
            cfps: [
                { title: "Conference A", deadline: "2024-12-31" },
                { title: "Conference B", deadline: "2024-08-15" },
                { title: "Conference C", deadline: "2024-05-01" }
            ]
        };

        function isWithinSixMonths(dateString) {
            const itemDate = new Date(dateString);
            const currentDate = new Date();
            const sixMonthsAgo = new Date(currentDate.setMonth(currentDate.getMonth() - 6));
            return itemDate >= sixMonthsAgo;
        }

        function isDeadlineFuture(dateString) {
            const deadline = new Date(dateString);
            const currentDate = new Date();
            return deadline > currentDate;
        }

        function updateList(items, listId, filterFunction) {
            const list = document.getElementById(listId);
            list.innerHTML = '';
            items.forEach(item => {
                if (filterFunction(item.date || item.deadline)) {
                    const li = document.createElement('li');
                    li.textContent = item.title;
                    list.appendChild(li);
                }
            });
        }

        function updateLists() {
            updateList(data.papers, 'papers-list', isWithinSixMonths);
            updateList(data.cfps, 'cfps-list', isDeadlineFuture);
        }

        // Initial update
        updateLists();

        // Update every day (86400000 milliseconds = 24 hours)
        setInterval(updateLists, 86400000);
    </script>
</body>
</html>
