[Uploading 新建 文本文档.html…]()
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>时间之外的梅花坞</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@400;500;600;700&family=Inter:wght@300;400&display=swap" rel="stylesheet">
    <style>
        /* 全局变量 */
        :root {
            --bg-primary: #f9f6f0;
            --bg-secondary: #f0ebe0;
            --text-main: #3a362b;
            --text-sub: #726b5c;
            --accent: #b48c66;
            --accent-soft: #e8d8c4;
            --border: #d9cbb7;
            --shadow: rgba(180, 140, 102, 0.15);
            --overlay: rgba(0, 0, 0, 0.3);
            --work-overlay: rgba(255,255,255,0.95);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html, body {
            height: 100%;
            overflow: hidden;
            font-family: 'Noto Serif SC', serif;
            scroll-behavior: smooth;
        }

        /* 顶部全局导航 */
        .top-nav {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            padding: 15px 20px;
            background: rgba(255, 255, 255, 0.95);
            border-bottom: 1px solid var(--border);
            z-index: 999;
            display: flex;
            justify-content: center;
            gap: 30px;
            flex-wrap: wrap;
        }
        .nav-item {
            color: var(--accent);
            text-decoration: none;
            font-size: 1rem;
            padding: 5px 10px;
            border-radius: 4px;
            transition: all 0.3s ease;
            cursor: pointer;
        }
        .nav-item:hover {
            background: var(--accent-soft);
            color: var(--text-main);
        }

        /* 核心：分步页面容器 */
        .page-container {
            height: 100vh;
            width: 100vw;
            position: relative;
            padding-top: 60px; /* 为顶部导航留出空间 */
        }

        /* 每个分步页面样式（全屏） */
        .page {
            height: 100vh;
            width: 100vw;
            padding: 40px 20px 80px 20px; /* 底部留足翻页提示空间 */
            display: flex;
            flex-direction: column;
            justify-content: flex-start; /* 改为从顶部开始，避免内容被挤到下方 */
            align-items: center;
            position: absolute;
            top: 0;
            left: 0;
            opacity: 0;
            visibility: hidden;
            transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
            overflow-y: auto;
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
        }

        /* 当前激活的页面 */
        .page.active {
            opacity: 1;
            visibility: visible;
        }

        /* ========== 1. 封面页 ========== */
        .page-cover {
            background: url("https://picsum.photos/id/188/2000/1200") center/cover no-repeat;
            color: white;
            text-align: center;
            justify-content: center;
        }
        .page-cover::after {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: var(--overlay);
            z-index: -1;
        }
        .cover-title {
            font-size: 3.8rem;
            letter-spacing: 10px;
            margin-bottom: 30px;
            text-shadow: 0 2px 15px rgba(0,0,0,0.5);
            animation: fadeUp 1.5s ease 0.5s forwards;
            opacity: 0;
            transform: translateY(20px);
        }
        .cover-sub {
            font-size: 1.3rem;
            letter-spacing: 6px;
            text-shadow: 0 2px 10px rgba(0,0,0,0.5);
            animation: fadeUp 1.5s ease 1s forwards;
            opacity: 0;
            transform: translateY(20px);
            line-height: 2;
        }

        /* 底部翻页提示（核心：纯文字+箭头，无按钮） */
        .page-tip {
            position: absolute;
            bottom: 30px;
            font-size: 1.1rem;
            letter-spacing: 3px;
            animation: fadeIn 2s ease 2s forwards;
            opacity: 0;
            color: white;
            text-shadow: 0 2px 8px rgba(0,0,0,0.5);
            cursor: pointer;
            user-select: none;
        }
        .page-tip::after {
            content: "↓";
            display: block;
            margin-top: 10px;
            animation: bounce 1.5s infinite;
            font-size: 1.5rem;
        }
        /* 非封面页的翻页提示（适配浅色背景） */
        .non-cover-tip {
            color: var(--accent);
            text-shadow: 0 1px 3px rgba(0,0,0,0.2);
        }

        /* ========== 通用页面样式 ========== */
        .page-content {
            max-width: 1000px;
            width: 100%;
            background-color: rgba(255, 255, 255, 0.9);
            padding: 50px;
            border-radius: 8px;
            box-shadow: 0 4px 20px var(--shadow);
            margin-bottom: 20px;
            margin-top: 20px; /* 增加顶部边距，避免被导航栏遮挡 */
        }
        .page-title {
            font-size: 2.2rem;
            color: var(--accent);
            margin-bottom: 30px;
            padding-bottom: 10px;
            border-bottom: 2px solid var(--accent-soft);
            display: inline-block;
            letter-spacing: 2px;
        }

        /* ========== 2. 个人介绍页 ========== */
        .page-intro {
            background-image: url("https://picsum.photos/id/1039/2000/1200");
        }
        .intro {
            display: grid;
            grid-template-columns: 1fr 2fr;
            gap: 40px;
            align-items: center;
        }
        .intro-avatar {
            width: 100%;
            max-width: 280px;
            border-radius: 8px;
            box-shadow: 0 4px 15px var(--shadow);
            aspect-ratio: 3/4;
            object-fit: cover;
            margin: 0 auto;
            /* 替换为用户提供的图片链接 */
            background: url("https://p9-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/6e83f17baae841f2ba595cd105353af9.jpg~tplv-a9rns2rl98-image.png?lk3s=8e244e95&rcl=20260313201315231A14B0E22BE5356193&rrcfp=dafada99&x-expires=2089627995&x-signature=XxcLMXdhGFbOsFBbnd9BTF8Ja1M%3D") center/cover;
        }
        .intro-text p {
            margin-bottom: 25px;
            font-size: 1.1rem;
            line-height: 1.9;
            color: var(--text-main);
            white-space: pre-line; /* 保留换行 */
        }
        .intro-tag {
            display: inline-block;
            padding: 6px 18px;
            background-color: var(--accent-soft);
            color: var(--accent);
            border-radius: 20px;
            margin-right: 10px;
            margin-bottom: 10px;
            font-size: 0.95rem;
        }
        .thoughts {
            font-style: italic;
            color: var(--text-main);
            font-size: 1.2rem;
            padding: 25px;
            border-left: 3px solid var(--accent);
            margin: 30px 0;
            background-color: var(--bg-secondary);
            border-radius: 0 8px 8px 0;
            line-height: 2;
            letter-spacing: 1px;
        }

        /* ========== 3. 作品+名家展示页 ========== */
        .page-works-masters {
            background-image: url("https://picsum.photos/id/1036/2000/1200");
        }
        .works-section, .masters-section {
            margin-bottom: 60px;
        }
        .works-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
            gap: 35px;
            margin-top: 30px;
        }
        /* 作品卡片样式 */
        .work-card {
            background-color: var(--bg-primary);
            padding: 25px 20px;
            border-radius: 8px;
            border: 1px solid var(--border);
            transition: all 0.3s ease;
            cursor: pointer;
            height: 100%;
            display: flex;
            flex-direction: column;
        }
        .work-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 10px 25px var(--shadow);
            border-color: var(--accent);
        }
        .work-title {
            font-size: 1.3rem;
            color: var(--accent);
            margin-bottom: 12px;
            font-weight: 600;
            letter-spacing: 1px;
        }
        .work-type {
            font-size: 0.9rem;
            color: var(--text-sub);
            margin-bottom: 18px;
            display: block;
            padding-bottom: 10px;
            border-bottom: 1px dashed var(--border);
        }
        .work-excerpt {
            font-size: 0.98rem;
            color: var(--text-main);
            line-height: 1.8;
            flex: 1;
        }
        .work-more {
            margin-top: 10px;
            font-size: 0.9rem;
            color: var(--accent);
            font-style: italic;
        }

        /* 作品详情弹窗 */
        .work-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background: rgba(0,0,0,0.7);
            z-index: 9999;
            display: none;
            align-items: center;
            justify-content: center;
            padding: 30px;
            overflow-y: auto;
        }
        .work-modal.active {
            display: flex;
        }
        .modal-content {
            max-width: 900px;
            width: 100%;
            background: var(--work-overlay);
            border-radius: 8px;
            padding: 40px;
            box-shadow: 0 8px 30px rgba(0,0,0,0.3);
            position: relative;
        }
        .modal-close {
            position: absolute;
            top: 20px;
            right: 20px;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: var(--accent-soft);
            border: 1px solid var(--accent);
            color: var(--accent);
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            transition: all 0.3s ease;
        }
        .modal-close:hover {
            background: var(--accent);
            color: white;
        }
        .modal-title {
            font-size: 2rem;
            color: var(--accent);
            text-align: center;
            margin-bottom: 20px;
            letter-spacing: 2px;
        }
        .modal-sub {
            font-size: 1rem;
            color: var(--text-sub);
            text-align: center;
            margin-bottom: 30px;
            display: block;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--accent-soft);
        }
        .modal-text {
            font-size: 1.05rem;
            line-height: 2;
            color: var(--text-main);
            text-indent: 2em;
            margin-bottom: 20px;
        }
        /* 不同作品背景区分 */
        #modal1 {background: url("https://picsum.photos/id/142/2000/1200") center/cover no-repeat;}
        #modal2 {background: url("https://picsum.photos/id/162/2000/1200") center/cover no-repeat;}
        #modal3 {background: url("https://picsum.photos/id/122/2000/1200") center/cover no-repeat;}
        #modal4 {background: url("https://picsum.photos/id/112/2000/1200") center/cover no-repeat;}
        .modal-bg {
            padding: 30px;
            border-radius: 8px;
            background: var(--work-overlay);
        }

        /* 名家区域样式（已移除头像） */
        .masters-list {
            margin-top: 20px;
        }
        .master-item {
            padding: 20px;
            border-bottom: 1px dashed var(--border);
            transition: all 0.3s ease;
            border-radius: 8px;
        }
        .master-item:hover {
            background-color: var(--bg-secondary);
        }
        .master-item:last-child {
            border-bottom: none;
        }
        .master-info h4 {
            font-size: 1.1rem;
            color: var(--accent);
            margin-bottom: 5px;
        }
        .master-desc {
            font-size: 0.95rem;
            color: var(--text-sub);
            margin-bottom: 10px;
        }
        .master-quote {
            font-style: italic;
            color: var(--text-main);
            padding-left: 10px;
            border-left: 2px solid var(--accent-soft);
        }

        /* ========== 4. 阅读清单页（已更换背景） ========== */
        .page-reading {
            background-image: url("https://picsum.photos/id/1036/2000/1200");
        }
        .reading-list {
            list-style: none;
            margin-top: 20px;
            width: 100%;
        }
        .reading-item {
            padding: 15px 20px;
            border-bottom: 1px solid var(--border);
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.3s ease;
            border-radius: 8px;
            cursor: pointer;
        }
        .reading-item:hover {
            background-color: var(--bg-secondary);
            padding-left: 30px;
        }
        .reading-item:last-child {
            border-bottom: none;
        }
        .reading-name {
            font-size: 1.1rem;
        }
        .reading-author {
            font-size: 0.95rem;
            color: var(--text-sub);
        }
        .reading-desc {
            font-size: 0.9rem;
            color: var(--text-sub);
            margin-top: 5px;
            line-height: 1.6;
        }

        /* ========== 5. 联系我页 ========== */
        .page-contact {
            background-image: url("https://picsum.photos/id/1048/2000/1200");
        }
        .contact {
            text-align: center;
        }
        .contact-text {
            font-size: 1.1rem;
            margin-bottom: 40px;
            color: var(--text-sub);
            line-height: 1.8;
        }
        .contact-links {
            display: flex;
            justify-content: center;
            gap: 40px;
            flex-wrap: wrap;
            margin-bottom: 50px;
        }
        .contact-link {
            color: var(--accent);
            text-decoration: none;
            font-size: 1.2rem;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 10px;
            transition: all 0.3s ease;
        }
        .contact-link:hover {
            color: var(--text-main);
            transform: translateY(-5px);
        }
        .contact-icon {
            font-size: 2rem;
            margin-bottom: 10px;
        }
        .signature {
            margin-top: 50px;
            color: var(--text-sub);
            line-height: 1.8;
            font-size: 1rem;
            font-style: italic;
        }

        /* ========== 动画 ========== */
        @keyframes fadeUp {
            to { opacity: 1; transform: translateY(0); }
        }
        @keyframes fadeIn {
            to { opacity: 1; }
        }
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        /* ========== 响应式适配 ========== */
        @media (max-width: 768px) {
            .cover-title { font-size: 2.8rem; letter-spacing: 6px; }
            .cover-sub { font-size: 1.1rem; letter-spacing: 4px; }
            .page-content { padding: 30px; }
            .intro { grid-template-columns: 1fr; }
            .intro-avatar { max-width: 200px; margin-bottom: 20px; }
            .page-title { font-size: 1.8rem; }
            .contact-links { gap: 20px; flex-direction: column; }
            .top-nav { gap: 15px; font-size: 0.9rem; }
            .page-tip { font-size: 1rem; }
            .works-grid { grid-template-columns: 1fr; gap: 25px; }
            .modal-content { padding: 30px; }
            .modal-title { font-size: 1.6rem; }
        }

        @media (max-width: 500px) {
            .cover-title { font-size: 2.2rem; letter-spacing: 4px; }
            .page-content { padding: 20px; }
            .reading-item { flex-direction: column; align-items: flex-start; gap: 5px; }
            .modal-content { padding: 20px; }
            .modal-text { font-size: 1rem; line-height: 1.8; }
            .page-tip { font-size: 0.9rem; }
        }
    </style>
