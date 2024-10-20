<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Research Hub: Normative Philosophy of Computing</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #3498db;
            --secondary-color: #2c3e50;
            --background-color: #ecf0f1;
            --card-background: #ffffff;
            --text-color: #333333;
            --shadow-color: rgba(0, 0, 0, 0.1);
        }
        body {
            font-family: 'Roboto', sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 0;
            background-color: var(--background-color);
            color: var(--text-color);
        }
        .container {
            max-width: 1000px;
            margin: 40px auto;
            padding: 20px;
        }
        h1 {
            color: var(--primary-color);
            text-align: center;
            font-size: 2.5em;
            margin-bottom: 40px;
        }
        .section {
            background-color: var(--card-background);
            border-radius: 8px;
            box-shadow: 0 4px 6px var(--shadow-color);
            padding: 20px;
            margin-bottom: 30px;
            transition: transform 0.3s ease;
        }
        .section:hover {
            transform: translateY(-5px);
        }
        h2 {
            color: var(--secondary-color);
            border-bottom: 2px solid var(--primary-color);
            padding-bottom: 10px;
            margin-top: 0;
        }
        ul {
            list-style-type: none;
            padding: 0;
        }
        li {
            background-color: #f8f9fa;
            border-left: 4px solid var(--primary-color);
            margin-bottom: 10px;
            padding: 15px;
            border-radius: 4px;
            transition: background-color 0.3s ease;
        }
        li:hover {
            background-color: #e9ecef;
        }
        .date, .location {
            font-style: italic;
            color: #666;
            font-size: 0.9em;
        }
        a {
            color: var(--primary-color);
            text-decoration: none;
        }
        a:hover {
            text-decoration: underline;
        }
        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            h1 {
                font-size: 2em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Research Hub: Normative Philosophy of Computing</h1>
        <div class="section" id="papers-section">
            <h2>Recent Papers</h2>
            <ul id="papers-list"></ul>
        </div>
        <div class="section" id="cfps-section">
            <h2>Call for Papers</h2>
            <ul id="cfps-list"></ul>
        </div>
        <div class="section" id="conferences-section">
            <h2>Upcoming Conferences and Events</h2>
            <ul id="conferences-list"></ul>
        </div>
    </div>

    <script>
        const data = {
            papers: [
                {
                    title: "GSM-Symbolic: Understanding the Limitations of Mathematical Reasoning in Large Language Models",
                    authors: "Iman Mirzadeh, Keivan Alizadeh, Hooman Shahrokhi, Oncel Tuzel, Samy Bengio, Mehrdad Farajtabar",
                    journal: "Apple Research",
                    date: "2024-10-07",
                    url: "https://arxiv.org/abs/2410.05229"
                },
                {
                    title: "Beneficent Intelligence: A Capability Approach to Modeling Benefit, Assistance, and Associated Moral Failures Through AI Systems",
                    authors: "London, A.J., Heidari, H.",
                    journal: "Minds & Machines",
                    date: "2024-09-01",
                    url: "https://doi.org/10.1007/s11023-024-09696-8"
                },
                {
                    title: "Sabotage Evaluations for Frontier Models",
                    authors: "Joe Benton, Misha Wagner, Eric Christiansen, Cem Anil, Ethan Perez, Jai Srivastav, Esin Durmus, et al.",
                    journal: "Anthropic Research",
                    date: "2024-10-18",
                    url: "https://www.anthropic.com/research/sabotage-evaluations"
                },
                {
                    title: "Megastudy Testing 25 Treatments to Reduce Antidemocratic Attitudes and Partisan Animosity",
                    authors: "Jan G. Voelkel et al.",
                    journal: "Science",
                    date: "2024-10-20",
                    url: "https://www.science.org/doi/10.1126/science.adh4764"
                },
                {
                    title: "The AI Design Regress",
                    authors: "Pamela Robinson",
                    journal: "Philosophical Studies",
                    date: "2024-07-27",
                    url: "https://link.springer.com/article/10.1007/s11098-024-02176-w"
                },
                {
                    title: "Intention Reconsideration in Artificial Agents: A Structured Account",
                    authors: "Fabrizio Cariani",
                    journal: "Philosophical Studies",
                    date: "2024-06-01",
                    url: "https://link.springer.com/article/10.1007/s11098-024-02172-0"
                },
                {
                    title: "Group Prioritarianism: Why AI Should not Replace Humanity",
                    authors: "Frank Hong",
                    journal: "Philosophical Studies",
                    date: "2024-07-13",
                    url: "https://link.springer.com/article/10.1007/s11098-024-02189-5"
                },
                {
                    title: "The Selfish Machine? On the Power and Limitation of Natural Selection to Understand the Development of Advanced AI",
                    authors: "Maarten Boudry & Simon Friederich",
                    journal: "Philosophical Studies",
                    date: "2024-09-24",
                    url: "https://link.springer.com/article/10.1007/s11098-024-02226-3"
                },
                {
                    title: "Controllable Safety Alignment: Inference-Time Adaptation to Diverse Safety Requirements",
                    authors: "Jingyu Zhang, Ahmed Elgohary, Ahmed Magooda, Daniel Khashabi, Benjamin Van Durme",
                    journal: "arXiv",
                    date: "2024-10-11",
                    url: "https://arxiv.org/abs/2410.08968"
                },
                {
                    title: "Jailbreaking LLM-Controlled Robots",
                    authors: "Alexander Robey, Zachary Ravichandran, Vijay Kumar, Hamed Hassani, George J. Pappas",
                    journal: "arXiv",
                    date: "2024-10-17",
                    url: "https://arxiv.org/abs/2410.13691"
                },
                {
                    title: "Moral Alignment for LLM Agents",
                    authors: "Elizaveta Tennant, Stephen Hailes, Mirco Musolesi",
                    journal: "arXiv",
                    date: "2024-10-02",
                    url: "https://arxiv.org/abs/2410.01639"
                },
                {
                    title: "Looking Inward: Language Models Can Learn About Themselves by Introspection",
                    authors: "Felix J. Binder, James Chua, Tomek Korbak, Henry Sleight, John Hughes, Robert Long, Ethan Perez, Miles Turpin, Owain Evans",
                    journal: "arXiv",
                    date: "2024-10-17",
                    url: "http://arxiv.org/abs/2410.13787"
                },
                {
                    title: "Autoregressive Large Language Models Are Computationally Universal",
                    authors: "Dale Schuurmans, Hanjun Dai, Francesco Zanini",
                    journal: "arXiv",
                    date: "2024-10-04",
                    url: "http://arxiv.org/abs/2410.03170"
                },
                {
                    title: "Persistent Pre-Training Poisoning of LLMs",
                    authors: "Yiming Zhang, Javier Rando, Ivan Evtimov, Jianfeng Chi, Eric Michael Smith, Nicholas Carlini, Florian Tramèr, Daphne Ippolito",
                    journal: "arXiv",
                    date: "2024-10-17",
                    url: "http://arxiv.org/abs/2410.13722"
                }
            ],
            cfps: [
                {
                    title: "Oxford Berlin Colloquium 2025: AI/Computing and Moral/Political Philosophy",
                    deadline: "2024-10-15",
                    url: "https://www.oxford-aiethics.ox.ac.uk/oxford-berlin-colloquium-2025-call-papers"
                },
                {
                    title: "ACM FAccT 2025 (Athens, Greece)",
                    deadline: "2025-01-15",
                    url:    "https://facctconference.org/2025/#:~:text=FAccT%202025,welcome%20your%20contributions%20and%20insights."
                },
                {
                    title: "Call for Papers on Social Cognition and Agency",
                    deadline: "2024-09-24",
                    url: "https://philevents.org/event/show/126422"
                },
                {
                    title: "TeXne Conference Call for Papers",
                    deadline: "2024-11-01",
                    url: "https://philevents.org/event/show/126054"
                },
                {
                    title: "Symposium 2025: Aristotle in the Era of A.I. - Call for Participation",
                    deadline: "2025-01-07",
                    url: "mailto:aristotle.ai@academyofathens.gr"
                }
            ],
            conferences: [
                {
                    title: "SRI Seminar Series 2024",
                    date: "2024-10-18",
                    location: "University of Toronto",
                    url: "https://srinstitute.utoronto.ca/news/sri-seminar-series-returns-2024-grosse-abebe-dwork-huq-more"
                },
                {
                    title: "TeXne Conference",
                    date: "2025-02-01",
                    location: "MIT",
                    url: "https://philevents.org/event/show/126054"
                },
                {
                    title: "Symposium 2025: Aristotle in the Era of A.I.",
                    date: "2025-07-10",
                    location: "Academy of Athens, Greece",
                    url: "mailto:info@academyofathens.gr"
                }
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

        function isConferenceFuture(dateString) {
            const conferenceDate = new Date(dateString);
            const currentDate = new Date();
            return conferenceDate >= currentDate;
        }

        // Sorting functions
        function sortByDateDescending(items) {
            return items.sort((a, b) => new Date(b.date) - new Date(a.date));
        }

        function sortByDateAscending(items) {
            return items.sort((a, b) => new Date(a.date || a.deadline) - new Date(b.date || b.deadline));
        }

        function updateList(items, listId, filterFunction, formatter) {
            const list = document.getElementById(listId);
            list.innerHTML = '';
            items.forEach(item => {
                if (filterFunction(item.date || item.deadline)) {
                    const li = document.createElement('li');
                    li.innerHTML = formatter(item);
                    list.appendChild(li);
                }
            });
        }

        function formatPaper(paper) {
            return `<strong><a href="${paper.url}" target="_blank">${paper.title}</a></strong><br>
                    ${paper.authors}<br>
                    <span class="date">${paper.journal}, Published: ${paper.date}</span>`;
        }

        function formatCFP(cfp) {
            return `<strong><a href="${cfp.url}" target="_blank">${cfp.title}</a></strong><br>
                    <span class="date">Deadline: ${cfp.deadline}</span>`;
        }

        function formatConference(conference) {
            return `<strong><a href="${conference.url}" target="_blank">${conference.title}</a></strong><br>
                    <span class="date">${conference.date}</span>, <span class="location">${conference.location}</span>`;
        }

        function updateLists() {
            const sortedPapers = sortByDateDescending(data.papers);
            const sortedCFPs = sortByDateAscending(data.cfps);
            const sortedConferences = sortByDateAscending(data.conferences);

            updateList(sortedPapers, 'papers-list', isWithinSixMonths, formatPaper);
            updateList(sortedCFPs, 'cfps-list', isDeadlineFuture, formatCFP);
            updateList(sortedConferences, 'conferences-list', isConferenceFuture, formatConference);
        }

        // Initial update
        updateLists();

        // Update every day (86400000 milliseconds = 24 hours)
        setInterval(updateLists, 86400000);
    </script>
</body>
</html>
