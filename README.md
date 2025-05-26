<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jon Tomin - Interactive Resume</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Visualization & Content Choices: 
        - Summary: Direct text from resume, presented prominently. Goal: Quick overview. Method: HTML text. Interaction: None.
        - Experience: Chronological list of roles. Goal: Show career progression. Method: HTML cards with JS toggle for details. Interaction: Click to expand/collapse bullet points.
        - Skills: Categorized lists. Goal: Showcase diverse competencies. Method: HTML tags/badges. Interaction: None.
        - Achievements: Key metrics as stat cards and one bar chart. Goal: Highlight quantifiable impact. Method: HTML stat cards; Chart.js for revenue vs. quota. Interaction: Chart tooltip. Justification: Bar chart visually emphasizes a key comparative achievement. Library: Chart.js.
        - Education/Certs: Clean lists. Goal: Display qualifications. Method: HTML lists. Interaction: None.
        - Contact: Clickable links. Goal: Easy outreach. Method: HTML links. Interaction: Click to open mail/LinkedIn.
        All textual content is sourced directly from the provided resume.
    -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .nav-link {
            @apply px-3 py-2 rounded-md text-sm font-medium text-stone-700 hover:bg-sky-100 hover:text-sky-700 transition-colors;
        }
        .nav-link.active {
            @apply bg-sky-600 text-white hover:bg-sky-700 hover:text-white;
        }
        .section-title {
            @apply text-3xl font-bold text-sky-700 mb-6 text-center;
        }
        .card {
            @apply bg-white p-6 rounded-lg shadow-lg transition-shadow hover:shadow-xl;
        }
        .stat-card {
            @apply bg-sky-50 p-6 rounded-lg shadow-md text-center;
        }
        .stat-number {
            @apply text-4xl font-bold text-sky-600 mb-2;
        }
        .stat-label {
            @apply text-sm text-stone-600;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px; /* Max width for readability */
            margin-left: auto;
            margin-right: auto;
            height: 300px; /* Base height */
            max-height: 400px; /* Max height */
        }
        @media (min-width: 768px) { /* md breakpoint */
            .chart-container {
                height: 350px;
            }
        }
        /* For experience details toggle */
        .details-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease-in-out;
        }
        .details-content.open {
            max-height: 1000px; /* Adjust as needed */
        }
    </style>