</head>
<body>
    <!-- 顶部全局导航 -->
    <nav class="top-nav">
        <span class="nav-item" onclick="switchPage(getCurrentPage(), 1)">封面</span>
        <span class="nav-item" onclick="switchPage(getCurrentPage(), 2)">关于我</span>
        <span class="nav-item" onclick="switchPage(getCurrentPage(), 3)">作品与名家</span>
        <span class="nav-item" onclick="switchPage(getCurrentPage(), 4)">近期阅读</span>
        <span class="nav-item" onclick="switchPage(getCurrentPage(), 5)">与我联结</span>
    </nav>

    <!-- 页面容器 -->
    <div class="page-container">
        <!-- ========== 1. 封面页 ========== -->
        <div class="page page-cover active" id="page1">
            <h1 class="cover-title">时间之外的梅花坞</h1>
            <p class="cover-sub">和我一起逃到过去，不要被时间发现</p>
            <!-- 保留封面页的翻页提示 -->
            <p class="page-tip" onclick="goNextPage()">点击进入</p>
        </div>

        <!-- ========== 2. 个人介绍页（已分行） ========== -->
        <div class="page page-intro" id="page2">
            <div class="page-content">
                <h2 class="page-title">关于我</h2>
                <div class="intro">
                    <div class="intro-avatar"></div>
                    <div class="intro-text">
                        <p>李晨旭，笔名杨筱，武汉大学2024级商科本科生，文学爱好者。现任院文艺部职委、太阳雨文学社编辑部部长，曾任汉阳树文学社社长。创作涵盖散文、诗歌，作品多次获省市级奖项。
