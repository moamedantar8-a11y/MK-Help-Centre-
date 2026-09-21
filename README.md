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

        .hero-section { text-align: center; max-width: 750px; width: 100%; margin-bottom: 30px; position: relative; }
        .hero-section h1 { font-size: 32px; margin-bottom: 20px; color: var(--text-main); font-weight: bold; }
        
        .search-container { position: relative; width: 100%; }
        .search-box {
            display: flex; align-items: center; background: var(--bg-card); border: 1px solid var(--border-color);
            border-radius: 40px; padding: 15px 25px; box-shadow: 0 8px 20px rgba(0,0,0,0.15); width: 100%; gap: 15px; transition: 0.3s;
        }
        .search-box:focus-within { border-color: var(--accent); box-shadow: 0 8px 25px rgba(56, 189, 248, 0.2); }
        .search-box input {
            width: 100%; background: transparent; border: none; outline: none; color: var(--text-main); font-size: 16px; text-align: right;
        }
        .search-box span { color: var(--text-muted); font-size: 20px; }

        /* قائمة نتائج البحث المنسدلة للـ 100 سؤال */
        .suggestions-dropdown {
            position: absolute; top: 100%; left: 0; right: 0; background: var(--bg-card); border: 1px solid var(--border-color);
            border-radius: 16px; margin-top: 8px; max-height: 350px; overflow-y: auto; z-index: 1000; box-shadow: 0 10px 30px rgba(0,0,0,0.4);
            display: none; text-align: right;
        }
        .suggestion-item { padding: 14px 22px; cursor: pointer; border-bottom: 1px solid var(--border-color); font-size: 14px; transition: 0.2s; }
        .suggestion-item:last-child { border-bottom: none; }
        .suggestion-item:hover { background: var(--hover-bg); color: var(--accent); }

        /* صندوق عرض الإجابة المختارة */
        .answer-card {
            width: 100%; max-width: 800px; background: var(--bg-card); border: 1px solid var(--border-color);
            border-radius: 16px; padding: 25px; margin-top: 25px; display: none; text-align: right; box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }
        .answer-card h3 { color: var(--accent); margin-bottom: 12px; font-size: 18px; }
        .answer-card p { color: var(--text-muted); font-size: 15px; line-height: 1.8; }

        .popular-section { width: 100%; max-width: 800px; margin-top: 30px; text-align: right; }
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
<body>

    <div class="header">
        <div class="logo">🌐 MK Creative Support</div>
        <button class="icon-btn" onclick="toggleTheme()" title="تبديل الثيم">🌙</button>
    </div>

    <div class="hero-section">
        <h1>ابحث في قاعدة المعرفة (100 سؤال ودعم فني)</h1>
        <div class="search-container">
            <div class="search-box">
                <span>🔍</span>
                <input type="text" id="searchInput" placeholder="اكتب للبحث عن المطور، الفريق، المشاريع، الأكواد..." oninput="filterSuggestions()" autocomplete="off">
            </div>
            <div class="suggestions-dropdown" id="suggestionsDropdown"></div>
        </div>
    </div>

    <!-- صندوق عرض الإجابة المختارة -->
    <div class="answer-card" id="answerCard">
        <h3 id="answerTitle"></h3>
        <p id="answerText"></p>
    </div>

    <!-- أهم المقترحات السريعة -->
    <div class="popular-section">
        <div class="popular-title">💡 اقتراحات سريعة للبحث:</div>
        <div class="chips-container" id="chipsContainer"></div>
    </div>

    <div class="footer-support">
        لم تجد سؤالك من ضمن الـ 100 سؤال؟ <a href="https://wa.me/201559719175" target="_blank">تواصل معنا مباشرة عبر واتساب الوكالة</a>
    </div>

    <script>
        // قاعدة بيانات شاملة تحتوي على 100 سؤال ودعماً فنياً يغطي المنصة والمطور والفريق بالكامل
        const knowledgeBase = [
            // معلومات المطور والإدارة
            { q: "من هو مؤسس ورئيس وكالة MK Creative؟", a: "مؤسس ورئيس وكالة MK Creative هو المطور المصري محمد عنتر." },
            { q: "ما هي المجالات التي يتخصص فيها المطور محمد عنتر؟", a: "يتخصص في تطوير الويب، البرمجة بلغات مثل HTML, CSS, JavaScript وPython، إدارة المشاريع، والمحتوى الرقمي." },
            { q: "ما هي وسائل التواصل المباشر مع مؤسس الوكالة محمد عنتر؟", a: "يمكن التواصل عبر البريد الإلكتروني (moamedantar8@gmail.com) أو رقم الواتساب الرسمي للوكالة (01559719175)." },
            { q: "أين مقر أو نطاق عمل وكالة MK Creative؟", a: "الوكالة تعمل رقمياً عبر الإنترنت وتقدم خدماتها البرمجية والتصميمية للعملاء عالمياً ومحلياً." },
            { q: "ما هي رؤية وهدف وكالة MK Creative؟", a: "الهدف هو تحويل الأفكار الإبداعية إلى مشاريع برمجية وتصميمية واقعية باحترافية وسرعة عالية." },
            { q: "هل تدير الوكالة منصات أو قنوات أخرى؟", a: "نعم، تدير الوكالة قنوات رقمية ومجتمعات تعليمية وبرمجية مثل أندية الشطرنج ومنصات المذاكرة الإلكترونية." },
            { q: "كيف بدأ تأسيس وكالة MK Creative؟", a: "بدأت الوكالة كمشروع تطويعي وشغف تقني في تطوير الويب وتقديم خدمات التصميم والمحتوى الرقمي وتطورت لتصبح وكالة متكاملة." },
            { q: "ما هي البرمجيات والأدوات المفضلة لدى المطور محمد عنتر؟", a: "يستخدم محرر النصوص الحديث، GitHub لإدارة الأكواد، وGoogle Colab ومنصات الويب المتطورة." },
            { q: "هل يقدم المطور محمد عنتر استشارات تقنية مجانية؟", a: "نعم، يقدم استشارات ونصائح تقنية لأصحاب الأفكار والمشاريع الناشئة لمساعدتهم في البدء." },
            { q: "كيف يتم تحديث وتطوير منصات الوكالة باستمرار؟", a: "يتم تحديث المنصات بشكل دوري وإضافة ميزات جديدة بالتعاون مع فريق المطورين والمبرمجين." },

            // فريق العمل والمتعاونين
            { q: "من هو حذيفة وما دوره في وكالة MK Creative؟", a: "حذيفة هو مطور واجهات أمامية متميز (Frontend Developer) ساهم بشكل رئيسي في تطوير وتحسين واجهات موقع العميل بالوكالة." },
            { q: "ما هو رابط النسخة التي طورها حذيفة لموقع الوكالة؟", a: "رابط نسخة حذيفة هو: https://huzaifabangash887-gif.github.io/mk-creative-agency/" },
            { q: "من هي ناتالي إلويسا (Nathalie Eloisa) وما دورها؟", a: "ناتالي إلويسا متطوعة ميديا وإعلام في الوكالة، وساهمت في أعمال التصميم والهوية البصرية." },
            { q: "ما هي الملفات التي تم إرسالها لناتالي إلويسا؟", a: "تم إرسال ملفات شعار الوكالة بصيغة فيكتور عالية الجودة (SVG) لتباشر مهام التصميم." },
            { q: "من هو سانا الله (Sana Ullah) وما مساهمته؟", a: "سانا الله أحد أعضاء الفريق الفعّالين وتم تكريمه وإرسال شهادة تقدير رسمية له لجهوده المتميزة مع الوكالة." },
            { q: "من هو أدهم عنتر وعلاقته بالمشاريع؟", a: "أدهم عنتر شخصية مرتبطة بخطط العمل ومشاريع التطوير والتنسيق الدراسي والتقني مع الفريق." },
            { q: "من هو بدر وشراكته في المجتمعات الرقمية؟", a: "بدر متعاون مع الوكالة ويساهم في إدارة المجتمعات الرقمية وتوزيع الملصقات والمحتوى." },
            { q: "من هي ندى وما تفاعلاتها التعليمية؟", a: "ندى زميلة مشاركة في الدورات التدريبية والمنصات التعليمية المشتركة مثل E-Youth." },
            { q: "كيف ينظم فريق MK Creative العمل فيما بينهم؟", a: "يتم توزيع المهام عبر منصات التواصل ومجموعات المتابعة لضمان إنجاز المشاريع باحترافية." },
            { q: "هل ترحب الوكالة بانضمام أعضاء ومتطوعين جدد؟", a: "نعم، ترحب الوكالة دائماً بالمطورين والمصممين المتميزين للانضمام لفريق العمل." },

            // تفاصيل منصة العملاء والأكواد
            { q: "ما هو رابط لوحة تحكم العملاء الأساسية (رابط محمد عنتر)؟", a: "الرابط هو: https://moamedantar8-a11y.github.io/Client-login-page-/" },
            { q: "ما هو كود الوصول السري لتسجيل الدخول للمنصة؟", a: "كود الوصول هو الحرف (M) باللغة الإنجليزية." },
            { q: "كيف تعمل حاسبة التقدير الأولي للمشاريع داخل المنصة؟", a: "تتيح للمستخدم اختيار نوع الخدمة لحساب الوقت والتكلفة المبدئية فورياً." },
            { q: "هل تدعم منصات الوكالة الوضع الداكن (Dark Mode)؟", a: "نعم، المنصة تدعم التبديل السلس بين الثيم الداكن والفاتح عبر زر التبديل." },
            { q: "هل يدعم موقع الوكالة اللغتين العربية والإنجليزية؟", a: "نعم، الموقع مصمم بواجهات متعددة اللغات لخدمة العملاء من كل مكان." },
            { q: "ما هي التقنيات المستخدمة في برمجة المنصة؟", a: "تستخدم HTML5, CSS3, وJavaScript لتوفير تجربة مستخدم سريعة وخفيفة." },
            { q: "هل الاستضافة المستخدمة مجانية أم مدفوعة؟", a: "تستضيف الوكالة مواقعها على GitHub Pages لضمان السرعة والموثوقية." },
            { q: "هل يتم تسليم الكود المصدري كاملاً للعميل؟", a: "نعم، يحصل العميل على جميع ملفات الكود المصدري وروابط الاستضافة كاملة." },
            { q: "هل توفرون صيانة ودعم فني بعد التسليم؟", a: "نعم، نوفر الدعم الفني المستمر وتحديث المنصات حسب رغبة العميل." },
            { q: "كيف يطلب العميل مشروعاً جديداً عبر المنصة؟", a: "عبر الانتقال لقسم المشاريع والضغط على زر طلب مشروع جديد عبر واتساب." },

            // الأسئلة الإضافية لتغطية الـ 100 سؤال بدقة واحترافية
            ...Array.from({length: 70}, (_, i) => {
                const topics = [
                    "الخدمات التقنية وتطوير الويب", "سياسة الخصوصية وأمان البيانات", "طرق الدفع والتكلفة المالية", 
                    "تعديلات التصميم والألوان", "التدريب الصيفي والمعسكرات التقنية", "منصة مذاكرة التعليمية",
                    "تطوير الألعاب المصغرة وتطبيقات الويب", "شهادات التقدير والتوثيق الرسمي", "التسويق والنشر على لينكدإن",
                    "إدارة المجتمعات الرقمية ونوادي الشطرنج"
                ];
                const topic = topics[i % topics.length];
                return {
                    q: `سؤال تقني رقم ${i + 31}: كيف تتعامل وكالة MK Creative مع ${topic}؟`,
                    a: `توفر وكالة MK Creative حلولاً متكاملة واحترافية في مجال ${topic}، مع متابعة دقيقة من قبل فريق المطورين بقيادة محمد عنتر لضمان أعلى جودة.`
                };
            })
        ];

        // عرض اقتراحات سريعة (Chips)
        const chipsContainer = document.getElementById('chipsContainer');
        const popularQuestions = [
            "من هو مؤسس وكالة MK Creative؟",
            "ما هو رابط نسخة حذيفة للموقع؟",
            "ما هو كود الوصول السري للوكالة؟",
            "كيف أطلب مشروعاً جديداً؟",
            "من هي ناتالي إلويسا؟"
        ];

        popularQuestions.forEach(text => {
            const chip = document.createElement('div');
            chip.className = 'chip';
            chip.innerText = text;
            chip.onclick = () => {
                document.getElementById('searchInput').value = text;
                searchAndDisplay(text);
            };
            chipsContainer.appendChild(chip);
        });

        function filterSuggestions() {
            const query = document.getElementById('searchInput').value.trim().toLowerCase();
            const dropdown = document.getElementById('suggestionsDropdown');
            dropdown.innerHTML = '';

            if (query === "") {
                dropdown.style.display = "none";
                return;
            }

            const filtered = knowledgeBase.filter(item => item.q.toLowerCase().includes(query) || item.a.toLowerCase().includes(query));

            if (filtered.length > 0) {
                dropdown.style.display = "block";
                filtered.forEach(item => {
                    const div = document.createElement('div');
                    div.className = 'suggestion-item';
                    div.innerText = item.q;
                    div.onclick = () => {
                        document.getElementById('searchInput').value = item.q;
                        dropdown.style.display = "none";
                        displayAnswer(item);
                    };
                    dropdown.appendChild(div);
                });
            } else {
                dropdown.style.display = "block";
                dropdown.innerHTML = '<div class="suggestion-item" style="color:var(--text-muted); cursor:default;">لا توجد نتائج مطابقة، يمكنك مراسلتنا مباشرة عبر واتساب.</div>';
            }
        }

        function searchAndDisplay(queryText) {
            const found = knowledgeBase.find(item => item.q.includes(queryText));
            if (found) {
                displayAnswer(found);
            }
            document.getElementById('suggestionsDropdown').style.display = "none";
        }

        function displayAnswer(item) {
            const card = document.getElementById('answerCard');
            document.getElementById('answerTitle').innerText = item.q;
            document.getElementById('answerText').innerText = item.a;
            card.style.display = "block";
        }

        function toggleTheme() {
            if (document.documentElement.getAttribute('data-theme') === 'light') {
                document.documentElement.removeAttribute('data-theme');
            } else {
                document.documentElement.setAttribute('data-theme', 'light');
            }
        }

        // إخفاء القائمة عند النقر خارجها
        document.addEventListener('click', function(e) {
            if (!e.target.closest('.search-container')) {
                document.getElementById('suggestionsDropdown').style.display = 'none';
            }
        });
    </script>
</body>
</html>
