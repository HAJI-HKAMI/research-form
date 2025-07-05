<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>المستشار خالد الحكمي - خبير الأبحاث العلمية</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;900&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Cairo', sans-serif;
            background-color: #0c1427;
            color: #e2e8f0;
            overflow-x: hidden;
        }
        #researchCanvas {
            cursor: pointer;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
        }
        .content-wrapper {
            position: relative;
            z-index: 1;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 2rem;
        }
        .glass-panel {
            background: rgba(12, 20, 39, 0.6);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 1rem;
            padding: 2rem;
        }
        .highlight-text {
            color: #38bdf8; /* sky-400 */
        }
        
        /* Modal Styles */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0, 0, 0, 0.7);
            display: flex;
            align-items: flex-start;
            justify-content: center;
            z-index: 50;
            overflow-y: auto;
            padding: 4rem 0;
        }
        .modal-content {
            background-color: white;
            color: #1f2937;
            border-radius: 1rem;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
            width: 90%;
            max-width: 56rem; /* max-w-3xl */
            position: relative;
        }
        .modal-close-btn {
            position: absolute;
            top: 1rem;
            left: 1rem;
            background: none;
            border: none;
            font-size: 2rem;
            color: #9ca3af;
            cursor: pointer;
            line-height: 1;
        }
        .modal-close-btn:hover {
            color: #1f2937;
        }

        /* Form Styles inside Modal */
        .form-header {
            background: linear-gradient(135deg, #005C97, #363795);
            color: white;
            padding: 2rem;
            border-top-left-radius: 1rem;
            border-top-right-radius: 1rem;
        }
        .form-label {
            font-weight: 600;
            color: #374151;
        }
        .form-input, .form-textarea, .form-select {
            background-color: #f9fafb;
            border: 1px solid #d1d5db;
            color: #111827;
            border-radius: 0.5rem;
            padding: 0.75rem;
            width: 100%;
            transition: border-color 0.2s, box-shadow 0.2s;
        }
        .form-input:focus, .form-textarea:focus, .form-select:focus {
            outline: none;
            border-color: #005C97;
            box-shadow: 0 0 0 3px rgba(0, 92, 151, 0.2);
        }
        .form-checkbox-label {
            display: flex;
            align-items: center;
            padding: 1rem;
            background-color: #f9fafb;
            border-radius: 0.5rem;
            border: 1px solid #d1d5db;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        .form-checkbox-label:hover {
            border-color: #005C97;
        }
        .form-checkbox:checked + .form-checkbox-label {
            background-color: #eef6fc;
            border-color: #005C97;
            font-weight: 600;
        }
        .form-checkbox {
            display: none;
        }
        .submit-btn {
            background-color: #005C97;
            color: white;
            font-weight: 700;
            padding: 0.75rem 1.5rem;
            border-radius: 0.5rem;
            transition: background-color 0.3s, transform 0.2s;
            width: 100%;
        }
        .submit-btn:hover {
            background-color: #363795;
            transform: translateY(-2px);
        }
        .required-star {
            color: #ef4444;
            font-weight: bold;
            margin-right: 2px;
        }
    </style>
</head>
<body>
    <canvas id="researchCanvas"></canvas>

    <div class="content-wrapper">
        <div class="glass-panel max-w-4xl">
            <h1 class="text-4xl md:text-6xl font-black mb-4">
                المستشار <span class="highlight-text">خالد الحكمي</span>
            </h1>
            <p class="text-xl md:text-2xl text-slate-300 mb-6 max-w-2xl mx-auto">
                خبير متخصص في الأبحاث العلمية والأكاديمية، بخبرة واسعة تمتد لسنوات، وإسهامات في نشر أكثر من <strong class="highlight-text text-3xl font-bold">300+</strong> بحث علمي.
            </p>
            <p class="text-lg text-slate-400 mb-8">
                نحوّل الأفكار البحثية المعقدة إلى دراسات رصينة ومؤثرة.
            </p>
            <button id="openFormBtn" class="inline-block bg-sky-500 text-white font-bold py-3 px-8 rounded-lg text-lg hover:bg-sky-600 transition-colors duration-300">
                ابدأ مشروعك البحثي
            </button>
        </div>
    </div>

    <!-- Form Modal -->
    <div id="formModal" class="modal-overlay hidden">
        <div class="modal-content">
            <button id="closeFormBtn" class="modal-close-btn">&times;</button>
            <div class="form-header text-center">
                <h1 class="text-3xl font-bold">نموذج طلب خدمة مساعدة بحثية</h1>
                <p class="mt-2 opacity-90">هذا النموذج هو خطوتنا الأولى معًا لفهم مشروعك البحثي بشكل أفضل.</p>
            </div>

            <form action="https://formspree.io/f/xblyedge" method="POST" class="p-8 space-y-8">
                <!-- Form content goes here -->
                <div class="space-y-6">
                    <h2 class="text-2xl font-bold border-b-2 border-gray-200 pb-2 text-gray-800">القسم الأول: معلومات أساسية</h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label for="fullName" class="form-label block mb-2">الاسم الكامل<span class="required-star">*</span></label>
                            <input type="text" name="fullName" id="fullName" class="form-input" placeholder="مثال: الدكتورة هيا المشحن" required>
                        </div>
                        <div>
                            <label for="email" class="form-label block mb-2">البريد الإلكتروني<span class="required-star">*</span></label>
                            <input type="email" name="email" id="email" class="form-input" placeholder="مثال: h.almashhan@example.com" required>
                        </div>
                    </div>
                     <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label for="phoneNumber" class="form-label block mb-2">رقم الجوال</label>
                            <input type="tel" name="phoneNumber" id="phoneNumber" class="form-input" placeholder="مثال: 0569965144">
                        </div>
                        <div>
                           <label for="degree" class="form-label block mb-2">الدرجة العلمية<span class="required-star">*</span></label>
                            <select id="degree" name="degree" class="form-select" required>
                                <option value="" disabled selected>اختر الدرجة العلمية...</option>
                                <option value="master">ماجستير</option>
                                <option value="phd">دكتوراه</option>
                                <option value="bachelor">بحث تخرج (بكالوريوس)</option>
                                <option value="paper">ورقة علمية للنشر</option>
                                <option value="other">أخرى</option>
                            </select>
                        </div>
                    </div>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label for="university" class="form-label block mb-2">الجامعة</label>
                            <input type="text" name="university" id="university" class="form-input" placeholder="مثال: جامعة الملك سعود">
                        </div>
                        <div>
                            <label for="major" class="form-label block mb-2">التخصص الجامعي</label>
                            <input type="text" name="major" id="major" class="form-input" placeholder="مثال: السياسات العامة والإدارة">
                        </div>
                    </div>
                    <div>
                        <label for="researchTitle" class="form-label block mb-2">عنوان البحث المعتمد<span class="required-star">*</span></label>
                        <textarea id="researchTitle" name="researchTitle" rows="3" class="form-textarea" placeholder="مثال: أثر التحول الرقمي على أداء القطاع العام في المدن الذكية" required></textarea>
                    </div>
                </div>
                <div class="space-y-6">
                    <h2 class="text-2xl font-bold border-b-2 border-gray-200 pb-2 text-gray-800">القسم الثاني: نطاق الخدمة المطلوبة</h2>
                     <p class="text-gray-600">ما هي طبيعة المساعدة التي تحتاجها؟ (يمكنك اختيار أكثر من خيار)<span class="required-star">*</span></p>
                     <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
                        <div><input type="checkbox" id="service1" name="service" value="Proposal" class="form-checkbox"><label for="service1" class="form-checkbox-label">إعداد خطة بحث (Proposal)</label></div>
                        <div><input type="checkbox" id="service2" name="service" value="Literature Review" class="form-checkbox"><label for="service2" class="form-checkbox-label">الإطار النظري والدراسات السابقة</label></div>
                        <div><input type="checkbox" id="service3" name="service" value="Methodology" class="form-checkbox"><label for="service3" class="form-checkbox-label">المنهجية والإجراءات</label></div>
                        <div><input type="checkbox" id="service4" name="service" value="Tool Development" class="form-checkbox"><label for="service4" class="form-checkbox-label">تطوير أدوات البحث (استبيان)</label></div>
                        <div><input type="checkbox" id="service5" name="service" value="Statistical Analysis" class="form-checkbox"><label for="service5" class="form-checkbox-label">التحليل الإحصائي (SPSS)</label></div>
                        <div><input type="checkbox" id="service6" name="service" value="Discussion" class="form-checkbox"><label for="service6" class="form-checkbox-label">مناقشة النتائج والتوصيات</label></div>
                        <div><input type="checkbox" id="service7" name="service" value="Proofreading" class="form-checkbox"><label for="service7" class="form-checkbox-label">تدقيق لغوي وتنسيق نهائي</label></div>
                        <div class="sm:col-span-2 lg:col-span-3"><input type="checkbox" id="service_full" name="service" value="Full Research" class="form-checkbox"><label for="service_full" class="form-checkbox-label text-center block w-full bg-blue-50">🚀 **إعداد البحث بالكامل (من الخطة إلى التسليم النهائي)**</label></div>
                     </div>
                </div>
                <div class="space-y-6">
                    <h2 class="text-2xl font-bold border-b-2 border-gray-200 pb-2 text-gray-800">القسم الثالث: المستندات والملفات المتاحة</h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label for="proposalFile" class="form-label block mb-2">خطة البحث المعتمدة</label>
                            <input type="file" name="proposalFile" id="proposalFile" class="form-input p-2">
                        </div>
                        <div>
                            <label for="styleGuideFile" class="form-label block mb-2">دليل الكتابة الخاص بالجامعة</label>
                            <input type="file" name="styleGuideFile" id="styleGuideFile" class="form-input p-2">
                        </div>
                    </div>
                </div>
                <div class="space-y-6">
                     <h2 class="text-2xl font-bold border-b-2 border-gray-200 pb-2 text-gray-800">القسم الرابع: تفاصيل إضافية</h2>
                     <div>
                           <label for="deadline" class="form-label block mb-2">متى موعد التسليم النهائي المطلوب؟<span class="required-star">*</span></label>
                           <input type="text" id="deadline" name="deadline" class="form-input" placeholder="DD/MM/YYYY" required>
                     </div>
                     <div>
                        <label for="supervisorNotes" class="form-label block mb-2">هل لديك أي ملاحظات محددة من مشرفك الأكاديمي؟</label>
                        <textarea id="supervisorNotes" name="supervisorNotes" rows="4" class="form-textarea" placeholder="اكتب هنا أي توجيهات أو نقاط تركيز طلبها مشرفك..."></textarea>
                     </div>
                </div>
                <div class="pt-6">
                    <button type="submit" class="submit-btn">إرسال الطلب</button>
                </div>
            </form>
        </div>
    </div>

    <script>
        // Interactive background script
        const canvas = document.getElementById('researchCanvas');
        const ctx = canvas.getContext('2d');
        let width, height;
        let nodes = [];
        const nodeCount = 50;
        const researchAreas = [
            'التحول الرقمي', 'السياسات العامة', 'الإدارة الحكومية', 'الذكاء الاصطناعي',
            'المدن الذكية', 'جودة الخدمات', 'التحليل الكمي', 'التحليل النوعي',
            'الاقتصاد السلوكي', 'الاستدامة البيئية', 'الأمن السيبراني', 'القانون الإداري',
            'رؤية 2030', 'إدارة المشاريع', 'الابتكار الاجتماعي'
        ];

        function Node(x, y, radius, label = '') {
            this.x = x;
            this.y = y;
            this.radius = radius;
            this.vx = (Math.random() - 0.5) * 0.5;
            this.vy = (Math.random() - 0.5) * 0.5;
            this.isLabelNode = !!label;
            this.label = label;
            this.color = this.isLabelNode ? 'rgba(56, 189, 248, 0.9)' : 'rgba(255, 255, 255, 0.5)';
        }

        function init() {
            width = canvas.width = window.innerWidth;
            height = canvas.height = window.innerHeight;
            nodes = [];
            for (let i = 0; i < nodeCount; i++) {
                const radius = Math.random() * 2 + 1;
                const x = Math.random() * width;
                const y = Math.random() * height;
                const label = i < researchAreas.length ? researchAreas[i] : '';
                nodes.push(new Node(x, y, label ? radius + 3 : radius, label));
            }
            animate();
        }

        function draw() {
            ctx.clearRect(0, 0, width, height);
            nodes.forEach(node => {
                ctx.beginPath();
                ctx.arc(node.x, node.y, node.radius, 0, Math.PI * 2);
                ctx.fillStyle = node.color;
                ctx.fill();
                if (node.isLabelNode) {
                    ctx.fillStyle = 'rgba(226, 232, 240, 0.9)';
                    ctx.font = '14px Cairo';
                    ctx.textAlign = 'center';
                    ctx.fillText(node.label, node.x, node.y - node.radius - 5);
                }
            });
            for (let i = 0; i < nodes.length; i++) {
                for (let j = i + 1; j < nodes.length; j++) {
                    const dist = Math.hypot(nodes[i].x - nodes[j].x, nodes[i].y - nodes[j].y);
                    if (dist < 150) {
                        ctx.beginPath();
                        ctx.moveTo(nodes[i].x, nodes[i].y);
                        ctx.lineTo(nodes[j].x, nodes[j].y);
                        ctx.strokeStyle = `rgba(255, 255, 255, ${1 - dist / 150})`;
                        ctx.stroke();
                    }
                }
            }
        }

        function update() {
            nodes.forEach(node => {
                node.x += node.vx;
                node.y += node.vy;
                if (node.x < 0 || node.x > width) node.vx *= -1;
                if (node.y < 0 || node.y > height) node.vy *= -1;
            });
        }

        function animate() {
            update();
            draw();
            requestAnimationFrame(animate);
        }
        window.addEventListener('resize', init);
        init();

        // Modal script
        const openFormBtn = document.getElementById('openFormBtn');
        const closeFormBtn = document.getElementById('closeFormBtn');
        const formModal = document.getElementById('formModal');

        openFormBtn.addEventListener('click', () => {
            formModal.classList.remove('hidden');
            // This line ensures the modal always opens scrolled to the top
            formModal.scrollTop = 0;
        });

        closeFormBtn.addEventListener('click', () => {
            formModal.classList.add('hidden');
        });

        // Close modal if clicking outside the content
        formModal.addEventListener('click', (event) => {
            if (event.target === formModal) {
                formModal.classList.add('hidden');
            }
        });
    </script>
</body>
</html>

