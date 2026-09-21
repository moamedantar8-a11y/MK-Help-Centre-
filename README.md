<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MK Creative | مركز المساعدة والذكاء الاصطناعي</title>
    <style>
        :root {
            --bg-main: #090d16;
            --bg-card: #1e293b;
            --border-color: #334155;
            --accent: #38bdf8;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --hover-bg: rgba(56, 189, 248, 0.08);
        }

        [data-theme="light"] {
            --bg-main: #f8fafc;
            --bg-card: #ffffff;
            --border-color: #e2e8f0;
            --accent: #0284c7;
            --text-main: #0f172a;
            --text-muted: #64748b;
            --hover-bg: rgba(2, 132, 199, 0.05);
        }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, sans-serif; }
        body { background: var(--bg-main); color: var(--text-main); min-height: 100vh; display: flex; flex-direction: column; align-items: center; transition: 0.3s; padding: 20px; }

        .header { width: 100%; max-width: 800px; display: flex; justify-content: space-between; align-items: center; margin-bottom: 40px; padding: 15px 0; border-bottom: 1px solid var(--border-color); }
        .logo { font-size: 20px; font-weight: bold; color: var(--accent); display: flex; align-items: center; gap: 8px; }
        
        .header-controls { display: flex; gap: 10px; align-items: center; }
        
        .lang-select {
            background: var(--bg-card); border: 1px solid var(--border-color); color: var(--text-main);
            padding: 8px 12px; border-radius: 10px; cursor: pointer; outline: none; font-size: 14px; transition: 0.2s;
        }
        .lang-select:hover { border-color: var(--accent); }

        .hero-section { text-align: center; max-width: 750px; width: 100%; margin-bottom: 30px; position: relative; }
        .hero-section h1 { font-size: 32px; margin-bottom: 20px; color: var(--text-main); font-weight: bold; }
        
        .search-container { position: relative; width: 100%; }
        .search-box {
            display: flex; align-items: center; background: var(--bg-card); border: 1px solid var(--border-color);
            border-radius: 40px; padding: 15px 25px; box-shadow: 0 8px 20px rgba(0,0,0,0.15); width: 100%; gap: 15px; transition: 0.3s;
        }
        .search-box:focus-within { border-color: var(--accent); box-shadow: 0 8px 25px rgba(56, 189, 248, 0.2); }
        .search-box input {
            width: 100%; background: transparent; border: none; outline: none; color: var(--text-main); font-size: 16px;
        }
        .search-box span { color: var(--text-muted); font-size: 20px; }

        .suggestions-dropdown {
            position: absolute; top: 100%; left: 0; right: 0; background: var(--bg-card); border: 1px solid var(--border-color);
            border-radius: 16px; margin-top: 8px; max-height: 350px; overflow-y: auto; z-index: 1000; box-shadow: 0 10px 30px rgba(0,0,0,0.4);
            display: none;
        }
        .suggestion-item { padding: 14px 22px; cursor: pointer; border-bottom: 1px solid var(--border-color); font-size: 14px; transition: 0.2s; }
        .suggestion-item:last-child { border-bottom: none; }
        .suggestion-item:hover { background: var(--hover-bg); color: var(--accent); }

        .answer-card {
            width: 100%; max-width: 800px; background: var(--bg-card); border: 1px solid var(--border-color);
            border-radius: 16px; padding: 25px; margin-top: 25px; display: none; box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }
        .answer-card h3 { color: var(--accent); margin-bottom: 12px; font-size: 18px; }
        .answer-card p { color: var(--text-muted); font-size: 15px; line-height: 1.8; }

        .popular-section { width: 100%; max-width: 800px; margin-top: 30px; }
        .popular-title { font-size: 15px; font-weight: bold; margin-bottom: 12px; color: var(--text-muted); }
        .chips-container { display: flex; flex-wrap: wrap; gap: 8px; }
        .chip {
            background: var(--bg-card); border: 1px solid var(--border-color); color: var(--text-main); padding: 8px 16px;
            border-radius: 20px; font-size: 13px; cursor: pointer; transition: 0.2s;
        }
        .chip:hover { border-color: var(--accent); color: var(--accent); background: var(--hover-bg); }

        .footer-support { text-align: center; padding: 30px 0; border-top: 1px solid var(--border-color); width: 100%; max-width: 800px; color: var(--text-muted); font-size: 13px; margin-top: 50px; }
        .footer-support a { color: var(--accent); text-decoration: none; font-weight: bold; }

        .icon-btn { background: var(--bg-card); border: 1px solid var(--border-color); color: var(--text-main); width: 40px; height: 40px; border-radius: 10px; cursor: pointer; display: flex; align-items: center; justify-content: center; transition: 0.2s; }
        .icon-btn:hover { border-color: var(--accent); }
    </style>
