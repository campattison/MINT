<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Research Hub: Normative Philosophy of Computing</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css" />
    <script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"></script>
    <script src="https://unpkg.com/three"></script>
    <script src="https://unpkg.com/globe.gl"></script>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
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
        #map-controls {
            margin-bottom: 10px;
        }

        .leaflet-popup-content-wrapper {
            border-radius: 8px;
            padding: 10px;
        }

        .leaflet-popup-content {
            margin: 5px;
        }

        .custom-icon {
            background-color: #3498db;
            border-radius: 50%;
            border: 2px solid #fff;
        }

        .summer-icon {
            background-color: #FFD700;
            border: 2px solid #FF6347;
            border-radius: 50%;
            box-shadow: 0 0 10px rgba(255, 215, 0, 0.5);
            transition: all 0.3s ease;
        }

        .summer-icon:hover {
            transform: scale(1.2);
        }

        .summer-popup .leaflet-popup-content-wrapper {
            background: linear-gradient(135deg, #87CEEB, #3CB371);
            border: 2px solid #FF6347;
        }

        .summer-popup .leaflet-popup-tip {
            background: #3CB371;
        }

        .summer-map {
            border: 10px solid transparent;
            border-image: url('beach-border.png') 30 round;
            transition: all 0.5s ease;
        }

        .summer-toggle-label {
            display: inline-block;
            padding: 5px 10px;
            background-color: #87CEEB;
            border-radius: 15px;
            transition: background-color 0.3s;
        }

        .summer-toggle-label.active {
            background-color: #FFD700;
        }

        @keyframes gentleWave {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-3px); }
        }

        .summer-icon {
            animation: gentleWave 3s infinite ease-in-out;
        }

        .summer-map::after {
            content: '☀️';
            position: absolute;
            top: 10px;
            right: 10px;
            font-size: 24px;
            animation: gentleWave 4s infinite ease-in-out;
        }

        #globeViz {
            width: 100%;
            height: 500px;
            background-color: #000011;
            position: relative;
            z-index: 10;
        }

        .summer-toggle-label {
            display: inline-block;
            padding: 5px 10px;
            background-color: #87CEEB;
            border-radius: 15px;
            transition: background-color 0.3s;
            margin-bottom: 10px;
        }

        .summer-toggle-label.active {
            background-color: #FFD700;
        }

        #month-selector {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 10px;
            margin-top: 20px;
            position: relative;
            z-index: 5;
        }

        .month-button {
            padding: 10px 15px;
            border: none;
            border-radius: 20px;
            background-color: #f0f0f0;
            color: #333;
            font-family: Arial, sans-serif;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .month-button:hover {
            background-color: #e0e0e0;
        }

        .month-button.active {
            background-color: #3498db;
            color: white;
        }

        @media (max-width: 768px) {
            .month-button {
                padding: 8px 12px;
                font-size: 12px;
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
        <div class="section" id="map-section">
            <h2>Conference Locations</h2>
            <div id="globeViz"></div>
            <div id="month-selector">
                <button class="month-button active" data-month="all">All Conferences</button>
                <button class="month-button" data-month="0">Jan</button>
                <button class="month-button" data-month="1">Feb</button>
                <button class="month-button" data-month="2">Mar</button>
                <button class="month-button" data-month="3">Apr</button>
                <button class="month-button" data-month="4">May</button>
                <button class="month-button" data-month="5">Jun</button>
                <button class="month-button" data-month="6">Jul</button>
                <button class="month-button" data-month="7">Aug</button>
                <button class="month-button" data-month="8">Sep</button>
                <button class="month-button" data-month="9">Oct</button>
                <button class="month-button" data-month="10">Nov</button>
                <button class="month-button" data-month="11">Dec</button>
            </div>
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
                },
                {
                    title: "Improving Instruction-Following in Language Models through Activation Steering",
                    authors: "Alessandro Stolfo, Vidhisha Balachandran, Safoora Yousefi, Eric Horvitz, Besmira Nushi",
                    journal: "arXiv",
                    date: "2024-10-15",
                    url: "https://arxiv.org/abs/2410.12877"
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
                    url: "https://facctconference.org/2025/#:~:text=FAccT%202025,welcome%20your%20contributions%20and%20insights."
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
                    url: "http://www.academyofathens.gr/en/aristotle-ai"
                },
                {
                    title: "Second International Symposium on Politics of Technologies in the Digital Age PHILOSOPHICAL AND INTERDISCIPLINARY PERSPECTIVES ON THE DIGITAL TRANSFORMATION OF THE PUBLIC SPHERE",
                    deadline: "2024-09-15",
                    url: "https://philevents.org/event/show/122038"
                },
                {
                    title: "2nd Annual National Symposium on Equitable AI",
                    deadline: "2024-11-15",
                    url: "https://philevents.org/event/show/127690"
                },
                {
                    title: "TexneCON 2025: Tech Ethics eXchange NorthEast, an Ethics of Technology Conference (including AI)",
                    deadline: "2024-11-01",
                    url: "https://philevents.org/event/show/126054"
                },
            ],
            conferences: [
                {
                    title: "SRI Seminar Series 2024",
                    date: "2024-10-18",
                    location: "University of Toronto",
                    url: "https://srinstitute.utoronto.ca/news/sri-seminar-series-returns-2024-grosse-abebe-dwork-huq-more",
                    lat: 43.6629,
                    lng: -79.3957
                },
                {
                    title: "TeXne Conference",
                    date: "2025-02-01",
                    location: "MIT",
                    url: "https://philevents.org/event/show/126054",
                    lat: 42.3601,
                    lng: -71.0942
                },
                {
                    title: "Symposium 2025: Aristotle in the Era of A.I.",
                    date: "2025-07-10",
                    location: "Academy of Athens, Greece",
                    url: "http://www.academyofathens.gr/en/aristotle-ai",
                    lat: 37.9838,
                    lng: 23.7275
                },
                {
                    title: "AISoLA, Conference Track Responsible and Trusted AI: An Interdisciplinary Perspective",
                    date: "2024-10-30 - 2024-11-03",
                    location: "Aldemar Knossos Royal, Crete, Greece",
                    url: "https://2024-isola.isola-conference.org/",
                    lat: 35.3253,
                    lng: 25.1444
                },
                {
                    title: "AI and Human Dignity",
                    date: "2024-10-31",
                    location: "Friedrich-Alexander-University Erlangen-Nürnberg, Germany",
                    url: "",
                    lat: 49.5979, // Approximate coordinates for Erlangen
                    lng: 11.0045
                },
                {
                    title: "TexneCON 2025: Tech Ethics eXchange NorthEast, an Ethics of Technology Conference",
                    date: "2024-11-01",
                    location: "Massachusetts Institute of Technology, Cambridge, MA, USA",
                    url: "https://philevents.org/event/show/126050",
                    lat: 42.3601,
                    lng: -71.0942
                },
                {
                    title: "AI and Human Dignity",
                    date: "2024-11-14",
                    location: "UNAM, Mexico City, Mexico",
                    url: "https://philevents.org/event/show/121922",
                    lat: 19.3262,
                    lng: -99.1761
                },
                {
                    title: "2nd Annual National Symposium on Equitable AI",
                    date: "2024-11-15",
                    location: "Morgan State University, Baltimore, MD, USA",
                    url: "https://philevents.org/event/show/127686",
                    lat: 39.3434,
                    lng: -76.5830
                },
                {
                    title: "AI and the Future of Science",
                    date: "2024-11-20",
                    location: "Lingnan University, Hong Kong",
                    url: "https://philevents.org/event/show/123930",
                    lat: 22.3363,
                    lng: 114.1641
                },
                {
                    title: "Second International Symposium on Politics of Technologies in the Digital Age",
                    date: "2024-11-21",
                    location: "University of Ioannina, Greece",
                    url: "https://philevents.org/event/show/122038",
                    lat: 39.6178,
                    lng: 20.8508
                },
                {
                    title: "Melanie Mitchell - AI's Challenge of Understanding the World",
                    date: "2024-11-22",
                    location: "University of Pittsburgh, PA, USA",
                    url: "https://philevents.org/event/show/127010",
                    lat: 40.4444,
                    lng: -79.9608
                },
                {
                    title: "Artificial Intelligence and the Professions",
                    date: "2024-12-05",
                    location: "Online",
                    url: "https://philevents.org/event/show/125678",
                    lat: null, // Online event, no specific location
                    lng: null
                }
            ]
        };

        // Sorting and filtering functions
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

        let globe;
        let selectedMonths = ['all'];

        function createGlobe() {
            const globeContainer = document.getElementById('globeViz');
            const width = globeContainer.clientWidth;
            const height = 500; // You can adjust this value

            globe = Globe()
                .globeImageUrl('//unpkg.com/three-globe/example/img/earth-blue-marble.jpg')
                .bumpImageUrl('//unpkg.com/three-globe/example/img/earth-topology.png')
                .width(width)
                .height(height)
                .showAtmosphere(true)
                .atmosphereColor('lightskyblue')
                .atmosphereAltitude(0.1)
                (globeContainer);

            // Stop auto-rotation
            globe.controls().autoRotate = false;

            const monthButtons = document.querySelectorAll('.month-button');
            monthButtons.forEach(button => {
                button.addEventListener('click', () => {
                    const month = button.dataset.month;
                    if (month === 'all') {
                        selectedMonths = ['all'];
                        monthButtons.forEach(btn => btn.classList.remove('active'));
                        button.classList.add('active');
                    } else {
                        if (selectedMonths.includes('all')) {
                            selectedMonths = [];
                            document.querySelector('[data-month="all"]').classList.remove('active');
                        }
                        button.classList.toggle('active');
                        if (button.classList.contains('active')) {
                            selectedMonths.push(month);
                            if (['5', '6', '7'].includes(month)) { // Summer months (June, July, August)
                                shootConfetti();
                            }
                        } else {
                            selectedMonths = selectedMonths.filter(m => m !== month);
                        }
                        if (selectedMonths.length === 0) {
                            selectedMonths = ['all'];
                            document.querySelector('[data-month="all"]').classList.add('active');
                        }
                    }
                    updateMarkers();
                });
            });

            updateMarkers();
        }

        function formatDate(dateString) {
            const date = new Date(dateString);
            const options = { month: 'long', day: 'numeric', year: 'numeric' };
            return date.toLocaleDateString('en-US', options);
        }

        function updateMarkers() {
            const markers = data.conferences
                .filter(conf => {
                    const date = new Date(conf.date);
                    return selectedMonths.includes('all') || selectedMonths.includes(date.getMonth().toString());
                })
                .map(conf => {
                    let { lat, lng } = conf;
                    if ((lat === 0 && lng === 0) || lat === null || lng === null) {
                        ({ lat, lng } = getRandomAntarcticaCoordinates());
                    }
                    const isAntarctica = lat < -60;
                    return {
                        lat,
                        lng,
                        size: 0.5,
                        color: isAntarctica ? '#FF69B4' : (selectedMonths.includes('all') ? '#FFD700' : '#3498db'),
                        label: `
                            <div style="
                                text-align: center; 
                                background-color: ${isAntarctica ? 'rgba(255,105,180,0.9)' : (selectedMonths.includes('all') ? 'rgba(255,223,186,0.9)' : 'rgba(255,255,255,0.9)')}; 
                                padding: 10px; 
                                border-radius: 5px;
                                box-shadow: 0 2px 5px rgba(0,0,0,0.2);
                                font-family: Arial, sans-serif;
                            ">
                                <strong style="color: ${isAntarctica ? '#8B008B' : (selectedMonths.includes('all') ? '#8B4513' : '#2c3e50')}; font-size: 14px;">${conf.title}</strong><br>
                                <span style="color: ${isAntarctica ? '#4B0082' : (selectedMonths.includes('all') ? '#CD853F' : '#34495e')}; font-size: 12px;">${formatDate(conf.date)}<br>${conf.location}</span><br>
                                <a href="${conf.url}" target="_blank" style="
                                    color: ${isAntarctica ? '#0000FF' : (selectedMonths.includes('all') ? '#0000FF' : '#3498db')}; 
                                    text-decoration: none; 
                                    font-weight: bold;
                                    font-size: 12px;
                                ">More information</a>
                            </div>
                        `,
                    };
                });

            globe.pointsData(markers)
                .pointAltitude(0.01)
                .pointColor('color')
                .pointLabel('label')
                .pointRadius('size')
                .onPointHover(point => {
                    if (point) {
                        globe.controls().autoRotate = false;
                    } else {
                        globe.controls().autoRotate = false; // Keep it false to prevent auto-rotation
                    }
                })
                .onPointClick(point => {
                    if (point) {
                        const conf = data.conferences.find(c => c.lat === point.lat && c.lng === point.lng);
                        if (conf) {
                            window.open(conf.url, '_blank');
                        }
                    }
                });

            // Add 3D arrows
            const arrowData = markers.map(marker => ({
                startLat: marker.lat,
                startLng: marker.lng,
                endLat: marker.lat,
                endLng: marker.lng,
                color: marker.color
            }));

            globe.arcsData(arrowData)
                .arcColor('color')
                .arcAltitude(0.2)
                .arcStroke(0.5)
                .arcDashLength(0.4)
                .arcDashGap(0.2)
                .arcDashAnimateTime(1500);

            if (selectedMonths.includes('all')) {
                globe.atmosphereColor('#FFB6C1');
            } else {
                globe.atmosphereColor('lightskyblue');
            }
        }

        function updateLists() {
            const sortedPapers = sortByDateDescending(data.papers);
            const sortedCFPs = sortByDateAscending(data.cfps);
            const sortedConferences = sortByDateAscending(data.conferences);

            updateList(sortedPapers, 'papers-list', () => true, formatPaper);
            updateList(sortedCFPs, 'cfps-list', () => true, formatCFP);
            updateList(sortedConferences, 'conferences-list', () => true, formatConference);

            createGlobe();
        }

        function shootConfetti() {
            const count = 200;
            const defaults = {
                origin: { y: 0.7 }
            };

            function fire(particleRatio, opts) {
                confetti(Object.assign({}, defaults, opts, {
                    particleCount: Math.floor(count * particleRatio)
                }));
            }

            fire(0.25, {
                spread: 26,
                startVelocity: 55,
            });
            fire(0.2, {
                spread: 60,
            });
            fire(0.35, {
                spread: 100,
                decay: 0.91,
                scalar: 0.8
            });
            fire(0.1, {
                spread: 120,
                startVelocity: 25,
                decay: 0.92,
                scalar: 1.2
            });
            fire(0.1, {
                spread: 120,
                startVelocity: 45,
            });
        }

        function getRandomAntarcticaCoordinates() {
            // Antarctica is roughly between -60 and -90 latitude, and all longitudes
            const lat = Math.random() * (-60 - (-90)) + (-90);
            const lng = Math.random() * 360 - 180;
            return { lat, lng };
        }

        // Initial update
        updateLists();

        // Update every day (86400000 milliseconds = 24 hours)
        setInterval(updateLists, 86400000);
    </script>
</body>
</html>