如果可以，我希望我们从未相遇，只如千千万万擦肩而过的沉默者，在茫茫人海中彼此遗忘。如果可以，希望你未曾读过我写下的文字——那些不过是一个浅薄之人对生活的浮光掠影，一场无心的戏谑。倘若我们不幸相遇，那我祝愿你永远幸福。</p>
                        <div class="intro-tag-group">
                            <span class="intro-tag">散文创作</span>
                            <span class="intro-tag">诗歌创作</span>
                            <span class="intro-tag">文学编辑</span>
                            <span class="intro-tag">商科在读</span>
                        </div>
                    </div>
                </div>
                <div class="thoughts">
                    树是生活，埋的是我；看花就好，别看我落魄…
                </div>
            </div>
            <!-- 移除该页面的翻页提示 -->
        </div>

        <!-- ========== 3. 作品+名家展示页（已移除头像+新增叶嘉莹） ========== -->
        <div class="page page-works-masters" id="page3">
            <div class="page-content">
                <div class="works-section">
                    <h2 class="page-title">我的作品</h2>
                    <div class="works-grid">
                        <!-- 作品1：再访桃花源 -->
                        <div class="work-card" onclick="openModal(1)">
                            <h3 class="work-title">再访桃花源</h3>
                            <span class="work-type">散文 | 解构意义下的重构</span>
                            <p class="work-excerpt">作为田园诗的巨擘，陶渊明的文字以其独有的清新、自然、淳朴，得到了后世文人的顶礼膜拜。模仿笔触，感慨田园者多；隔世遥望，饮酒和诗者多。其创作的《桃花源记》，更是具有永恒的艺术审美价值，“桃花源”成为了后世之人遥不可及的“温柔乡”。</p>
                            <p class="work-excerpt">桃花源中的生活样态，是陶渊明理想中的世界：“土地平旷，屋舍俨然，有良田美池桑竹之属。阡陌交通，鸡犬相闻。其中往来种作，男女衣着，悉如外人。黄发垂髫，并怡然自乐。”不难发现，桃花源中的生活与老子的“小国寡民”政治理想不谋而合，无战、安民是其核心，亦是封建时期普罗大众的夙愿。</p>
                            <p class="work-excerpt">和平繁华在封建时代往往是例外，战火纷争却是常态。在历史的周期律下，敏感的文人一次次希望又一次次绝望，用文字搭建起精神的桥梁，让流离失所的人们窥见“信念”的模样。</p>
                            <p class="work-more">详情请见公众号「时间之外的梅花坞」</p>
                        </div>
                        <!-- 作品2：天鹅之歌 -->
                        <div class="work-card" onclick="openModal(2)">
                            <h3 class="work-title">天鹅之歌</h3>
                            <span class="work-type">散文 | 命运的交响曲</span>
                            <p class="work-excerpt">传说，天鹅在临死之前会发出它这一生当中最凄美的叫声，也许是因为它知道自己时间不多了，所以要把握这最后的时光，将它最美好的一面毫不保留地完全表现出来。读到这段话，我莫名想到了贝多芬，当体悟了生命必然的悲剧性，面对命运的压迫，我们发出的怒吼又何尝不是一首天鹅之歌呢？</p>
                            <p class="work-excerpt">作为十八世纪维也纳古典乐派代表人物，贝多芬以其天才的创作手法，用交响的旋律诉说着自己对于世界喷薄而出的感情，而在其个体性背后，我们又能看到人类面对苦难时的顽强、偶遇英雄时的敬意，对爱情的矢志不渝、对理想的上下求索。</p>
                            <p class="work-excerpt">贝多芬在第五交响曲第一乐章的乐谱上，用一行小字写着“命运在敲门”。于是我们不禁发问，什么是命运？当一个人仕途顺畅、人生得意时，鲜少提到这是“命运”；反而是郁郁不得志、遭遇苦难时，才会将一切归罪于“命运”。</p>
                            <p class="work-more">详情请见公众号「时间之外的梅花坞」</p>
                        </div>
                        <!-- 作品3：逝者无情，人间有情 -->
                        <div class="work-card" onclick="openModal(3)">
                            <h3 class="work-title">逝者无情，人间有情</h3>
                            <span class="work-type">读书札记 | 读《逝川》有感</span>
                            <p class="work-excerpt">人只能守着逝川的一段，守住的就活下去、老下去，守不住的就成为它岸边的坟冢听它的水声，依然望着它。极北之地，藏在世俗之外的一个诗意的村庄里，流传着一个美丽的传说：捕到泪鱼的人家将会平安、无灾。这个朴素愿望的背后，是人们对平淡生活的热爱。</p>
                            <p class="work-excerpt">小说中自然景物始终与人物情感、命运紧密相连：“逝川日日夜夜地流，吉喜一天天的苍老，两岸的树林却愈发蓊郁了”，以河流的永恒、树林的繁茂与吉喜的衰老形成对比，无一字写孤独，却处处透着孤独。</p>
                            <p class="work-excerpt">初雪覆盖的阿甲村，“红松木栅栏上顶着的雪像是温柔的火焰一样瑰丽”，岸边的篝火“远远看去像是一只只金碗在闪闪发光”，洁白的雪、温暖的火与蓝色的泪鱼相互映衬，构成一幅纯净而忧伤的画面，既烘托出生命的美好，也暗示着其脆弱。</p>
                            <p class="work-more">详情请见公众号「时间之外的梅花坞」</p>
                        </div>
                        <!-- 作品4：重山 -->
                        <div class="work-card" onclick="openModal(4)">
                            <h3 class="work-title">重山</h3>
                            <span class="work-type">小说 | 神不在殿中，而在回头处</span>
                            <p class="work-excerpt">风声是第一个征兆。它穿过山坳，像一声悠长而破碎的叹息，缠绕在他早已疲惫的脚踝上。他抬起头，前方那座废弃的土地庙，在暮色里只剩下一个歪斜的轮廓。庙门早已朽烂，虚掩着一道深不见底的黑暗。</p>
                            <p class="work-excerpt">目光适应了昏暗后，他看见角落那尊神像。彩漆剥落，面容模糊，只有那双石雕的眼睛，空洞地望着远山之外的世界，三个蒲团散在佛像前，布面烂得露出里面的枯草，还沾着深色的霉斑。</p>
                            <p class="work-excerpt">打开窗后，凌冽的风不请自来，这年轻人却任由这刀剑造访他的脸颊，倔强地保持着最后一丝清醒。尽管如此，倦意仍如潮水般漫上，将他推向一个熟悉又陌生的地方——低矮的楼房，蜿蜒的小路，是他记忆里童年的轮廓。</p>
                            <p class="work-more">详情请见公众号「时间之外的梅花坞」</p>
                        </div>
                    </div>
                </div>

                <div class="masters-section">
                    <h2 class="page-title">心向往之的文学名家</h2>
                    <div class="masters-list">
                        <div class="master-item">
                            <div class="master-info">
                                <h4>鲁迅</h4>
                                <p class="master-desc">中国现代文学奠基人，以笔为刃，唤醒国民灵魂</p>
                                <p class="master-quote">"横眉冷对千夫指，俯首甘为孺子牛。"</p>
                            </div>
                        </div>
                        <div class="master-item">
                            <div class="master-info">
                                <h4>闻一多</h4>
                                <p class="master-desc">新月派代表诗人、学者，用诗歌与生命诠释爱国情怀</p>
                                <p class="master-quote">"为什么我的眼里常含泪水？因为我对这土地爱得深沉…"</p>
                            </div>
                        </div>
                        <div class="master-item">
                            <div class="master-info">
                                <h4>骆玉明</h4>
                                <p class="master-desc">复旦大学中文系教授，古典文学研究大家，文风温润通透</p>
                                <p class="master-quote">"文学是对生命的温柔凝视，让我们在喧嚣中听见内心的回响。"</p>
                            </div>
                        </div>
                        <div class="master-item">
                            <div class="master-info">
                                <h4>叶嘉莹</h4>
                                <p class="master-desc">中国古典诗词大家，一生致力于诗词传承，以温柔力量点亮诗词之美</p>
                                <p class="master-quote">"以诗为灯，照亮自己，也照亮他人。"</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <!-- 移除该页面的翻页提示 -->
        </div>

        <!-- ========== 4. 阅读清单页（已更新为你当前在读，补充刘再复作者信息） ========== -->
        <div class="page page-reading" id="page4">
            <div class="page-content">
                <h2 class="page-title">近期阅读</h2>
                <ul class="reading-list">
                    <li class="reading-item" onclick="alert('《古船》：张炜代表作，以胶东半岛洼狸镇为舞台，书写中国农民的命运与历史的沉重。小说通过隋、赵、李三大家族的兴衰，展现了从土改到改革开放四十余年的中国乡村变迁，既有对历史的深刻反思，也有对人性的复杂描摹。')">
                        <div>
                            <span class="reading-name">《古船》</span>
                            <p class="reading-desc">张炜 | 乡土中国的史诗，家族兴衰与时代阵痛的交织</p>
                        </div>
                        <span class="reading-author">张炜</span>
                    </li>
                    <li class="reading-item" onclick="alert('《日瓦格医生》：帕斯捷尔纳克代表作，1958年诺贝尔文学奖获奖作品。以医生日瓦格的视角，见证俄国革命与战争中的人性与爱情，探讨了个人在历史洪流中的命运与坚守。')">
                        <div>
                            <span class="reading-name">《日瓦格医生》</span>
                            <p class="reading-desc">帕斯捷尔纳克 | 战争与革命中的个体命运，诗意与苦难的永恒对话</p>
                        </div>
                        <span class="reading-author">帕斯捷尔纳克</span>
                    </li>
                    <li class="reading-item" onclick="alert('《纯粹理性批判》：康德经典哲学著作，西方哲学史上的里程碑式作品。康德在书中探讨人类认知的边界与先验逻辑的基础，试图为理性划定界限，回答"人能够知道什么"的根本问题。')">
                        <div>
                            <span class="reading-name">《纯粹理性批判》</span>
                            <p class="reading-desc">康德 | 西方哲学的里程碑，为人类理性划定界限</p>
                        </div>
                        <span class="reading-author">康德</span>
                    </li>
                    <li class="reading-item" onclick="alert('《文学慧悟十八点》：刘再复先生的文学随笔集，从古典到现代，拆解文本背后的生命智慧。书中以通透的视角解读文学经典，探讨文学与人生的本质联系，是理解文学与生命的佳作。')">
                        <div>
                            <span class="reading-name">《文学慧悟十八点》</span>
                            <p class="reading-desc">刘再复 | 以通透之眼，洞见文学与人生的本质</p>
                        </div>
                        <span class="reading-author">刘再复</span>
                    </li>
                </ul>
            </div>
            <!-- 移除该页面的翻页提示 -->
        </div>

        <!-- ========== 5. 联系我页（已更新邮箱+移除公众号二维码+修改签名） ========== -->
        <div class="page page-contact" id="page5">
            <div class="page-content contact">
                <h2 class="page-title">与我联结</h2>
                <p class="contact-text">若你也偏爱文字，愿与我交流创作与阅读的点滴，欢迎联系</p>
                <div class="contact-links">
                    <a href="mailto:15871690453@163.com" class="contact-link">
                        <span class="contact-icon">📧</span>
                        邮箱：15871690453@163.com
                    </a>
                    <a href="https://mp.weixin.qq.com/s/你的公众号文章链接" class="contact-link">
                        <span class="contact-icon">📖</span>
                        公众号：时间之外的梅花坞
                    </a>
                </div>
                <!-- 修改签名文字 -->
                <div class="signature">
                    愿我们都能找到一个春天
                </div>
            </div>
            <!-- 移除该页面的翻页提示 -->
        </div>
    </div>

    <!-- 作品1详情弹窗 -->
    <div class="work-modal" id="modal1">
        <div class="modal-content">
            <div class="modal-close" onclick="closeModal()">×</div>
            <div class="modal-bg">
                <h3 class="modal-title">再访桃花源</h3>
                <span class="modal-sub">解构意义下的重构 | 原创 杨筱 时间之外的梅花坞</span>
                <p class="modal-text">作为田园诗的巨擘，陶渊明的文字以其独有的清新、自然、淳朴，得到了后世文人的顶礼膜拜。模仿笔触，感慨田园者多；隔世遥望，饮酒和诗者多。其创作的《桃花源记》，更是具有永恒的艺术审美价值，“桃花源”成为了后世之人遥不可及的“温柔乡”。</p>
                <p class="modal-text">桃花源中的生活样态，是陶渊明理想中的世界：“土地平旷，屋舍俨然，有良田美池桑竹之属。阡陌交通，鸡犬相闻。其中往来种作，男女衣着，悉如外人。黄发垂髫，并怡然自乐。”不难发现，桃花源中的生活与老子的“小国寡民”政治理想不谋而合，无战、安民是其核心，亦是封建时期普罗大众的夙愿。</p>
                <p class="modal-text">和平繁华在封建时代往往是例外，战火纷争却是常态。在历史的周期律下，敏感的文人一次次希望又一次次绝望，用文字搭建起精神的桥梁，让流离失所的人们窥见“信念”的模样。费孝通在《乡土中国》中指出，农耕文明的本质是“生于斯、长于斯”的定居模式，土地的不可移动性决定了农民“安土重迁”，而农业与家族的绑定，又形成了“乐业”的精神依托，“小国寡民”恰是解决了封建百姓的“生存”与“发展”问题。</p>
                <p class="modal-text">弗洛伊德的精神分析理论指出，“创作是成年人的游戏替代品”，文学创作本质上是人类对精神世界的补偿性重构。陶渊明借“桃花源人衣着悉如外人”的细节，说“人相近”之实，他用另一条时间线给出答案：只有跳出“传统的社会”，才能真正远离纷争。而他面对的，是政治诡谲、民生凋敝的现实，将自己从这样的社会中抽离，才是他寻找答案的方式。</p>
                <p class="modal-text">《桃花源记》中的渔夫，褪去了传统隐逸形象的外衣，拷上了世俗的枷锁。他未遵守与村中人“不足为外人道也”的约定，反而“处处志之”“诣太守，说如此”，邀名市誉的行为，与传统渔父的精神形成罅隙，可见其并非“纯洁”的符号。而陶渊明以“桃花”命名这一理想世界，因桃花在《山海经》中是鬼怪屏障，在道教中是驱邪符号，本身便是纯洁的代表。</p>
                <p class="modal-text">桃花源中的人们“不知有汉，无论魏晋”，未经历外界的动荡与苦难，善良淳朴如桃花般纯洁，而桃花源也是陶渊明的政治理想，与现实的黑暗形成鲜明对比。他五次出仕又五次辞官，并非无建功立业之心，而是在君不君、臣不臣的世道中，保持自身的独立性已成奢望。他向世俗认输，而后逃跑，这看似消极的躲避，背后是无尽的落差、不甘与血泪，桃花源便成了他精神的最后一块净土。</p>
                <p class="modal-text">桃花源更有着“一去无返”的保护机制，渔夫“处处志之”却“不复得路”，南阳刘子骥寻之未果抱憾而亡，这是陶渊明对理想世界的守护。若大批外人涌入，“小国寡民”的美好便会被打破，而桃花源的存在，本就依托于现世的苦难——若现实安居乐业，桃花源便失去了存在的必然性。它是陶渊明的精神世界，容不得世俗的玷污。</p>
                <p class="modal-text">整篇故事以高尚之士刘子骥的死亡收束，充满了强烈的悲剧性，最终“后遂无问津者”，陶渊明的政治理想，终究被历史掩盖。而中国人的实用主义与冷峻，也让桃花源只留存在文人骚客的笔墨觥筹之间。陶渊明在挽歌中言：“死去何所道，托体同山阿。”这既是对死亡的淡然，亦是对世俗的无奈，而那份藏在桃花源中的理想，却成为了后世文人永恒的精神慰藉。</p>
            </div>
        </div>
    </div>

    <!-- 作品2详情弹窗 -->
    <div class="work-modal" id="modal2">
        <div class="modal-content">
            <div class="modal-close" onclick="closeModal()">×</div>
            <div class="modal-bg">
                <h3 class="modal-title">天鹅之歌</h3>
                <span class="modal-sub">命运的交响曲 | 原创 杨筱 时间之外的梅花坞</span>
                <p class="modal-text">传说，天鹅在临死之前会发出它这一生当中最凄美的叫声，也许是因为它知道自己时间不多了，所以要把握这最后的时光，将它最美好的一面毫不保留地完全表现出来。读到这段话，我莫名想到了贝多芬，当体悟了生命必然的悲剧性，面对命运的压迫，我们发出的怒吼又何尝不是一首天鹅之歌呢？</p>
                <p class="modal-text">作为十八世纪维也纳古典乐派代表人物，贝多芬以其天才的创作手法，用交响的旋律诉说着自己对于世界喷薄而出的感情，而在其个体性背后，我们又能看到人类面对苦难时的顽强、偶遇英雄时的敬意，对爱情的矢志不渝、对理想的上下求索。贝多芬赋予人类离合悲喜、命途多舛以更崇高的意蕴，完成了对人类普遍困境的体思。</p>
                <p class="modal-text">贝多芬在第五交响曲第一乐章的乐谱上，用一行小字写着“命运在敲门”。于是我们不禁发问，什么是命运？当一个人仕途顺畅、人生得意时，鲜少提到这是“命运”；反而是郁郁不得志、遭遇苦难时，才会将一切归罪于“命运”。美好转瞬即逝，痛苦却层出不穷，追问到最后无因可寻，便只得怪罪于这一超自然物，“命运”一词自诞生之初，便带着人类对生命的思考而充满着悲剧色彩。</p>
                <p class="modal-text">西方的“命运观”有着“命不可改”的显著特点，这源于古希腊的地理环境与文化积淀。希腊陆地多山少田，农业难以维系，大海虽提供了谋生途径，却也暗藏致命危险，地理环境的张力让希腊人对自然充满敬畏，形成了“命运高于神权”的认知。古希腊神话中，命运三女神的裁决宙斯无法干预，阿克琉斯、赫克托尔、俄狄浦斯王，皆逃不过命运的束缚，他们积极对抗却终究落败，这是古希腊人对人生无常的悲鸣。</p>
                <p class="modal-text">既然命不可改，我们该以何种态度面对？顺应命运可审时度势，对抗命运则在毁灭中塑造崇高，强者与弱者并无高低之分，不过是选择不同。贝多芬的一生，便是对抗命运的一生。他年少成名，前半生风光无限，可命运却接连给予重击：爱情失意终身未娶，家庭变故错失机遇，听力衰弱受尽煎熬，最终的水肿病让他苦不堪言。他的一辈子充斥着贫穷、失意与绝望，可他却说：卓越的人的一大优点是在不利和艰难的遭遇里百折不挠。</p>
                <p class="modal-text">恩格斯曾评价《命运交响曲》：“要是没有听过这部壮丽的作品的话，那么你这一生可以说是什么作品也没听过。”舒曼亦言：“不论你听过多少遍，都会像自然现象一样产生新的敬仰和惊叹。”这部作品被解读为“面对命运-抗争命运-赢得命运”的过程，而在旋律的背后，是贝多芬对命运最热烈的反抗。</p>
                <p class="modal-text">第一乐章的“短-短-短-长”是命运的敲门声，紧张的C小调将不安感推向极致，命运试图摧毁一切；第二乐章是灵魂的复活，优美的旋律中窥见希望的影子，灵魂在低谷中攀升；第三乐章是重生后的追问与再战，命运再次张牙舞爪，而灵魂的反抗愈发激烈，蛰伏的力量即将爆发；第四乐章是胜利的凯歌，C大调的英雄进行曲振奋人心，命运被击倒，抗争者迎来凯旋。</p>
                <p class="modal-text">可现实并非乐曲，人类往往是一次次被命运打倒，又一次次爬起，谁也无法真正“扼住命运的咽喉”，不过是在抗争中安慰自我的精神存续。贝多芬的胜利，终究只存在于音符之中，可他却为我们提供了面对命运的另一种途径——直面苦难，永不屈服。这种抗争呈现出悲壮色彩，因它揭示了有限与无限的对抗，肉身的脆弱反衬精神的超越，物质的湮灭凸显价值的永恒。</p>
                <p class="modal-text">命运与生命相对，向生命炫耀淫威；命运又与精神相应，证明着精神的密度。生命在命运下饱受磨难，精神却在命运下变得崇高坚韧，生命的悲剧转化为精神的厚度，精神在命运的注视下飞升。明知不可为而为之，除了鲁莽的愚蠢，更有大义凛然的勇气，在西西弗斯式的抗争中，结果早已不重要，我们在荒诞的抗争中找到了生命的尊严，而这份直面命运的精神，早已超越了交响曲本身，彰显了人类永恒的斗争精神。</p>
            </div>
        </div>
    </div>

    <!-- 作品3详情弹窗 -->
    <div class="work-modal" id="modal3">
        <div class="modal-content">
            <div class="modal-close" onclick="closeModal()">×</div>
            <div class="modal-bg">
                <h3 class="modal-title">逝者无情，人间有情</h3>
                <span class="modal-sub">读《逝川》有感 | 杨筱 时间之外的梅花坞</span>
                <p class="modal-text">人只能守着逝川的一段，守住的就活下去、老下去，守不住的就成为它岸边的坟冢听它的水声，依然望着它。本文是笔者两年前的一篇读书札记，今日整理后发出，以作茶余饭后之消遣。</p>
                <p class="modal-text">极北之地，藏在世俗之外的一个诗意的村庄里，流传着一个美丽的传说：捕到泪鱼的人家将会平安、无灾。这个朴素愿望的背后，不仅是人们对幸福安稳生活的追求，更是人们深埋于心底的对平淡生活的热爱。小说《逝川》中，以浙川流过的阿甲村为故事背景，以吉喜为主人公，在讲述某一年吉喜为胡刀妻子接生而错过捕泪鱼的同时，穿插了其成长经历与爱情故事。故事情节简单，并没有太多的曲折，却以一种淡淡的忧伤和潜藏在文字背后深深的宿命感，让人读之动容。</p>
                <p class="modal-text">小说中自然景物始终与人物情感、命运紧密相连：“逝川日日夜夜地流，吉喜一天天的苍老，两岸的树林却愈发蓊郁了”，以河流的永恒、树林的繁茂与吉喜的衰老形成对比，无一字写孤独，却处处透着孤独；“当晚秋的风在林间放肆地撕扯失去水分的树叶时，敏感的老渔妇吉喜就把捕捞泪鱼的工具准备好了”，用秋风扫叶的萧瑟，暗喻命运对吉喜的折磨，景与情浑然一体。</p>
                <p class="modal-text">初雪覆盖的阿甲村，“红松木栅栏上顶着的雪像是温柔的火焰一样瑰丽”，岸边的篝火“远远看去像是一只只金碗在闪闪发光”，洁白的雪、温暖的火与蓝色的泪鱼相互映衬，构成一幅纯净而忧伤的画面，既烘托出生命的美好，也暗示着其脆弱。而结尾处“一抹绯红的霞光出现在天际，使阿甲渔村沉浸在受孕般的和平之中”，则以霞光的绚烂驱散了苦难的阴霾，预示着希望与新生，让读者在感伤之余，感受到生命的力量。</p>
                <p class="modal-text">逝川，本是流过阿甲村的一条河流，却让人想到孔夫子的“逝者如斯夫，不舍昼夜”。河流奔腾不息，是生命流逝的象征，吉喜从发髻高绾的少女变为驼背的老渔妇，生命随逝川无可奈何地流逝，而逝川依旧日夜流淌，两岸树林越发蓊郁。这条河流不宽阔却平静，为渔村带来平安与欢乐，它极深的水漾起袅袅水雾，包容着人们的一切辛酸与悲伤。村民们不知其源头，亦不知其去向，它汩汩流淌、生生不息，这便是最真切的生命觉悟：川水是永恒的，生命是短暂的，流逝的水里，有人们逝去的岁月，有人们心底的悲喜。</p>
                <p class="modal-text">而小说并未止步于生命逝去的感伤，吉喜因帮助胡刀妻子接生错过捕泪鱼，满心失望时，却发现水盆中游着十几条蓝幽幽的泪鱼——这是村人对她的回馈。吉喜七十八岁的一生，勤劳能干，为村人带来无数温暖与美好，而当她悲伤时，村人也以善良和爱意回应。她一生未成为胡会的妻子，却得到了全村人的爱，这种生命与生命之间流淌的温情，超越了生命短暂之悲，溶入亘古不息的川水，上善若水，悠远绵长。</p>
                <p class="modal-text">泪鱼“身体呈扁圆形，红色的鳍，蓝色的鳞片”，每年第一场雪后出现，到来时逝川便发出呜呜的声响，仿佛世间最感伤的曲调汇集于此。泪鱼是苦难的生命象征，它们一路承受命运的跌宕，却始终坚定前行，因悲凉而哭泣，因关爱而心安，在苦难中消化痛苦，也在苦难中获得温爱与成长。而泪鱼亦是吉喜一生命运的隐喻，更是所有人生命的象征：生命的河流中，有眼泪也有温情，有不幸也有美好，悲喜交互，才是真实的人生。</p>
                <p class="modal-text">小说中刻意提及当地女子的生育能力，核心情节是迎接生命的到来，泪鱼于雪夜来临，生命亦于雪夜降生，初雪便成为纯洁、希望与新生的隐喻。洁白的白雪让阿甲村人的心灵洁净，雪夜里胡刀的妻子生下一儿一女，“那生动的啼哭声就像果实的甜香气一样四处弥漫”，迟子建说：“每一个生命的诞生都是上帝赐予人间的禁果，它饱含着痛苦和欢乐，甘甜而又辛酸。”新的生命，是村落对未来最美的希望。</p>
                <p class="modal-text">吉喜，名含“吉祥欢喜”，作者对其饱含喜爱与期待，可她的一生却满是苦难。她美丽能干、爱憎分明，却因爱人胡会的虚荣，错失爱情，孤独一生。可她始终以爱待人，中年后为渔村妇女接生，延续生命，这份母性的情怀与奉献的精神，让她成为阿甲村的“神灵”。她的一生充满矛盾：赞美与诅咒、美丽与忧伤、遗憾与幸福，而这一切的总和，便是真实的人生。这份人生智慧的了悟，让我们的心灵更加懂得包容与宁和。</p>
                <p class="modal-text">迟子建对大自然和生命的挚爱，让她的小说展现出自然、温暖、纯净的底色。阿甲渔村的一切生灵：逝川、泪鱼、吉喜、渔人、初雪、霞光……构成了一个令我们无限感怀向往的精神圣境。让那纯白的雪落进心里，用爱抚慰那一条蓝色泣珠的泪鱼，这便是《逝川》留给我们最珍贵的礼物。</p>
            </div>
        </div>
    </div>

    <!-- 作品4详情弹窗 -->
    <div class="work-modal" id="modal4">
        <div class="modal-content">
            <div class="modal-close" onclick="closeModal()">×</div>
            <div class="modal-bg">
                <h3 class="modal-title">重山</h3>
                <span class="modal-sub">神不在殿中，而在回头处 | 原创 杨筱</span>
                <p class="modal-text">风声是第一个征兆。它穿过山坳，像一声悠长而破碎的叹息，缠绕在他早已疲惫的脚踝上。他抬起头，前方那座废弃的土地庙，在暮色里只剩下一个歪斜的轮廓。庙门早已朽烂，虚掩着一道深不见底的黑暗。他伸手去推，门轴却没有发出预想中的呻吟。院里的草木没了人修剪，疯长的野蒿没过脚踝，把原先的石板路盖得严严实实；正中央的大殿最是萧索，屋顶瓦片碎了一地，发黑的梁木上结满蛛网。几缕残光从屋顶的破洞渗下，照亮了空气中悬浮的、缓慢舞动的尘埃。气味很复杂，是陈年霉味、冷冽土腥，全然没有了当年的香火气。</p>
                <p class="modal-text">目光适应了昏暗后，他看见角落那尊神像。彩漆剥落，面容模糊，只有那双石雕的眼睛，空洞地望着远山之外的世界，三个蒲团散在佛像前，布面烂得露出里面的枯草，还沾着深色的霉斑。他好像听到了钟声，紧接着却是一阵阵晕眩，血液顿时涌入他那疲惫的脑中，身体失去了平衡，他闭上了双眼。四周再次归于死寂。庙外，夜色四合，山峦沉默。只有风，依旧不知疲倦地，吹过重重山隘。</p>
                <p class="modal-text">打开窗后，凌冽的风不请自来，这年轻人却任由这刀剑造访他的脸颊，倔强地保持着最后一丝清醒。尽管如此，倦意仍如潮水般漫上，将他推向一个熟悉又陌生的地方——低矮的楼房，蜿蜒的小路，是他记忆里童年的轮廓。他向前走，突然来到一所院墙外，墙内人声鼎沸、纸钱翩翩如蝶。他惶恐着，走向那扇陈旧的破门，可他无论如何都推不开那扇摇摇欲坠的门。</p>
                <p class="modal-text">他挣扎着醒来，四肢沉重。他又一次坐在了深黑的夜里，无论怎么调节，这月光似乎总是让这年轻人的眼睛生疼。这一连几日的怪梦如冷清小路上的一阵风一般，起落无痕，却又那么真实。他烦躁着，今夜注定无眠。辗转无果后，他选择坐起，他知道，他的思绪在凌晨三点的深巷之中，来来回回，一遍又一遍地找寻着一个能够让他安然入睡的理由。</p>
                <p class="modal-text">熹微的晨光照耀下，一座城市正在逐渐苏醒着。城市的东面，是一重一重起伏的山峦。云雾缭绕间，为大山蒙上了一层神秘的面纱。可是城里人却仿佛什么都知道似的，从不好奇那一片大山后方会是什么，只是留在城市里日夜不息。如果大山也会感慨，它也许会这样说道：“你们难道不希望探索吗？山的背后或许是海呢？”可惜，山的背后不是海，只是一个再平常不过的村子。村子的后山上有一座古寺，叫作“寒钟寺”，传说自建成至今，已有三百年历史。禅房简朴，草木幽深；梵音袅袅，幽香阵阵，寒钟寺的氛围，藏着最纯粹的安宁。</p>
                <p class="modal-text">每到黄昏之时，寺里的僧人便会敲响那口古钟，钟声厚重而绵长，穿过层层叠叠的山峦，飘向远方。那钟声像是有魔力一般，能抚平人心底的褶皱，让浮躁的灵魂找到归处。他曾在无数个黄昏，坐在寒钟寺的台阶上，听着钟声，看着夕阳一点点沉入山坳，心中的迷茫与痛苦，也仿佛随钟声消散在风中。</p>
                <p class="modal-text">可他终究还是离开了。城市的霓虹，生活的压力，像一张无形的网，将他牢牢困住。他以为逃离了大山，就能找到想要的生活，却不知，真正的归宿，从来不在远方，而在回头处。当他再次踏上这片土地，站在废弃的土地庙前，才终于明白：神不在金碧辉煌的殿宇中，不在香火鼎盛的庙宇里，而在每一个回头的瞬间，在每一次对过往的回望里，在那些被我们遗忘的、藏着温暖与爱的时光中。</p>
                <p class="modal-text">风依旧吹着，他缓缓蹲下身，抚摸着脚下干裂的土地，像是触摸着岁月的纹路。远处，寒钟寺的钟声隐约传来，这一次，他没有再逃避，而是迎着风声，朝着钟声传来的方向，一步步走去。重山之后，不是海，是归途；回头之处，不是过往，是心安。</p>
            </div>
        </div>
    </div>

    <script>
        // 获取当前激活页面的页码
        function getCurrentPage() {
            const activePage = document.querySelector('.page.active');
            return parseInt(activePage.id.replace('page', ''));
        }

        // 分步页面切换核心函数
        function switchPage(currentPageNum, targetPageNum) {
            const currentPage = document.getElementById(`page${currentPageNum}`);
            currentPage.classList.remove('active');
            
            const targetPage = document.getElementById(`page${targetPageNum}`);
            targetPage.classList.add('active');
            
            window.scrollTo(0, 0);
        }

        // 下一页
        function goNextPage() {
            const current = getCurrentPage();
            const next = current === 5 ? 1 : current + 1;
            switchPage(current, next);
        }

        // 上一页（保留函数，顶部导航可用）
        function goPrevPage() {
            const current = getCurrentPage();
            const prev = current === 1 ? 5 : current - 1;
            switchPage(current, prev);
        }

        // 打开作品弹窗
        function openModal(num) {
            const modal = document.getElementById(`modal${num}`);
            modal.classList.add('active');
            // 禁止页面滚动
            document.body.style.overflow = 'hidden';
        }

        // 关闭作品弹窗
        function closeModal() {
            const modals = document.querySelectorAll('.work-modal');
            modals.forEach(modal => {
                modal.classList.remove('active');
            });
            // 恢复页面滚动
            document.body.style.overflow = 'auto';
        }

        // 支持键盘方向键切换（可选保留）
        document.addEventListener('keydown', (e) => {
            if (e.key === 'ArrowRight' || e.key === 'ArrowDown') {
                goNextPage();
            } else if (e.key === 'ArrowLeft' || e.key === 'ArrowUp') {
                goPrevPage();
            } else if (e.key === 'Escape') {
                closeModal(); // 按ESC关闭弹窗
            }
        });

        // 点击弹窗外部关闭弹窗
        document.querySelectorAll('.work-modal').forEach(modal => {
            modal.addEventListener('click', (e) => {
                if (e.target === modal) {
                    closeModal();
                }
            });
        });
    </script>
</body>
</html>