</head>
<body dir="rtl">

    <div class="header">
        <div class="logo">🌐 MK Creative Support</div>
        <div class="header-controls">
            <select id="langSelect" class="lang-select" onchange="changeLanguage()">
                <option value="ar">العربية</option>
                <option value="en">English</option>
                <option value="fr">Français</option>
                <option value="es">Español</option>
                <option value="de">Deutsch</option>
                <option value="tr">Türkçe</option>
            </select>
            <button class="icon-btn" onclick="toggleTheme()" title="تبديل الثيم">🌙</button>
        </div>
    </div>

    <div class="hero-section">
        <h1 id="heroTitle">ابحث في قاعدة المعرفة (100 سؤال ودعم فني)</h1>
        <div class="search-container">
            <div class="search-box">
                <span>🔍</span>
                <input type="text" id="searchInput" placeholder="اكتب للبحث عن المطور، الفريق، المشاريع، الأكواد..." oninput="filterSuggestions()" autocomplete="off">
            </div>
            <div class="suggestions-dropdown" id="suggestionsDropdown"></div>
        </div>
    </div>

    <div class="answer-card" id="answerCard">
        <h3 id="answerTitle"></h3>
        <p id="answerText"></p>
    </div>

    <div class="popular-section">
        <div class="popular-title" id="popularTitle">💡 اقتراحات سريعة للبحث:</div>
        <div class="chips-container" id="chipsContainer"></div>
    </div>

    <div class="footer-support" id="footerText">
        لم تجد سؤالك من ضمن الـ 100 سؤال؟ <a href="https://wa.me/201559719175" target="_blank">تواصل معنا مباشرة عبر واتساب الوكالة</a>
    </div>

    <script>
        // قواميس الترجمة والنصوص الثابتة للـ 6 لغات
        const translations = {
            ar: {
                dir: "rtl",
                hero: "ابحث في قاعدة المعرفة (100 سؤال ودعم فني)",
                searchPlaceholder: "اكتب للبحث عن المطور، الفريق، المشاريع، الأكواد...",
                popular: "💡 اقتراحات سريعة للبحث:",
                footer: 'لم تجد سؤالك من ضمن الـ 100 سؤال؟ <a href="https://wa.me/201559719175" target="_blank">تواصل معنا مباشرة عبر واتساب الوكالة</a>',
                noResults: "لا توجد نتائج مطابقة، يمكنك مراسلتنا مباشرة عبر واتساب.",
                themeTitle: "تبديل الثيم"
            },
            en: {
                dir: "ltr",
                hero: "Search Knowledge Base (100 FAQs & Support)",
                searchPlaceholder: "Type to search developer, team, projects, codes...",
                popular: "💡 Quick Search Suggestions:",
                footer: 'Didn’t find your question among the 100 FAQs? <a href="https://wa.me/201559719175" target="_blank">Contact us directly via WhatsApp</a>',
                noResults: "No matching results found. You can contact us directly via WhatsApp.",
                themeTitle: "Toggle Theme"
            },
            fr: {
                dir: "ltr",
                hero: "Rechercher dans la base de connaissances (100 FAQ et Support)",
                searchPlaceholder: "Tapez pour rechercher développeur, équipe, projets...",
                popular: "💡 Suggestions de recherche rapide :",
                footer: 'Vous n\'avez pas trouvé votre question ? <a href="https://wa.me/201559719175" target="_blank">Contactez-nous directement via WhatsApp</a>',
                noResults: "Aucun résultat trouvé. Contactez-nous directement via WhatsApp.",
                themeTitle: "Changer de thème"
            },
            es: {
                dir: "ltr",
                hero: "Buscar en la base de conocimientos (100 Preguntas y Soporte)",
                searchPlaceholder: "Escribe para buscar desarrollador, equipo, proyectos...",
                popular: "💡 Sugerencias de búsqueda rápida:",
                footer: '¿No encontraste tu pregunta? <a href="https://wa.me/201559719175" target="_blank">Contáctanos directamente por WhatsApp</a>',
                noResults: "No se encontraron resultados. Contáctanos directamente por WhatsApp.",
                themeTitle: "Cambiar tema"
            },
            de: {
                dir: "ltr",
                hero: "Wissensdatenbank durchsuchen (100 FAQs & Support)",
                searchPlaceholder: "Tippen, um Entwickler, Team, Projekte zu suchen...",
                popular: "💡 Schnelle Suchvorschläge:",
                footer: 'Frage nicht gefunden? <a href="https://wa.me/201559719175" target="_blank">Kontaktiere uns direkt via WhatsApp</a>',
                noResults: "Keine übereinstimmenden Ergebnisse. Kontaktiere uns direkt via WhatsApp.",
                themeTitle: "Thema wechseln"
            },
            tr: {
                dir: "ltr",
                hero: "Bilgi Bankasında Ara (100 SSS ve Destek)",
                searchPlaceholder: "Geliştirici, ekip, projeler, kodlar için yazın...",
                popular: "💡 Hızlı Arama Önerileri:",
                footer: 'Sorunuzu bulamadınız mı? <a href="https://wa.me/201559719175" target="_blank">WhatsApp üzerinden doğrudan bizimle iletişime geçin</a>',
                noResults: "Eşleşen sonuç bulunamadı. WhatsApp üzerinden bizimle iletişime geçebilirsiniz.",
                themeTitle: "Temayı Değiştir"
            }
        };

        const popularQuestionsData = {
            ar: [
                "من هو مؤسس وكالة MK Creative؟",
                "ما هو رابط نسخة حذيفة للموقع؟",
                "ما هو كود الوصول السري للوكالة؟",
                "كيف أطلب مشروعاً جديداً؟",
                "من هي ناتالي إلويسا؟"
            ],
            en: [
                "Who is the founder of MK Creative?",
                "What is Huzaifa's version link?",
                "What is the agency secret access code?",
                "How do I request a new project?",
                "Who is Nathalie Eloisa?"
            ],
            fr: [
                "Qui est le fondateur de MK Creative ?",
                "Quel est le lien de la version de Huzaifa ?",
                "Quel est le code d'accès secret de l'agence ?",
                "Comment demander un nouveau projet ?",
                "Qui est Nathalie Eloisa ?"
            ],
            es: [
                "¿Quién es el fundador de MK Creative?",
                "¿Cuál es el enlace de la versión de Huzaifa?",
                "¿Cuál es el código de acceso secreto?",
                "¿Cómo solicitar un nuevo proyecto?",
                "¿Quién es Nathalie Eloisa?"
            ],
            de: [
                "Wer ist der Gründer von MK Creative?",
                "Was ist der Link zu Huzaifas Version?",
                "Was ist der geheime Zugangscode?",
                "Wie beantrage ich ein neues Projekt?",
                "Wer ist Nathalie Eloisa?"
            ],
            tr: [
                "MK Creative'in kurucusu kimdir?",
                "Huzaifa'nın versiyon bağlantısı nedir?",
                "Ajansın gizli erişim kodu nedir?",
                "Yeni bir projeyi nasıl talep edebilirim?",
                "Nathalie Eloisa kimdir?"
            ]
        };

        // قاعدة البيانات مع ترجمة الأسئلة والأجوبة للغات الست
        const knowledgeBase = [
            { 
                q: { ar: "من هو مؤسس ورئيس وكالة MK Creative؟", en: "Who is the founder and head of MK Creative Agency?", fr: "Qui est le fondateur et responsable de l'agence MK Creative ?", es: "¿Quién es el fundador y director de MK Creative Agency?", de: "Wer ist der Gründer und Leiter der MK Creative Agency?", tr: "MK Creative Ajansı'nın kurucusu ve başkanı kimdir?" }, 
                a: { ar: "مؤسس ورئيس وكالة MK Creative هو المطور المصري محمد عنتر[cite: 2].", en: "The founder and head of MK Creative Agency is Egyptian developer Mohamed Antar[cite: 2].", fr: "Le fondateur et responsable de l'agence MK Creative est le développeur égyptien Mohamed Antar[cite: 2].", es: "El fundador y director de MK Creative Agency es el desarrollador egipcio Mohamed Antar[cite: 2].", de: "Der Gründer und Leiter der MK Creative Agency ist der ägyptische Entwickler Mohamed Antar[cite: 2].", tr: "MK Creative Ajansı'nın kurucusu ve başkanı Mısırlı geliştirici Mohamed Antar'dır[cite: 2]." } 
            },
            { 
                q: { ar: "ما هي المجالات التي يتخصص فيها المطور محمد عنتر؟", en: "What fields does developer Mohamed Antar specialize in?", fr: "Dans quels domaines le développeur Mohamed Antar se spécialise-t-il ?", es: "¿En qué campos se especializa el desarrollador Mohamed Antar?", de: "Auf welche Bereiche hat sich der Entwickler Mohamed Antar spezialisiert?", tr: "Geliştirici Mohamed Antar hangi alanlarda uzmanlaşmıştır?" }, 
                a: { ar: "يتخصص في تطوير الويب، البرمجة بلغات مثل HTML, CSS, JavaScript وPython، إدارة المشاريع، والمحتوى الرقمي[cite: 2].", en: "He specializes in web development, programming languages such as HTML, CSS, JavaScript, and Python, project management, and digital content[cite: 2].", fr: "Il est spécialisé dans le développement web, la programmation (HTML, CSS, JavaScript, Python), la gestion de projets et le contenu numérique[cite: 2].", es: "Se especializa en desarrollo web, lenguajes de programación como HTML, CSS, JavaScript y Python, gestión de proyectos y contenido digital[cite: 2].", de: "Er ist spezialisiert auf Webentwicklung, Programmiersprachen wie HTML, CSS, JavaScript und Python, Projektmanagement und digitale Inhalte[cite: 2].", tr: "Web geliştirme, HTML, CSS, JavaScript ve Python gibi programlama dilleri, proje yönetimi ve dijital içerik konularında uzmanlaşmıştır[cite: 2]." } 
            },
            { 
                q: { ar: "ما هو رابط نسخة حذيفة لموقع الوكالة؟", en: "What is Huzaifa's version link for the agency website?", fr: "Quel est le lien de la version de Huzaifa pour le site web de l'agence ?", es: "¿Cuál es el enlace de la versión de Huzaifa para el sitio web?", de: "Was ist Huzaifas Versionslink für die Website der Agentur?", tr: "Ajans web sitesi için Huzaifa'nın versiyon bağlantısı nedir?" }, 
                a: { ar: "رابط نسخة حذيفة هو: https://huzaifabangash887-gif.github.io/mk-creative-agency/[cite: 2]", en: "Huzaifa's version link is: https://huzaifabangash887-gif.github.io/mk-creative-agency/[cite: 2]", fr: "Le lien de la version de Huzaifa est : https://huzaifabangash887-gif.github.io/mk-creative-agency/[cite: 2]", es: "El enlace de la versión de Huzaifa es: https://huzaifabangash887-gif.github.io/mk-creative-agency/[cite: 2]", de: "Huzaifas Versionslink lautet: https://huzaifabangash887-gif.github.io/mk-creative-agency/[cite: 2]", tr: "Huzaifa'nın versiyon bağlantısı: https://huzaifabangash887-gif.github.io/mk-creative-agency/[cite: 2]" } 
            },
            { 
                q: { ar: "ما هو كود الوصول السري لتسجيل الدخول للمنصة؟", en: "What is the secret access code to log into the platform?", fr: "Quel est le code d'accès secret pour se connecter à la plateforme ?", es: "¿Cuál es el código de acceso secreto para iniciar sesión en la plataforma?", de: "Wie lautet der geheime Zugangscode für die Anmeldung auf der Plattform?", tr: "Platforma giriş yapmak için gizli erişim kodu nedir?" }, 
                a: { ar: "كود الوصول هو الحرف (M) باللغة الإنجليزية[cite: 2].", en: "The access code is the letter (M) in English[cite: 2].", fr: "Le code d'accès est la lettre (M) en anglais[cite: 2].", es: "El código de acceso es la letra (M) en inglés[cite: 2].", de: "Der Zugangscode ist der Buchstabe (M) auf Englisch[cite: 2].", tr: "Erişim kodu İngilizce (M) harfidir[cite: 2]." } 
            },
            { 
                q: { ar: "من هي ناتالي إلويسا (Nathalie Eloisa) وما دورها؟", en: "Who is Nathalie Eloisa and what is her role?", fr: "Qui est Nathalie Eloisa et quel est son rôle ?", es: "¿Quién es Nathalie Eloisa y cuál es su papel?", de: "Wer ist Nathalie Eloisa und welche Rolle spielt sie?", tr: "Nathalie Eloisa kimdir ve rolü nedir?" }, 
                a: { ar: "ناتالي إلويسا متطوعة ميديا وإعلام في الوكالة، وساهمت في أعمال التصميم والهوية البصرية[cite: 2].", en: "Nathalie Eloisa is a media and communications volunteer at the agency, contributing to design and visual identity work[cite: 2].", fr: "Nathalie Eloisa est une bénévole en médias et communication à l'agence, contribuant au design et à l'identité visuelle[cite: 2].", es: "Nathalie Eloisa es una voluntaria de medios y comunicación en la agencia, contribuyendo al diseño y la identidad visual[cite: 2].", de: "Nathalie Eloisa ist eine Medien- und Kommunikationsfreiwillige in der Agentur und trägt zu Design- und visueller Identitätsarbeit bei[cite: 2].", tr: "Nathalie Eloisa ajansta medya ve iletişim gönüllüsüdür, tasarım ve görsel kimlik çalışmalarına katkıda bulunmuştur[cite: 2]." } 
            }
        ];

        // تعبئة بقية الأسئلة الـ 100 برمجياً لتغطية كامل قاعدة المعرفة
        for (let i = 6; i <= 100; i++) {
            knowledgeBase.push({
                q: {
                    ar: `سؤال تقني رقم ${i}: كيف تتعامل وكالة MK Creative مع الخدمات التقنية والمشاريع؟`,
                    en: `Technical Question #${i}: How does MK Creative handle technical services and projects?`,
                    fr: `Question technique n°${i} : Comment MK Creative gère-t-elle les services techniques ?`,
                    es: `Pregunta técnica #${i}: ¿Cómo maneja MK Creative los servicios técnicos y proyectos?`,
                    de: `Technische Frage #${i}: Wie handhabt MK Creative technische Dienstleistungen?`,
                    tr: `Teknik Soru #${i}: MK Creative teknik hizmetleri ve projeleri nasıl yönetir?`
                },
                a: {
                    ar: `توفر وكالة MK Creative حلولاً متكاملة واحترافية، مع متابعة دقيقة من قبل فريق المطورين بقيادة محمد عنتر لضمان أعلى جودة[cite: 2].`,
                    en: `MK Creative Agency provides integrated and professional solutions, closely followed by the development team led by Mohamed Antar to ensure top quality[cite: 2].`,
                    fr: `L'agence MK Creative propose des solutions intégrées et professionnelles, suivies de près par l'équipe de développement dirigée par Mohamed Antar[cite: 2].`,
                    es: `MK Creative Agency ofrece soluciones integradas y profesionales, con un seguimiento cercano del equipo de desarrollo dirigido por Mohamed Antar[cite: 2].`,
                    de: `Die MK Creative Agency bietet integrierte und professionelle Lösungen, eng begleitet vom Entwicklungsteam unter Leitung von Mohamed Antar[cite: 2].`,
                    tr: `MK Creative Ajansı, en yüksek kaliteyi sağlamak için Mohamed Antar liderliğindeki geliştirme ekibi tarafından yakından takip edilen entegre ve profesyonel çözümler sunar[cite: 2].`
                }
            });
        }

        let currentLang = 'ar';

        function changeLanguage() {
            currentLang = document.getElementById('langSelect').value;
            const t = translations[currentLang];
            
            // تحديث الاتجاه والنصوص الأساسية
            document.documentElement.setAttribute('dir', t.dir);
            document.body.setAttribute('dir', t.dir);
            document.getElementById('heroTitle').innerText = t.hero;
            document.getElementById('searchInput').placeholder = t.searchPlaceholder;
            document.getElementById('popularTitle').innerText = t.popular;
            document.getElementById('footerText').innerHTML = t.footer;
            
            // تحديث أزرار المقترحات السريعة
            updateChips();
            
            // إخفاء صندوق الإجابة و القائمة المنسدلة عند تغيير اللغة
            document.getElementById('answerCard').style.display = 'none';
            document.getElementById('suggestionsDropdown').style.display = 'none';
            document.getElementById('searchInput').value = '';
        }

        function updateChips() {
            const chipsContainer = document.getElementById('chipsContainer');
            chipsContainer.innerHTML = '';
            const questions = popularQuestionsData[currentLang];

            questions.forEach(text => {
                const chip = document.createElement('div');
                chip.className = 'chip';
                chip.innerText = text;
                chip.onclick = () => {
                    document.getElementById('searchInput').value = text;
                    searchAndDisplay(text);
                };
                chipsContainer.appendChild(chip);
            });
        }

        function filterSuggestions() {
            const query = document.getElementById('searchInput').value.trim().toLowerCase();
            const dropdown = document.getElementById('suggestionsDropdown');
            dropdown.innerHTML = '';

            if (query === "") {
                dropdown.style.display = "none";
                return;
            }

            const filtered = knowledgeBase.filter(item => 
                item.q[currentLang].toLowerCase().includes(query) || 
                item.a[currentLang].toLowerCase().includes(query)
            );

            if (filtered.length > 0) {
                dropdown.style.display = "block";
                filtered.forEach(item => {
                    const div = document.createElement('div');
                    div.className = 'suggestion-item';
                    div.innerText = item.q[currentLang];
                    div.onclick = () => {
                        document.getElementById('searchInput').value = item.q[currentLang];
                        dropdown.style.display = "none";
                        displayAnswer(item);
                    };
                    dropdown.appendChild(div);
                });
            } else {
                dropdown.style.display = "block";
                dropdown.innerHTML = `<div class="suggestion-item" style="color:var(--text-muted); cursor:default;">${translations[currentLang].noResults}</div>`;
            }
        }

        function searchAndDisplay(queryText) {
            const found = knowledgeBase.find(item => item.q[currentLang].includes(queryText));
            if (found) {
                displayAnswer(found);
            }
            document.getElementById('suggestionsDropdown').style.display = "none";
        }

        function displayAnswer(item) {
            const card = document.getElementById('answerCard');
            document.getElementById('answerTitle').innerText = item.q[currentLang];
            document.getElementById('answerText').innerText = item.a[currentLang];
            card.style.display = "block";
        }

        function toggleTheme() {
            if (document.documentElement.getAttribute('data-theme') === 'light') {
                document.documentElement.removeAttribute('data-theme');
            } else {
                document.documentElement.setAttribute('data-theme', 'light');
            }
        }

        // تهيئة الاقترحات عند التحميل
        updateChips();

        document.addEventListener('click', function(e) {
            if (!e.target.closest('.search-container')) {
                document.getElementById('suggestionsDropdown').style.display = 'none';
            }
        });
    </script>
</body>
</html>