</head>
<body class="bg-stone-100 text-stone-800">

    <nav id="navbar" class="bg-white/80 backdrop-blur-md shadow-md fixed top-0 left-0 right-0 z-50">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <div class="flex items-center">
                    <a href="#summary" class="text-2xl font-bold text-sky-700">Jon Tomin</a>
                </div>
                <div class="hidden md:block">
                    <div class="ml-10 flex items-baseline space-x-4">
                        <a href="#summary" data-section="summary" class="nav-link active">Summary</a>
                        <a href="#experience" data-section="experience" class="nav-link">Experience</a>
                        <a href="#skills" data-section="skills" class="nav-link">Skills</a>
                        <a href="#achievements" data-section="achievements" class="nav-link">Achievements</a>
                        <a href="#education" data-section="education" class="nav-link">Education</a>
                        <a href="#contact" data-section="contact" class="nav-link">Contact</a>
                    </div>
                </div>
                <div class="md:hidden">
                    <button id="mobile-menu-button" class="text-stone-700 hover:text-sky-700 focus:outline-none">
                        <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
                        </svg>
                    </button>
                </div>
            </div>
        </div>
        <div id="mobile-menu" class="md:hidden hidden">
            <div class="px-2 pt-2 pb-3 space-y-1 sm:px-3">
                <a href="#summary" data-section="summary" class="block nav-link mobile-nav-link active">Summary</a>
                <a href="#experience" data-section="experience" class="block nav-link mobile-nav-link">Experience</a>
                <a href="#skills" data-section="skills" class="block nav-link mobile-nav-link">Skills</a>
                <a href="#achievements" data-section="achievements" class="block nav-link mobile-nav-link">Achievements</a>
                <a href="#education" data-section="education" class="block nav-link mobile-nav-link">Education</a>
                <a href="#contact" data-section="contact" class="block nav-link mobile-nav-link">Contact</a>
            </div>
        </div>
    </nav>

    <main class="pt-16">
        <section id="summary" class="min-h-screen flex items-center justify-center py-12 px-4 sm:px-6 lg:px-8 bg-gradient-to-br from-sky-50 to-stone-50">
            <div class="max-w-3xl mx-auto text-center">
                <h1 class="text-5xl md:text-6xl font-extrabold text-sky-700 mb-4">Jon Tomin</h1>
                <p class="text-xl md:text-2xl text-stone-600 font-medium mb-8">VP-Level Sales Leader | AI & SaaS Specialist | Healthcare Innovator</p>
                <div class="bg-white p-8 rounded-xl shadow-2xl">
                    <p class="text-lg text-stone-700 leading-relaxed">
                        Visionary VP-level Sales Leader with 15+ years of experience driving exceptional growth in IT and SaaS sectors, specializing in multi-million dollar enterprise deals across healthcare and technology verticals. Expert in new logo acquisition, C-suite relationship management, and building high-performing sales teams. Proven ability to lead complex sales cycles, craft strategic go-to-market plans for AI-enabled platforms, and scale revenue through consultative and ROI-driven selling. Deep experience in cloud technologies and enterprise software for hospitals and health systems. Eager to bring leadership and innovation to fuel new business development.
                    </p>
                </div>
                <a href="#experience" class="mt-10 inline-block bg-sky-600 text-white font-semibold py-3 px-8 rounded-lg shadow-md hover:bg-sky-700 transition-colors text-lg">
                    Explore My Experience &darr;
                </a>
            </div>
        </section>

        <section id="experience" class="py-16 px-4 sm:px-6 lg:px-8 bg-white">
            <div class="max-w-4xl mx-auto">
                <h2 class="section-title">💼 Professional Experience</h2>
                <p class="text-center text-stone-600 mb-12 text-lg">A proven track record of driving growth and leading high-performing teams across innovative companies.</p>
                <div class="space-y-12">
                    <div class="card experience-item">
                        <div class="flex justify-between items-start mb-2">
                            <div>
                                <h3 class="text-2xl font-semibold text-sky-700">Head of Sales & Marketing</h3>
                                <p class="text-md text-stone-600">Doseform (Remote)</p>
                            </div>
                            <p class="text-sm text-stone-500">2023 – Present</p>
                        </div>
                        <p class="italic text-stone-500 mb-3">AI-driven SaaS platform modernizing pharmacy workflows for hospitals and retail health.</p>
                        <button class="text-sky-600 hover:text-sky-800 font-medium text-sm toggle-details">Show Details &darr;</button>
                        <ul class="mt-2 space-y-1 text-stone-700 list-disc list-inside details-content">
                            <li>Led GTM strategy targeting hospitals, health systems, and enterprise pharmacy networks, establishing Doseform’s market positioning.</li>
                            <li>Closed key enterprise deals with multiple large health systems, driving early adoption and customer validation.</li>
                            <li>Secured funding through direct support in investor presentations and strategic pipeline growth.</li>
                            <li>Oversaw successful integrations with leading EHR platforms including Epic, Cerner, and Meditech, ensuring clinical interoperability.</li>
                            <li>Partnered with product and engineering teams to align sales strategy with evolving platform capabilities and client demands.</li>
                        </ul>
                    </div>

                    <div class="card experience-item">
                        <div class="flex justify-between items-start mb-2">
                            <div>
                                <h3 class="text-2xl font-semibold text-sky-700">Head of Sales</h3>
                                <p class="text-md text-stone-600">Vital.io (Remote) - Contract</p>
                            </div>
                            <p class="text-sm text-stone-500">2024 – 2025</p>
                        </div>
                        <p class="italic text-stone-500 mb-3">AI analytics SaaS platform for health systems.</p>
                        <button class="text-sky-600 hover:text-sky-800 font-medium text-sm toggle-details">Show Details &darr;</button>
                        <ul class="mt-2 space-y-1 text-stone-700 list-disc list-inside details-content">
                            <li>Closed a <strong>$3M CARR net-new system-wide agreement</strong> across 83 hospitals — the company’s largest deal to date.</li>
                            <li>Implemented the IMPACT Sales Process, shortening sales cycles and improving win rates via strategic, data-driven selling.</li>
                            <li>Built and led a high-performing national sales team, increasing pipeline by 400% through targeted outreach and ABM campaigns.</li>
                            <li>Developed and executed go-to-market strategies aligned with executive priorities to expand market share and client base.</li>
                            <li>Leveraged Apollo.io and Dripify for pipeline automation and hunter-style prospecting.</li>
                        </ul>
                    </div>
                    
                    <div class="card experience-item">
                        <div class="flex justify-between items-start mb-2">
                            <div>
                                <h3 class="text-2xl font-semibold text-sky-700">Regional VP of Sales & Business Development</h3>
                                <p class="text-md text-stone-600">98point6 Technologies (Remote)</p>
                            </div>
                            <p class="text-sm text-stone-500">2023 – 2024</p>
                        </div>
                        <p class="italic text-stone-500 mb-3">AI-powered virtual care platform.</p>
                        <button class="text-sky-600 hover:text-sky-800 font-medium text-sm toggle-details">Show Details &darr;</button>
                        <ul class="mt-2 space-y-1 text-stone-700 list-disc list-inside details-content">
                            <li>Directed enterprise sales across multi-state regions, closing strategic partnerships with Walmart and major IDNs.</li>
                            <li>Collaborated directly with the CEO and executive team on growth strategy and enterprise GTM alignment.</li>
                            <li>Became preferred RFP vendor through a 12-month competitive evaluation process.</li>
                            <li>Exceeded revenue targets by aligning innovative SaaS offerings with evolving health system needs.</li>
                        </ul>
                    </div>

                    <div class="card experience-item">
                         <div class="flex justify-between items-start mb-2">
                            <div>
                                <h3 class="text-2xl font-semibold text-sky-700">Regional Sales Director, Southwest Region</h3>
                                <p class="text-md text-stone-600">Omnicell (NASDAQ: OMCL) (Remote)</p>
                            </div>
                            <p class="text-sm text-stone-500">2022 – 2023</p>
                        </div>
                        <button class="text-sky-600 hover:text-sky-800 font-medium text-sm toggle-details">Show Details &darr;</button>
                        <ul class="mt-2 space-y-1 text-stone-700 list-disc list-inside details-content">
                            <li>Oversaw a $120M annual revenue territory across 7 states.</li>
                            <li>Recruited and led a 7-person sales team, building a $400M pipeline within 10 months.</li>
                            <li>Focused on strategic growth and automation solutions for hospital systems and enterprise pharmacy networks.</li>
                        </ul>
                        <hr class="my-4 border-stone-200">
                        <h4 class="text-lg font-semibold text-sky-600">Health System Sales Executive, Western Region</h4>
                        <p class="text-sm text-stone-500 mb-2">2020 – 2022</p>
                        <ul class="space-y-1 text-stone-700 list-disc list-inside">
                            <li>Won $25M competitive IDN conversion by leveraging ROI-focused presentations and complex stakeholder management.</li>
                            <li>Surpassed quotas consistently and earned promotion based on sales excellence and strategic execution.</li>
                        </ul>
                        <hr class="my-4 border-stone-200">
                         <h4 class="text-lg font-semibold text-sky-600">Area Account Executive, Pacific Northwest</h4>
                        <p class="text-sm text-stone-500 mb-2">2017 – 2020</p>
                        <ul class="space-y-1 text-stone-700 list-disc list-inside">
                             <li>Awarded Rep of the Year (2019) after generating $31M in revenue against an $8M quota.</li>
                             <li>Managed 250+ provider accounts; built long-cycle consultative relationships with C-suite buyers.</li>
                        </ul>
                    </div>
                    
                    <div class="card experience-item">
                        <div class="flex justify-between items-start mb-2">
                            <div>
                                <h3 class="text-2xl font-semibold text-sky-700">Owner / Head of Sales</h3>
                                <p class="text-md text-stone-600">Paulsen's Pharmacy (Portland, OR)</p>
                            </div>
                            <p class="text-sm text-stone-500">2015 – 2018</p>
                        </div>
                        <button class="text-sky-600 hover:text-sky-800 font-medium text-sm toggle-details">Show Details &darr;</button>
                        <ul class="mt-2 space-y-1 text-stone-700 list-disc list-inside details-content">
                            <li>Grew business valuation from $350K to $2M and expanded into long-term care and hospice services.</li>
                            <li>Tripled prescription volume by securing direct contracts with PBMs and health systems.</li>
                        </ul>
                    </div>

                    <div class="card experience-item">
                        <div class="flex justify-between items-start mb-2">
                            <div>
                                <h3 class="text-2xl font-semibold text-sky-700">Sales Director</h3>
                                <p class="text-md text-stone-600">Parata Systems (Portland, OR)</p>
                            </div>
                            <p class="text-sm text-stone-500">2011 – 2015</p>
                        </div>
                        <button class="text-sky-600 hover:text-sky-800 font-medium text-sm toggle-details">Show Details &darr;</button>
                        <ul class="mt-2 space-y-1 text-stone-700 list-disc list-inside details-content">
                            <li>Sold pharmacy automation and central fill systems into enterprise networks like Kaiser and Providence.</li>
                            <li>Achieved President’s Club and Eagle’s Nest honors for sales leadership.</li>
                        </ul>
                    </div>

                    <div class="card experience-item">
                        <div class="flex justify-between items-start mb-2">
                            <div>
                                <h3 class="text-2xl font-semibold text-sky-700">Account Executive</h3>
                                <p class="text-md text-stone-600">Carestream Dental (Portland, OR)</p>
                            </div>
                            <p class="text-sm text-stone-500">2008 – 2011</p>
                        </div>
                        <button class="text-sky-600 hover:text-sky-800 font-medium text-sm toggle-details">Show Details &darr;</button>
                        <ul class="mt-2 space-y-1 text-stone-700 list-disc list-inside details-content">
                            <li>Top performer in SaaS and digital imaging for dental health systems.</li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>

        <section id="skills" class="py-16 px-4 sm:px-6 lg:px-8 bg-stone-50">
            <div class="max-w-5xl mx-auto">
                <h2 class="section-title">💡 Core Competencies</h2>
                <p class="text-center text-stone-600 mb-12 text-lg">Leveraging a diverse skill set to deliver exceptional results in sales, strategy, and leadership.</p>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                    <div class="card">
                        <h3 class="text-xl font-semibold text-sky-700 mb-3">Sales Leadership & Strategy</h3>
                        <div class="flex flex-wrap gap-2">
                            <span class="bg-sky-100 text-sky-800 px-3 py-1 rounded-full text-sm">Sales Strategy & Pipeline Growth</span>
                            <span class="bg-sky-100 text-sky-800 px-3 py-1 rounded-full text-sm">Sales Team Leadership & Coaching</span>
                            <span class="bg-sky-100 text-sky-800 px-3 py-1 rounded-full text-sm">Strategic Planning & Execution</span>
                        </div>
                    </div>
                    <div class="card">
                        <h3 class="text-xl font-semibold text-sky-700 mb-3">Client & Deal Management</h3>
                        <div class="flex flex-wrap gap-2">
                            <span class="bg-sky-100 text-sky-800 px-3 py-1 rounded-full text-sm">New Logo Acquisition</span>
                            <span class="bg-sky-100 text-sky-800 px-3 py-1 rounded-full text-sm">C-Suite Engagement & Enterprise Negotiation</span>
                            <span class="bg-sky-100 text-sky-800 px-3 py-1 rounded-full text-sm">Consultative & ROI-Based Selling</span>
                        </div>
                    </div>
                    <div class="card">
                        <h3 class="text-xl font-semibold text-sky-700 mb-3">Industry Expertise</h3>
                        <div class="flex flex-wrap gap-2">
                            <span class="bg-sky-100 text-sky-800 px-3 py-1 rounded-full text-sm">AI & SaaS Solution Sales</span>
                            <span class="bg-sky-100 text-sky-800 px-3 py-1 rounded-full text-sm">IT & Software Services Sales</span>
                            <span class="bg-sky-100 text-sky-800 px-3 py-1 rounded-full text-sm">Healthcare GTM Strategy</span>
                        </div>
                    </div>
                    <div class="card md:col-span-2 lg:col-span-3">
                        <h3 class="text-xl font-semibold text-sky-700 mb-3">Technical Proficiencies (Tools)</h3>
                        <div class="flex flex-wrap gap-2">
                            <span class="bg-teal-100 text-teal-800 px-3 py-1 rounded-full text-sm">Salesforce</span>
                            <span class="bg-teal-100 text-teal-800 px-3 py-1 rounded-full text-sm">HubSpot</span>
                            <span class="bg-teal-100 text-teal-800 px-3 py-1 rounded-full text-sm">Apollo.io</span>
                            <span class="bg-teal-100 text-teal-800 px-3 py-1 rounded-full text-sm">Dripify</span>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="achievements" class="py-16 px-4 sm:px-6 lg:px-8 bg-white">
            <div class="max-w-5xl mx-auto">
                <h2 class="section-title">🏆 Key Achievements & Impact</h2>
                <p class="text-center text-stone-600 mb-12 text-lg">Quantifiable results demonstrating significant impact on revenue, growth, and market position.</p>
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8 mb-12">
                    <div class="stat-card">
                        <p class="stat-number">$3M</p>
                        <p class="stat-label">CARR Net-New System-Wide Agreement (Vital.io)</p>
                    </div>
                    <div class="stat-card">
                        <p class="stat-number">400%</p>
                        <p class="stat-label">Pipeline Increase (Vital.io)</p>
                    </div>
                    <div class="stat-card">
                        <p class="stat-number">$400M</p>
                        <p class="stat-label">Pipeline Built in 10 Months (Omnicell)</p>
                    </div>
                    <div class="stat-card">
                        <p class="stat-number">$25M</p>
                        <p class="stat-label">Competitive IDN Conversion (Omnicell)</p>
                    </div>
                     <div class="stat-card">
                        <p class="stat-number">5.7x</p>
                        <p class="stat-label">Valuation Growth ($350K to $2M at Paulsen's Pharmacy)</p>
                    </div>
                    <div class="stat-card">
                        <p class="stat-number">3x</p>
                        <p class="stat-label">Prescription Volume (Paulsen's Pharmacy)</p>
                    </div>
                </div>
                <div class="card">
                    <h3 class="text-xl font-semibold text-sky-700 mb-4 text-center">Rep of the Year (2019) - Omnicell</h3>
                    <p class="text-center text-stone-600 mb-6">Generated $31M in revenue against an $8M quota.</p>
                    <div class="chart-container">
                        <canvas id="quotaAchievementChart"></canvas>
                    </div>
                </div>
            </div>
        </section>

        <section id="education" class="py-16 px-4 sm:px-6 lg:px-8 bg-stone-50">
            <div class="max-w-4xl mx-auto">
                <h2 class="section-title">🎓 Education & Certifications</h2>
                <p class="text-center text-stone-600 mb-12 text-lg">Committed to continuous learning and staying at the forefront of industry advancements.</p>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-10">
                    <div class="card">
                        <h3 class="text-2xl font-semibold text-sky-700 mb-3">Education</h3>
                        <p class="text-lg font-medium text-stone-800">Portland State University</p>
                        <p class="text-md text-stone-600">Bachelor of Science, Business Administration (Marketing)</p>
                    </div>
                    <div class="card">
                        <h3 class="text-2xl font-semibold text-sky-700 mb-3">Certifications & Training</h3>
                        <ul class="space-y-2 text-stone-700">
                            <li><strong class="text-sky-600">Agentic AI for Business Leaders</strong> – Vanderbilt University</li>
                            <li><strong class="text-sky-600">OpenAI GPT Applications</strong> – Vanderbilt University</li>
                            <li><strong class="text-sky-600">GenAI for Executives</strong> – IBM</li>
                            <li><strong class="text-sky-600">AI Fundamentals</strong> – University of Pennsylvania</li>
                            <li>Challenger Sales</li>
                            <li>MEDDPICC</li>
                            <li>IMPACT Sales Process</li>
                            <li>Miller Heiman</li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>

        <section id="contact" class="py-16 px-4 sm:px-6 lg:px-8 bg-sky-700 text-white">
            <div class="max-w-3xl mx-auto text-center">
                <h2 class="text-3xl font-bold mb-6">📞 Get In Touch</h2>
                <p class="text-lg text-sky-100 mb-8">Let's connect and discuss how I can contribute to your organization's success.</p>
                <div class="space-y-4 md:space-y-0 md:flex md:justify-center md:space-x-6">
                    <a href="mailto:jtomin14@gmail.com" class="inline-block bg-white text-sky-700 font-semibold py-3 px-6 rounded-lg shadow-md hover:bg-sky-50 transition-colors">
                        📧 Email Me
                    </a>
                    <a href="https://www.linkedin.com/in/jontomin" target="_blank" rel="noopener noreferrer" class="inline-block bg-sky-500 text-white font-semibold py-3 px-6 rounded-lg shadow-md hover:bg-sky-400 transition-colors">
                        🔗 LinkedIn Profile
                    </a>
                     <a href="tel:+1-971-322-8264" class="inline-block bg-white text-sky-700 font-semibold py-3 px-6 rounded-lg shadow-md hover:bg-sky-50 transition-colors">
                        📱 Call Me
                    </a>
                </div>
            </div>
        </section>
    </main>

    <footer class="bg-stone-800 text-stone-300 text-center py-6">
        <p>&copy; 2025 Jon Tomin. Interactive Resume.</p>
    </footer>

    <script>
        // Mobile menu toggle
        const mobileMenuButton = document.getElementById('mobile-menu-button');
        const mobileMenu = document.getElementById('mobile-menu');
        mobileMenuButton.addEventListener('click', () => {
            mobileMenu.classList.toggle('hidden');
        });

        // Close mobile menu when a link is clicked
        const mobileNavLinks = document.querySelectorAll('.mobile-nav-link');
        mobileNavLinks.forEach(link => {
            link.addEventListener('click', () => {
                mobileMenu.classList.add('hidden');
            });
        });

        // Smooth scroll and active nav link highlighting
        const navLinks = document.querySelectorAll('.nav-link');
        const sections = document.querySelectorAll('section');

        function changeNav(targetSectionId) {
            navLinks.forEach(link => {
                link.classList.remove('active');
                if (link.dataset.section === targetSectionId) {
                    link.classList.add('active');
                }
            });
        }
        
        // Intersection Observer for active section highlighting
        const observerOptions = {
            root: null, // viewport
            rootMargin: '0px',
            threshold: 0.5 // 50% of the section is visible
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    const sectionId = entry.target.id;
                    changeNav(sectionId);
                }
            });
        }, observerOptions);

        sections.forEach(section => {
            observer.observe(section);
        });
        
        // Initial active link for summary
        if (window.location.hash === '' || window.location.hash === '#summary') {
             changeNav('summary');
        } else {
            changeNav(window.location.hash.substring(1));
        }


        // Experience details toggle
        const detailToggles = document.querySelectorAll('.toggle-details');
        detailToggles.forEach(toggle => {
            toggle.addEventListener('click', () => {
                const content = toggle.nextElementSibling; // Assumes ul is the next sibling
                content.classList.toggle('open');
                toggle.textContent = content.classList.contains('open') ? 'Hide Details \u2191' : 'Show Details \u2193';
            });
        });

        // Chart.js for Quota Achievement
        const ctx = document.getElementById('quotaAchievementChart').getContext('2d');
        const quotaAchievementChart = new Chart(ctx, {
            type: 'bar',
            data: {
                labels: ['Quota', 'Revenue Achieved'],
                datasets: [{
                    label: 'Sales Performance ($M)',
                    data: [8, 31], // Quota: $8M, Revenue: $31M
                    backgroundColor: [
                        'rgba(251, 146, 60, 0.6)', // Tailwind orange-400 with opacity
                        'rgba(56, 189, 248, 0.6)'  // Tailwind sky-400 with opacity
                    ],
                    borderColor: [
                        'rgba(251, 146, 60, 1)',
                        'rgba(56, 189, 248, 1)'
                    ],
                    borderWidth: 1
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                scales: {
                    y: {
                        beginAtZero: true,
                        title: {
                            display: true,
                            text: 'Amount in Millions ($M)'
                        }
                    }
                },
                plugins: {
                    legend: {
                        display: false // Hiding legend as it's clear from labels
                    },
                    tooltip: {
                        callbacks: {
                            label: function(context) {
                                let label = context.dataset.label || '';
                                if (label) {
                                    label += ': ';
                                }
                                if (context.parsed.y !== null) {
                                    label += '$' + context.parsed.y + 'M';
                                }
                                return label;
                            }
                        }
                    }
                },
                // Ensure labels are not cut off (Chart.js default behavior might sometimes do this)
                // This can be further fine-tuned if needed with padding options in layout
                layout: {
                    padding: {
                        bottom: 10 // Add some padding at the bottom if x-axis labels are long
                    }
                },
                // For wrapping long labels (though 'Quota' and 'Revenue Achieved' are short)
                // This is a more complex solution for Chart.js, often requiring custom plugins or specific version features.
                // For now, keeping labels concise.
                // If needed, a simpler approach for very long labels is to use arrays of strings:
                // labels: [['Long Label', 'Part 1'], ['Long Label', 'Part 2']]
            }
        });
    </script>
</body>
</html>
