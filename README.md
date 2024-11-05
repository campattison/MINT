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

        .subsection {
            margin-bottom: 30px;
            padding: 20px;
            background-color: var(--card-background);
            border-radius: 8px;
            box-shadow: 0 2px 4px var(--shadow-color);
        }

        .subsection h3 {
            color: var(--secondary-color);
            margin-top: 0;
            font-size: 1.3em;
            border-bottom: 1px solid var(--primary-color);
            padding-bottom: 8px;
        }

        .category-description {
            color: #666;
            font-style: italic;
            margin-bottom: 15px;
            font-size: 0.9em;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Research Hub: Normative Philosophy of Computing</h1>
        <div class="section" id="papers-section">
            <h2>Recent Publications</h2>
            
            <div class="subsection">
                <h3>Conceptual & Normative Analysis</h3>
                <p class="category-description">Papers focusing on philosophical frameworks, ethical implications, and conceptual foundations</p>
                <ul id="philosophy-papers-list"></ul>
            </div>

            <div class="subsection">
                <h3>Technical Implementation & Empirical Studies</h3>
                <p class="category-description">Papers focusing on technical development, empirical results, and implementation approaches</p>
                <ul id="cs-papers-list"></ul>
            </div>

            <div class="subsection">
                <h3>Interdisciplinary Integration</h3>
                <p class="category-description">Papers that explicitly bridge theoretical frameworks with technical implementation</p>
                <ul id="hybrid-papers-list"></ul>
            </div>
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
                <!-- Month buttons will be dynamically inserted here -->
            </div>
        </div>
    </div>
   

    <script>
        const data = {
            philosophyPapers: [
                {
                    title: "Beneficent Intelligence: A Capability Approach to Modeling Benefit, Assistance, and Associated Moral Failures Through AI Systems",
                    authors: "London, A.J., Heidari, H.",
                    journal: "Minds & Machines",
                    date: "2024-09-01",
                    url: "https://doi.org/10.1007/s11023-024-09696-8"
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
                }
            ],
            csPapers: [
                {
                    title: "Teaching Models to Balance Resisting and Accepting Persuasion",
                    authors: "Elias Stengel-Eskin, Peter Hase, Mohit Bansal",
                    journal: "arXiv",
                    date: "2024-10-18",
                    url: "https://arxiv.org/abs/2410.14596"
                },
                {
                    title: "GSM-Symbolic: Understanding the Limitations of Mathematical Reasoning in Large Language Models",
                    authors: "Iman Mirzadeh, Keivan Alizadeh, Hooman Shahrokhi, Oncel Tuzel, Samy Bengio, Mehrdad Farajtabar",
                    journal: "Apple Research",
                    date: "2024-10-07",
                    url: "https://arxiv.org/abs/2410.05229"
                },
                {
                    title: "Scalable watermarking for identifying large language model outputs",
                    authors: "Sumanth Dathathri, Abigail See, Sumedh Ghaisas, Po-Sen Huang, Rob McAdam, Johannes Welbl, Vandana Bachani, Alex Kaskasoli, Robert Stanforth, Tatiana Matejovicova, Jamie Hayes, Nidhi Vyas, Majd Al Merey, Jonah Brown-Cohen, Rudy Bunel, Borja Balle, Taylan Cemgil, Zahra Ahmed, Kitty Stacpoole, Ilia Shumailov, Ciprian Baetu, Sven Gowal, Demis Hassabis & Pushmeet Kohli ",
                    journal: "Nature",
                    date: "2024-10-23",
                    url: "https://www.nature.com/articles/s41586-024-09696-8"
                },
                {
                    title: "Beyond Browsing: API-Based Web Agents",
                    authors: "Yueqi Song, Frank Xu, Shuyan Zhou, Graham Neubig",
                    journal: "arXiv",
                    date: "2024-10-21",
                    url: "https://arxiv.org/abs/2410.16464"
                },
                {
                    title: "Sabotage Evaluations for Frontier Models",
                    authors: "Joe Benton, Misha Wagner, Eric Christiansen, Cem Anil, Ethan Perez, Jai Srivastav, Esin Durmus, et al.",
                    journal: "Anthropic Research",
                    date: "2024-10-18",
                    url: "https://www.anthropic.com/research/sabotage-evaluations"
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
            hybridPapers: [
                {
                    title: "Moral Alignment for LLM Agents",
                    authors: "Elizaveta Tennant, Stephen Hailes, Mirco Musolesi",
                    journal: "arXiv",
                    date: "2024-10-02",
                    url: "https://arxiv.org/abs/2410.01639"
                },
                {
                    title: "Megastudy Testing 25 Treatments to Reduce Antidemocratic Attitudes and Partisan Animosity",
                    authors: "Jan G. Voelkel et al.",
                    journal: "Science",
                    date: "2024-10-20",
                    url: "https://www.science.org/doi/10.1126/science.adh4764"
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

        function updateList(items, listId, formatter) {
            const list = document.getElementById(listId);
            list.innerHTML = '';
            items.forEach(item => {
                const li = document.createElement('li');
                li.innerHTML = formatter(item);
                list.appendChild(li);
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
            const height = 500;

            globe = Globe()
                .globeImageUrl('//unpkg.com/three-globe/example/img/earth-blue-marble.jpg')
                .bumpImageUrl('//unpkg.com/three-globe/example/img/earth-topology.png')
                .width(width)
                .height(height)
                .showAtmosphere(true)
                .atmosphereColor('lightskyblue')
                .atmosphereAltitude(0.1)
                (globeContainer);

            globe.controls().autoRotate = false;

            updateMonthButtons();
            updateMarkers();
        }

        function updateMonthButtons() {
            const monthSelector = document.getElementById('month-selector');
            const allButton = monthSelector.querySelector('[data-month="all"]');
            monthSelector.innerHTML = ''; // Clear existing buttons
            monthSelector.appendChild(allButton); // Add back the "All Conferences" button

            const months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
            const currentMonth = new Date().getMonth();

            for (let i = 0; i < 12; i++) {
                const monthIndex = (currentMonth + i) % 12;
                const button = document.createElement('button');
                button.className = 'month-button';
                button.setAttribute('data-month', monthIndex);
                button.textContent = months[monthIndex];
                monthSelector.appendChild(button);
            }

            // Re-add event listeners
            const monthButtons = document.querySelectorAll('.month-button');
            monthButtons.forEach(button => {
                button.addEventListener('click', handleMonthButtonClick);
            });
        }

        function handleMonthButtonClick() {
            const month = this.dataset.month;
            if (month === 'all') {
                selectedMonths = ['all'];
                document.querySelectorAll('.month-button').forEach(btn => btn.classList.remove('active'));
                this.classList.add('active');
            } else {
                if (selectedMonths.includes('all')) {
                    selectedMonths = [];
                    document.querySelector('[data-month="all"]').classList.remove('active');
                }
                this.classList.toggle('active');
                if (this.classList.contains('active')) {
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
                .map(conf => ({
                    lat: conf.lat,
                    lng: conf.lng,
                    size: 0.5,
                    color: '#00ff00', // Bright green
                    label: `
                        <div style="text-align: center; background-color: rgba(255,255,255,0.9); padding: 10px; border-radius: 5px; box-shadow: 0 2px 5px rgba(0,0,0,0.2); font-family: Arial, sans-serif;">
                            <strong style="color: #2c3e50; font-size: 14px;">${conf.title}</strong><br>
                            <span style="color: #34495e; font-size: 12px;">${formatDate(conf.date)}<br>${conf.location}</span><br>
                            <a href="${conf.url}" target="_blank" style="color: #3498db; text-decoration: none; font-weight: bold; font-size: 12px;">More information</a>
                        </div>
                    `,
                    url: conf.url // Add the URL to the marker data
                }));

            // Add 3D arrows
            const arrowData = markers.map(marker => ({
                startLat: marker.lat,
                startLng: marker.lng,
                endLat: marker.lat,
                endLng: marker.lng,
                color: '#00ff00' // Bright green
            }));

            globe
                .pointsData(markers)
                .pointAltitude(0.01)
                .pointColor('color')
                .pointLabel('label')
                .pointRadius('size')
                .arcsData(arrowData)
                .arcColor('color')
                .arcAltitude(0.2)
                .arcStroke(0.5)
                .arcDashLength(0.9)
                .arcDashGap(1)
                .arcDashAnimateTime(2000)
                .onPointClick(point => {
                    if (point && point.url) {
                        window.open(point.url, '_blank');
                    }
                })
                .customLayerData(markers)
                .customThreeObject(d => {
                    const sprite = new THREE.Sprite(
                        new THREE.SpriteMaterial({map: new THREE.TextureLoader().load('https://raw.githubusercontent.com/mrdoob/three.js/master/examples/textures/sprites/disc.png')})
                    );
                    sprite.scale.set(2, 2, 1);
                    sprite.material.color.set('#00ff00'); // Bright green
                    return sprite;
                })
                .customThreeObjectUpdate((obj, d) => {
                    Object.assign(obj.position, globe.getCoords(d.lat, d.lng, 0.1));
                    obj.position.y += Math.sin(Date.now() / 1000) * 0.05; // Hovering effect
                });
        }

        function limitPapers(papers, limit = 10) {
            return papers.slice(0, limit);
        }

        function updateLists() {
            const sortedPapers = sortByDateDescending(data.papers);
            const limitedPapers = limitPapers(sortedPapers, 10);
            const sortedCFPs = sortByDateAscending(data.cfps);
            const sortedConferences = sortByDateAscending(data.conferences);

            updateList(limitedPapers, 'papers-list', formatPaper);
            updateList(sortedCFPs, 'cfps-list', formatCFP);
            updateList(sortedConferences, 'conferences-list', formatConference);

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

        // Initial update
        updateLists();
        createGlobe();

        // Update every day (86400000 milliseconds = 24 hours)
        setInterval(() => {
            updateLists();
            updateMonthButtons();
        }, 86400000);
    </script>
</body>
</html>
