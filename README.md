<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>彩讯股份 · 2026 社招 JD 生成工具</title>
<style>
* { box-sizing: border-box; margin: 0; padding: 0; }

:root {
  --bg: #f5f4f1;
  --surface: #ffffff;
  --surface2: #f0efe9;
  --border: #e2e0d8;
  --border2: #ccc9be;
  --text: #1a1a16;
  --text2: #5a5850;
  --text3: #999488;
  --green: #1a7a4a;
  --green-bg: #e8f5ee;
  --green-bd: #aad4bc;
  --blue: #1558a0;
  --blue-bg: #e4eff9;
  --blue-bd: #a8c8f0;
  --amber: #7a4a08;
  --amber-bg: #faecd8;
  --amber-bd: #eebb60;
  --purple: #3c2e8a;
  --purple-bg: #eeedfe;
  --purple-bd: #afa9ec;
  --red: #a32d2d;
  --accent: #d4380d;
  --accent-bg: #fff1ec;
  --accent-bd: #fbb89a;
  --r: 8px;
  --r-lg: 12px;
}

body {
  font-family: -apple-system, "PingFang SC", "Microsoft YaHei", "Helvetica Neue", Arial, sans-serif;
  background: var(--bg);
  color: var(--text);
  font-size: 14px;
  line-height: 1.6;
  height: 100vh;
  overflow: hidden;
  display: flex;
  flex-direction: column;
}

/* ── Header ── */
.header {
  background: #111110;
  padding: 0 28px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 54px;
  flex-shrink: 0;
  border-bottom: 1px solid #2a2a28;
}
.hd-left { display: flex; align-items: center; gap: 14px; }
.hd-logo {
  width: 30px; height: 30px; border-radius: 5px;
  background: linear-gradient(135deg, #1a7a4a 0%, #0f5235 100%);
  display: flex; align-items: center; justify-content: center;
  font-size: 12px; font-weight: 800; color: #fff; letter-spacing: -0.5px;
}
.hd-name { font-size: 14px; font-weight: 600; color: #f0ede6; }
.hd-divider { width: 1px; height: 18px; background: #333; }
.hd-sub { font-size: 12px; color: #666; }
.hd-right { display: flex; align-items: center; gap: 10px; }
.hd-badge {
  font-size: 10px; letter-spacing: 0.08em; padding: 3px 10px;
  border-radius: 100px; font-weight: 600;
  background: rgba(212,56,13,0.15); color: #e8805a;
  border: 1px solid rgba(212,56,13,0.3);
}
.hd-badge-g {
  background: rgba(26,122,74,0.15); color: #52c88c;
  border: 1px solid rgba(26,122,74,0.3);
}

/* ── Layout ── */
.main {
  display: grid;
  grid-template-columns: 380px 1fr;
  flex: 1;
  overflow: hidden;
}

/* ── Form Panel ── */
.panel-form {
  background: var(--surface);
  border-right: 1px solid var(--border);
  display: flex;
  flex-direction: column;
  overflow: hidden;
}
.form-scroll { flex: 1; overflow-y: auto; padding: 18px 20px 6px; }
.form-scroll::-webkit-scrollbar { width: 4px; }
.form-scroll::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 2px; }

.sec-head {
  font-size: 10px; font-weight: 700; letter-spacing: 0.12em; text-transform: uppercase;
  color: var(--text3); padding: 14px 0 8px;
  border-top: 1px solid var(--border); margin-top: 4px;
  display: flex; align-items: center; gap: 8px;
}
.sec-head:first-child { border-top: none; padding-top: 2px; margin-top: 0; }

.lk {
  font-size: 9px; padding: 1px 7px; border-radius: 100px;
  font-weight: 600; letter-spacing: 0.05em; text-transform: none;
}
.lk-e { background: var(--green-bg); color: var(--green); border: 1px solid var(--green-bd); }
.lk-l { background: var(--surface2); color: var(--text3); border: 1px solid var(--border); }

.fr { margin-bottom: 11px; }
.fl {
  font-size: 11px; color: var(--text2); margin-bottom: 4px;
  display: flex; align-items: center; gap: 6px;
}

input[type=text], textarea, select {
  width: 100%; font-family: inherit; font-size: 13px;
  padding: 7px 10px; border: 1px solid var(--border);
  border-radius: var(--r); background: var(--surface); color: var(--text);
  outline: none; transition: border-color 0.15s;
}
input[type=text]:focus, textarea:focus, select:focus { border-color: #1558a0; box-shadow: 0 0 0 2px rgba(21,88,160,0.08); }
textarea { resize: vertical; line-height: 1.7; }

.row2 { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; }

/* Location toggles */
.loc-wrap { display: flex; flex-wrap: wrap; gap: 6px; margin-top: 3px; }
.loc-btn {
  font-size: 12px; padding: 5px 13px; border-radius: 100px; cursor: pointer;
  border: 1px solid var(--border); background: var(--surface); color: var(--text2);
  transition: all 0.15s; user-select: none;
}
.loc-btn.on {
  background: var(--blue-bg); color: var(--blue);
  border-color: var(--blue-bd); font-weight: 500;
}

/* Tag input */
.tag-row { display: flex; gap: 6px; margin-bottom: 5px; }
.tag-row input { flex: 1; }
.btn-add {
  flex-shrink: 0; width: 34px; font-size: 18px; font-weight: 300;
  border: 1px solid var(--border); border-radius: var(--r);
  background: var(--surface); color: var(--text2); cursor: pointer;
  transition: background 0.12s; display: flex; align-items: center; justify-content: center;
}
.btn-add:hover { background: var(--surface2); }
.tags-wrap { display: flex; flex-wrap: wrap; gap: 5px; min-height: 22px; }
.tag-pill {
  font-size: 11px; padding: 3px 9px; border-radius: 100px;
  background: var(--surface2); border: 1px solid var(--border);
  color: var(--text2); display: flex; align-items: center; gap: 4px;
}
.tag-rm { cursor: pointer; color: var(--text3); font-size: 13px; line-height: 1; }
.tag-rm:hover { color: var(--red); }

/* Lock box */
.lock-box {
  background: var(--surface2); border: 1px dashed var(--border2);
  border-radius: var(--r); padding: 10px 12px;
  font-size: 11px; color: var(--text3); line-height: 1.7;
}

/* Preset */
.preset-row { display: flex; gap: 7px; }
.preset-row select { flex: 1; }
.btn-preset {
  flex-shrink: 0; padding: 7px 12px; font-size: 12px; font-weight: 600;
  border: 1px solid var(--blue-bd); border-radius: var(--r);
  background: var(--blue-bg); color: var(--blue); cursor: pointer;
  white-space: nowrap; transition: background 0.12s;
}
.btn-preset:hover { background: #d4e8f5; }

/* Gen btn */
.gen-wrap { padding: 12px 20px 16px; border-top: 1px solid var(--border); flex-shrink: 0; background: var(--surface); }
.btn-gen {
  width: 100%; padding: 11px; font-size: 14px; font-weight: 700;
  border: none; border-radius: var(--r);
  background: #111110; color: #f0ede6; cursor: pointer;
  letter-spacing: 0.04em; transition: background 0.15s;
}
.btn-gen:hover { background: #2a2a28; }

/* ── Preview Panel ── */
.panel-preview {
  overflow-y: auto;
  background: var(--bg);
  padding: 22px 28px;
}
.panel-preview::-webkit-scrollbar { width: 5px; }
.panel-preview::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 2px; }

.prev-toolbar {
  display: flex; align-items: center; justify-content: space-between;
  margin-bottom: 16px;
}
.prev-label {
  font-size: 10px; font-weight: 700; letter-spacing: 0.14em;
  text-transform: uppercase; color: var(--text3);
}
.tbtn-row { display: flex; gap: 7px; align-items: center; }
.btn-act {
  font-size: 12px; font-weight: 500; padding: 6px 14px;
  border: 1px solid var(--border2); border-radius: var(--r);
  background: var(--surface); color: var(--text2); cursor: pointer; transition: all 0.12s;
}
.btn-act:hover { background: var(--surface2); }
.btn-act.pri { background: #111110; color: #f0ede6; border-color: #111110; }
.btn-act.pri:hover { background: #2a2a28; }
.copy-ok { font-size: 11px; color: var(--green); display: none; }

/* ── JD Output ── */
.jd-wrap {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: var(--r-lg); overflow: hidden;
}

/* Hero */
.jd-hero { background: #111110; padding: 26px 28px 22px; }
.jd-eyebrow {
  display: flex; align-items: center; gap: 8px; margin-bottom: 14px; flex-wrap: wrap;
}
.ey-chip {
  font-size: 9px; letter-spacing: 0.12em; text-transform: uppercase; font-weight: 700;
  padding: 3px 10px; border-radius: 2px;
  font-family: "SF Mono", "Consolas", monospace;
}
.ey-green {
  background: rgba(26,122,74,0.15); color: #52c88c;
  border: 1px solid rgba(82,200,140,0.25);
}
.ey-red {
  background: rgba(212,56,13,0.12); color: #e8805a;
  border: 1px solid rgba(212,56,13,0.25);
}
.ey-gray {
  background: rgba(255,255,255,0.06); color: #888;
  border: 1px solid rgba(255,255,255,0.1);
}
.jd-title { font-size: 24px; font-weight: 800; color: #f0ede6; margin-bottom: 14px; line-height: 1.2; letter-spacing: -0.01em; }
.jd-meta-row { display: flex; flex-wrap: wrap; gap: 16px; }
.jd-mi { display: flex; align-items: center; gap: 6px; font-size: 12px; }
.jd-dot { width: 5px; height: 5px; border-radius: 50%; flex-shrink: 0; }
.jd-dot-g { background: #52c88c; }
.jd-dot-p { background: #a08cf0; }
.jd-dot-o { background: #e8805a; }
.jd-sal { color: #52c88c; font-family: "SF Mono", monospace; font-size: 11px; font-weight: 600; }
.jd-loc { color: #c0b8f0; font-size: 12px; }
.jd-type { color: #e8805a; font-size: 11px; font-family: "SF Mono", monospace; }

/* Body */
.jd-body { padding: 20px 28px; }
.jd-sec { margin-bottom: 18px; }
.jd-sec:last-child { margin-bottom: 0; }

.jd-sh {
  font-size: 10px; font-weight: 700; letter-spacing: 0.12em; text-transform: uppercase;
  color: var(--text3); padding-bottom: 8px; margin-bottom: 10px;
  border-bottom: 1px solid var(--border);
}

/* Locked */
.jd-locked {
  background: var(--surface2); border-left: 3px solid var(--border2);
  padding: 12px 14px; border-radius: 0 var(--r) var(--r) 0;
}
.jd-locked-lbl {
  font-size: 9px; letter-spacing: 0.12em; text-transform: uppercase;
  color: var(--text3); margin-bottom: 7px;
  font-family: "SF Mono", monospace; font-weight: 700;
}
.jd-locked-text { font-size: 12px; color: var(--text2); line-height: 1.85; }

/* Tags */
.jd-tags { display: flex; flex-wrap: wrap; gap: 6px; }
.jd-tag {
  font-size: 11px; padding: 3px 10px; border-radius: 100px;
  background: var(--surface2); border: 1px solid var(--border); color: var(--text2);
}
.jd-tag-b { background: var(--blue-bg); color: var(--blue); border-color: var(--blue-bd); }
.jd-tag-g { background: var(--green-bg); color: var(--green); border-color: var(--green-bd); }
.jd-tag-a { background: var(--amber-bg); color: var(--amber); border-color: var(--amber-bd); }

/* List */
.jd-ul { list-style: none; display: flex; flex-direction: column; gap: 6px; }
.jd-ul li { font-size: 13px; color: var(--text2); padding-left: 14px; position: relative; line-height: 1.7; }
.jd-ul li::before { content: "›"; position: absolute; left: 0; color: var(--green); font-weight: 700; }
.jd-ul li strong { color: var(--text); font-weight: 600; }

/* Address block */
.jd-addr-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 8px; }
.jd-addr-card {
  background: var(--surface2); border: 1px solid var(--border);
  border-radius: var(--r); padding: 10px 12px;
}
.jd-addr-city { font-size: 11px; font-weight: 700; color: var(--text); margin-bottom: 3px; }
.jd-addr-detail { font-size: 11px; color: var(--text2); line-height: 1.6; }

/* Priority */
.jd-priority {
  background: var(--amber-bg); border: 1px solid var(--amber-bd);
  border-radius: var(--r); padding: 12px 14px;
}
.jd-pri-lbl { font-size: 10px; font-weight: 700; color: var(--amber); margin-bottom: 8px; letter-spacing: 0.06em; }

/* Footer */
.jd-footer {
  border-top: 1px solid var(--border); padding: 12px 28px;
  display: flex; align-items: center; justify-content: space-between;
  background: var(--surface2);
}
.jd-footer-l { font-size: 11px; color: var(--text3); line-height: 1.6; }
.jd-footer-l strong { color: var(--text2); font-weight: 600; }
.jd-footer-r { display: flex; gap: 6px; align-items: center; }
.stk-chip {
  font-family: "SF Mono", monospace; font-size: 10px;
  padding: 3px 8px; border-radius: 3px;
  border: 1px solid var(--border); color: var(--green); background: var(--green-bg);
}

/* empty */
.empty {
  text-align: center; padding: 90px 20px; color: var(--text3); font-size: 13px; line-height: 2.2;
}
</style>
</head>
<body>

<!-- Header -->
<div class="header">
  <div class="hd-left">
    <div class="hd-logo">CX</div>
    <div class="hd-name">彩讯股份</div>
    <div class="hd-divider"></div>
    <div class="hd-sub">社招 JD 生成工具</div>
  </div>
  <div class="hd-right">
    <span class="hd-badge">社会招聘</span>
    <span class="hd-badge-g">2026</span>
  </div>
</div>

<!-- Main -->
<div class="main">

  <!-- Form -->
  <div class="panel-form">
    <div class="form-scroll">

      <div class="sec-head">快速预设</div>
      <div class="fr">
        <div class="fl">选择岗位类型，自动填入默认内容</div>
        <div class="preset-row">
          <select id="preset-sel">
            <option value="">-- 选择预设岗位 --</option>
            <option value="agent">AI Agent 应用开发工程师</option>
            <option value="backend">后端开发工程师（Java/Go）</option>
            <option value="frontend">前端开发工程师</option>
            <option value="algo">算法工程师（NLP/CV）</option>
            <option value="pm">产品经理（AI 方向）</option>
            <option value="data">数据工程师</option>
          </select>
          <button class="btn-preset" onclick="applyPreset()">应用</button>
        </div>
      </div>

      <div class="sec-head">岗位信息 <span class="lk lk-e">可编辑</span></div>

      <div class="fr">
        <div class="fl">岗位名称</div>
        <input type="text" id="f-title" placeholder="如：高级后端工程师">
      </div>

      <div class="fr">
        <div class="fl">薪资范围（万/年）</div>
        <div class="row2">
          <input type="text" id="f-sal-min" placeholder="最低，如 25万">
          <input type="text" id="f-sal-max" placeholder="最高，如 45万">
        </div>
      </div>

      <div class="fr">
        <div class="fl">工作地点（多选，点击切换）</div>
        <div class="loc-wrap" id="loc-wrap">
          <span class="loc-btn" data-v="北京">北京</span>
          <span class="loc-btn" data-v="广州">广州</span>
          <span class="loc-btn" data-v="深圳">深圳</span>
          <span class="loc-btn" data-v="成都">成都</span>
          <span class="loc-btn" data-v="杭州">杭州</span>
        </div>
      </div>

      <div class="fr">
        <div class="fl">优先专业</div>
        <div class="tag-row">
          <input type="text" id="f-major" placeholder="输入专业名，回车添加">
          <button class="btn-add" onclick="addTag('major')">+</button>
        </div>
        <div class="tags-wrap" id="tags-major"></div>
      </div>

      <div class="fr">
        <div class="fl">关键词 / 技能标签</div>
        <div class="tag-row">
          <input type="text" id="f-kw" placeholder="如：RAG知识库，回车添加">
          <button class="btn-add" onclick="addTag('kw')">+</button>
        </div>
        <div class="tags-wrap" id="tags-kw"></div>
      </div>

      <div class="fr">
        <div class="fl">核心职责（每行一条）</div>
        <textarea id="f-duties" placeholder="每行写一条职责描述，换行分隔&#10;&#10;如：&#10;负责企业级 AI Agent 平台的架构设计与核心模块开发&#10;主导大模型能力在业务场景中的工程化落地" style="min-height:160px"></textarea>
      </div>

      <div class="fr">
        <div class="fl">任职要求（每行一条）</div>
        <textarea id="f-reqs" placeholder="每行写一条要求，换行分隔&#10;&#10;如：&#10;本科及以上学历，计算机、AI 等相关专业&#10;3年以上后端开发经验" style="min-height:120px"></textarea>
      </div>

      <div class="fr">
        <div class="fl">技术栈要求</div>
        <div class="tag-row">
          <input type="text" id="f-stack" placeholder="如：Python，回车添加">
          <button class="btn-add" onclick="addTag('stack')">+</button>
        </div>
        <div class="tags-wrap" id="tags-stack"></div>
      </div>

      <div class="fr">
        <div class="fl">优先条件</div>
        <div class="tag-row">
          <input type="text" id="f-bonus" placeholder="如：有大模型落地项目经验">
          <button class="btn-add" onclick="addTag('bonus')">+</button>
        </div>
        <div class="tags-wrap" id="tags-bonus"></div>
      </div>

      <div class="sec-head">锁定模板 <span class="lk lk-l">品牌标准，不可修改</span></div>
      <div class="lock-box">
        以下内容自动嵌入，无需填写：<br>
        公司简介 · 五大竞争壁垒 · 为什么选择彩讯 · 期权福利说明<br>
        <strong style="color:var(--text2)">办公地址</strong>随所选工作地点自动切换
      </div>

    </div>
    <div class="gen-wrap">
      <button class="btn-gen" onclick="generate()">生成 JD 预览 →</button>
    </div>
  </div>

  <!-- Preview -->
  <div class="panel-preview">
    <div class="prev-toolbar">
      <div class="prev-label">JD 预览</div>
      <div class="tbtn-row">
        <span class="copy-ok" id="copy-ok">✓ 已复制</span>
        <button class="btn-act" onclick="copyText()">复制纯文本</button>
        <button class="btn-act pri" onclick="exportWord()">导出 Word ↓</button>
      </div>
    </div>
    <div id="preview-area">
      <div class="empty">填写左侧信息后<br>点击「生成 JD 预览」</div>
    </div>
  </div>

</div>

<script>
// ── State ──
const S = { major:[], kw:[], stack:[], bonus:[] };

// ── Office Addresses ──
const OFFICES = {
  "北京": {
    name: "北京研发中心",
    addr: "北京市海淀区西三环中路10号 望海楼大厦",
    detail: "地铁10号线 长春桥站 B口步行5分钟"
  },
  "广州": {
    name: "广州总部 / 研发中心",
    addr: "广州市天河区珠江新城冼村路5号 凯华国际中心",
    detail: "地铁3号线 珠江新城站 D口步行8分钟"
  },
  "深圳": {
    name: "深圳研发中心",
    addr: "深圳市南山区科技园南区 深圳湾科技生态园10栋",
    detail: "地铁2号线 高新园站 A口步行7分钟"
  },
  "成都": {
    name: "成都研发中心",
    addr: "成都市高新区天府三街218号 矩形广场B座",
    detail: "地铁1号线 天府三街站 步行3分钟"
  },
  "杭州": {
    name: "杭州研发中心",
    addr: "杭州市滨江区网商路699号 阿里云谷园区5号楼",
    detail: "地铁4号线 江陵路站 步行10分钟"
  }
};

// ── Presets ──
const PRESETS = {
  agent: {
    title: "AI Agent 应用开发工程师",
    salMin: "25万", salMax: "45万",
    locs: ["北京","广州","深圳","成都","杭州"],
    major: ["计算机","人工智能","软件工程","控制科学","数学","物理"],
    kw: ["Prompt工程","多Agent协同","RAG知识库","MLOps","大模型微调"],
    duties: "主导亿级月活场景下生产级 AI Agent 全流程构建，覆盖 Harness 架构、Eval 体系、向量检索及可观测性体系搭建\n负责 AI Agent 与企业系统的集成落地，推动大模型能力在电信、金融等真实业务场景中系统化应用\n参与多 Agent 协作框架设计，探索 Test-Time Compute 等前沿方向的工程化路径",
    reqs: "本科及以上学历，计算机、人工智能等相关专业\n3年以上 AI 应用开发经验，有大模型工程落地项目优先\n熟悉主流 LLM 框架及 RAG、微调等技术",
    stack: ["Python","TypeScript","Go","LangChain","LlamaIndex","PyTorch","HuggingFace","LoRA微调","vLLM推理"],
    bonus: ["有千万级用户AI产品研发经验","大模型开源项目贡献","顶会论文（ACL/NeurIPS等）","Kaggle竞赛名次"]
  },
  backend: {
    title: "后端开发工程师（Java/Go）",
    salMin: "20万", salMax: "38万",
    locs: ["北京","广州","深圳"],
    major: ["计算机","软件工程","信息工程","通信工程"],
    kw: ["高并发","微服务","分布式","云原生","性能优化"],
    duties: "负责核心业务平台后端架构设计与开发，支撑亿级用户并发场景稳定运行\n参与 RichAICloud 平台后端服务开发，推动服务云原生化改造与性能优化\n主导系统技术方案评审，承担核心模块的设计与攻坚",
    reqs: "本科及以上学历，计算机相关专业\n3年以上 Java 或 Go 后端开发经验\n有亿级流量系统设计与优化经验者优先",
    stack: ["Java","Go","Spring Boot","gRPC","Kafka","Redis","MySQL","Kubernetes","Docker"],
    bonus: ["参与过大规模分布式系统建设","有信创/国产化适配经验","开源社区贡献"]
  },
  frontend: {
    title: "前端开发工程师",
    salMin: "18万", salMax: "32万",
    locs: ["北京","广州","深圳","杭州"],
    major: ["计算机","软件工程","数字媒体","信息管理"],
    kw: ["React","Vue","工程化","性能优化","可视化"],
    duties: "负责企业级 AI 产品前端研发，包括 AI BI、智能客服等智能体应用界面开发\n推动前端工程化体系建设，制定并落实前端规范与研发效能提升方案\n与产品、设计深度协作，探索适配大模型交互的新型前端 UX 范式",
    reqs: "本科及以上学历，计算机相关专业\n3年以上前端开发经验，熟练掌握 React 或 Vue3\n有数据可视化或复杂表单系统开发经验",
    stack: ["React","TypeScript","Vue3","Vite","ECharts","WebSocket","Node.js"],
    bonus: ["有低代码/可视化平台研发经验","参与过开源 UI 组件库","ToB产品前端经验"]
  },
  algo: {
    title: "算法工程师（NLP/CV）",
    salMin: "30万", salMax: "55万",
    locs: ["北京","深圳","杭州"],
    major: ["计算机","人工智能","数学","统计学","模式识别"],
    kw: ["大模型微调","RAG","向量检索","多模态","推理加速"],
    duties: "负责企业级大模型应用算法研究与工程落地，涵盖模型微调、推理优化及评测体系构建\n主导 AI 知识库、语音智能体等核心产品的算法模块设计与实现\n持续跟进前沿 LLM 研究成果，驱动 arXiv 到生产环境的快速落地闭环",
    reqs: "硕士及以上学历，人工智能、计算机相关专业\n3年以上 NLP/LLM 相关算法经验\n熟练掌握 PyTorch，有 LoRA、RLHF 等微调实战经验",
    stack: ["Python","PyTorch","HuggingFace Transformers","LoRA/QLoRA","vLLM","FAISS","LangChain","CUDA"],
    bonus: ["顶会论文（ACL/EMNLP/CVPR等）","Kaggle竞赛 Top%","大模型开源框架核心贡献者"]
  },
  pm: {
    title: "产品经理（AI 方向）",
    salMin: "22万", salMax: "40万",
    locs: ["北京","广州","深圳"],
    major: ["计算机","信息管理","工商管理","设计学"],
    kw: ["AI产品设计","用户研究","数据分析","ToB产品","Agent交互"],
    duties: "负责 AI 智能体产品（AI BI、智能客服、AI知识库等）的规划、需求分析与版本迭代\n深入理解电信、金融等行业客户业务痛点，主导产品需求挖掘与解决方案设计\n与算法、工程团队协同，推动大模型能力在业务场景中的系统化落地",
    reqs: "本科及以上学历，相关专业\n3年以上 ToB 产品设计经验，有 AI 产品从0到1经历优先\n具备基础的 Prompt 工程认知，能与算法团队有效沟通",
    stack: ["Axure/Figma","SQL基础","A/B测试","用户访谈","数据埋点分析"],
    bonus: ["有行业大客户产品交付经验","主导过AI产品商业化落地","懂技术的复合型PM"]
  },
  data: {
    title: "数据工程师",
    salMin: "18万", salMax: "35万",
    locs: ["北京","广州","成都"],
    major: ["计算机","统计学","数学","信息管理","软件工程"],
    kw: ["数据仓库","ETL","实时计算","数据治理","数据资产"],
    duties: "负责企业数据平台架构设计与建设，支撑数据智能业务板块稳定运行\n设计并实施数据模型、ETL 流程及数据质量管理体系\n参与 AI BI 产品数据层建设，赋能业务智能分析场景",
    reqs: "本科及以上学历，计算机相关专业\n3年以上大数据开发经验，熟练掌握 Spark 或 Flink\n有金融或电信行业数仓建设经验优先",
    stack: ["Spark","Flink","Hive","Kafka","ClickHouse","Airflow","Python","SQL"],
    bonus: ["主导过亿级规模数仓建设","有实时数据平台架构经验","数据治理体系落地经验"]
  }
};

function applyPreset() {
  const key = document.getElementById('preset-sel').value;
  if (!key) return;
  const p = PRESETS[key];
  document.getElementById('f-title').value = p.title;
  document.getElementById('f-sal-min').value = p.salMin;
  document.getElementById('f-sal-max').value = p.salMax;
  document.getElementById('f-duties').value = p.duties;
  document.getElementById('f-reqs').value = p.reqs || '';
  document.querySelectorAll('.loc-btn').forEach(b => {
    b.classList.toggle('on', p.locs.includes(b.dataset.v));
  });
  ['major','kw','stack','bonus'].forEach(t => { S[t] = [...p[t]]; renderTags(t); });
}

// ── Tags ──
function renderTags(type) {
  document.getElementById('tags-' + type).innerHTML = S[type].map(v =>
    `<span class="tag-pill">${v}<span class="tag-rm" onclick="removeTag('${type}','${encodeURIComponent(v)}')">×</span></span>`
  ).join('');
}
function addTag(type) {
  const input = document.getElementById('f-' + type);
  const v = input.value.trim();
  if (v && !S[type].includes(v)) { S[type].push(v); renderTags(type); }
  input.value = ''; input.focus();
}
function removeTag(type, enc) {
  S[type] = S[type].filter(x => x !== decodeURIComponent(enc));
  renderTags(type);
}
['major','kw','stack','bonus'].forEach(t => {
  document.getElementById('f-' + t).addEventListener('keydown', e => {
    if (e.key === 'Enter') { e.preventDefault(); addTag(t); }
  });
});
document.querySelectorAll('.loc-btn').forEach(b => b.addEventListener('click', () => b.classList.toggle('on')));

// ── Getters ──
function getV(id) { return document.getElementById(id).value.trim(); }
function getLocs() { return [...document.querySelectorAll('.loc-btn.on')].map(b => b.dataset.v); }
function getSalary() {
  const mn = getV('f-sal-min'), mx = getV('f-sal-max');
  if (!mn && !mx) return '薪资面议';
  if (!mx) return mn + '/年 + 期权激励';
  return mn + ' — ' + mx + '/年 + 期权激励';
}

// ── Generate ──
function generate() {
  const title = getV('f-title') || '（未填写岗位名称）';
  const salary = getSalary();
  const locs = getLocs();
  const duties = getV('f-duties').split('\n').filter(l => l.trim());
  const reqs = getV('f-reqs').split('\n').filter(l => l.trim());

  const addrCards = locs.map(city => {
    const o = OFFICES[city];
    if (!o) return '';
    return `<div class="jd-addr-card">
      <div class="jd-addr-city">${city} · ${o.name}</div>
      <div class="jd-addr-detail">${o.addr}</div>
      <div class="jd-addr-detail" style="color:var(--text3);margin-top:3px">${o.detail}</div>
    </div>`;
  }).join('');

  document.getElementById('preview-area').innerHTML = `
  <div class="jd-wrap">
    <div class="jd-hero">
      <div class="jd-eyebrow">
        <span class="ey-chip ey-green">彩讯股份 · 300634.SZ</span>
        <span class="ey-chip ey-red">社会招聘</span>
        <span class="ey-chip ey-gray">2026</span>
      </div>
      <div class="jd-title">${title}</div>
      <div class="jd-meta-row">
        <div class="jd-mi"><div class="jd-dot jd-dot-g"></div><span class="jd-sal">${salary}</span></div>
        <div class="jd-mi"><div class="jd-dot jd-dot-p"></div><span class="jd-loc">${locs.length ? locs.join(' / ') : '地点待定'}</span></div>
        <div class="jd-mi"><div class="jd-dot jd-dot-o"></div><span class="jd-type">社会招聘</span></div>
      </div>
    </div>

    <div class="jd-body">

      <div class="jd-sec">
        <div class="jd-sh">公司简介</div>
        <div class="jd-locked">
          <div class="jd-locked-lbl">标准模板 · 不可修改</div>
          <div class="jd-locked-text">彩讯科技股份有限公司（股票代码：300634.SZ）创立于2004年，国家高新技术企业、国家鼓励的重点软件企业，员工4000+人，北京、广州、深圳、杭州、成都五大研发中心，致力于成为 AI 时代的企业服务领导者。公司以 <strong>Rich AICloud</strong> 与 <strong>Rich AIBox</strong> 为核心，构建覆盖算力、平台与应用的全栈 AI 能力体系，主要客户包括中国移动、中国联通、南方电网、国家电网、中国银行、中国人寿、中国国际航空、南方航空等行业头部企业。</div>
        </div>
      </div>

      <div class="jd-sec">
        <div class="jd-sh">为什么选择彩讯</div>
        <div class="jd-locked">
          <div class="jd-locked-lbl">标准模板 · 不可修改</div>
          <ul class="jd-ul" style="margin-top:0">
            <li><strong>真实场景</strong> — 代码直接跑在亿级用户生产环境，服务中国移动、南方电网、中国银行等头部客户</li>
            <li><strong>GPU 自由</strong> — 自有 RichAICloud 算力池，LoRA 微调到 vLLM 推理全链路自己跑，不是调 API</li>
            <li><strong>成长驱动</strong> — 1v1 资深导师带教，快速成长通道，成长看交付记录不看工龄</li>
            <li><strong>前沿同步</strong> — 在研课题：多Agent协作涌现 / Test-Time Compute / 可信 AI 治理</li>
            <li><strong>长期回报</strong> — A 股期权激励 + 五城研发中心灵活选择 + 管理 / 专业双通道晋升</li>
          </ul>
        </div>
      </div>

      ${S.major.length ? `<div class="jd-sec"><div class="jd-sh">优先专业</div><div class="jd-tags">${S.major.map(t=>`<span class="jd-tag">${t}</span>`).join('')}</div></div>` : ''}

      ${S.kw.length ? `<div class="jd-sec"><div class="jd-sh">岗位关键词</div><div class="jd-tags">${S.kw.map(t=>`<span class="jd-tag jd-tag-b">${t}</span>`).join('')}</div></div>` : ''}

      ${duties.length ? `<div class="jd-sec"><div class="jd-sh">核心职责</div><ul class="jd-ul">${duties.map(d=>`<li>${d}</li>`).join('')}</ul></div>` : ''}

      ${reqs.length ? `<div class="jd-sec"><div class="jd-sh">任职要求</div><ul class="jd-ul">${reqs.map(r=>`<li>${r}</li>`).join('')}</ul></div>` : ''}

      ${S.stack.length ? `<div class="jd-sec"><div class="jd-sh">技术栈要求</div><div class="jd-tags">${S.stack.map(t=>`<span class="jd-tag jd-tag-g">${t}</span>`).join('')}</div></div>` : ''}

      ${S.bonus.length ? `
      <div class="jd-sec">
        <div class="jd-priority">
          <div class="jd-pri-lbl">★ 优先考虑</div>
          <div class="jd-tags">${S.bonus.map(t=>`<span class="jd-tag jd-tag-a">${t}</span>`).join('')}</div>
        </div>
      </div>` : ''}

      ${locs.length ? `
      <div class="jd-sec">
        <div class="jd-sh">工作地点 · 办公地址</div>
        <div class="jd-locked">
          <div class="jd-locked-lbl">根据所选地点自动生成 · 标准模板</div>
          <div class="jd-addr-grid" style="margin-top:8px">${addrCards}</div>
        </div>
      </div>` : ''}

    </div>

    <div class="jd-footer">
      <div class="jd-footer-l">
        <strong>彩讯科技股份有限公司</strong>  ·  社会招聘  ·  2026<br>
        <span style="font-size:10px">如有疑问请联系招聘团队</span>
      </div>
      <div class="jd-footer-r">
        <span class="stk-chip">300634.SZ</span>
      </div>
    </div>
  </div>`;
}

// ── Copy Text ──
function copyText() {
  const title = getV('f-title') || '未填写';
  const salary = getSalary();
  const locs = getLocs();
  const duties = getV('f-duties').split('\n').filter(l=>l.trim());
  const reqs = getV('f-reqs').split('\n').filter(l=>l.trim());

  const lines = [
    `【${title}】（社会招聘）`,
    `薪资：${salary}`,
    `地点：${locs.join(' / ') || '待定'}`,
    '',
    '【公司简介】',
    '彩讯科技股份有限公司（300634.SZ），创立于2004年，国家高新技术企业，员工4000+，五大研发中心。以 Rich AICloud 与 Rich AIBox 为核心，构建全栈AI能力体系，服务中国移动、南方电网、中国银行等头部企业。',
    '',
    '【为什么选择彩讯】',
    '· 真实场景 — 代码直接跑在亿级用户生产环境，服务头部客户',
    '· GPU 自由 — 自有算力池，全链路自己跑，不调 API',
    '· 成长驱动 — 1v1资深导师带教，成长看交付记录',
    '· 前沿同步 — 在研：多Agent协作涌现 / Test-Time Compute / 可信AI治理',
    '· 长期回报 — A股期权激励 + 五城研发中心 + 双通道晋升',
    '',
  ];
  if (S.major.length) lines.push('【优先专业】', S.major.join('、'), '');
  if (S.kw.length) lines.push('【岗位关键词】', S.kw.join(' | '), '');
  if (duties.length) { lines.push('【核心职责】'); duties.forEach(d=>lines.push('· '+d)); lines.push(''); }
  if (reqs.length) { lines.push('【任职要求】'); reqs.forEach(r=>lines.push('· '+r)); lines.push(''); }
  if (S.stack.length) lines.push('【技术栈要求】', S.stack.join(' | '), '');
  if (S.bonus.length) lines.push('【优先考虑】', S.bonus.join(' · '), '');
  if (locs.length) {
    lines.push('【工作地点 · 办公地址】');
    locs.forEach(city => {
      const o = OFFICES[city];
      if (o) lines.push(`${city} · ${o.name}：${o.addr}（${o.detail}）`);
    });
  }

  navigator.clipboard.writeText(lines.join('\n')).then(() => {
    const el = document.getElementById('copy-ok');
    el.style.display = 'inline';
    setTimeout(() => el.style.display = 'none', 2200);
  });
}

// ── Export Word ──
function exportWord() {
  if (!window.docx) { alert('Word 导出库加载中，请稍后重试（需联网加载一次）'); return; }
  const { Document, Packer, Paragraph, TextRun, AlignmentType, LevelFormat, BorderStyle } = window.docx;

  const title = getV('f-title') || '岗位JD';
  const salary = getSalary();
  const locs = getLocs();
  const duties = getV('f-duties').split('\n').filter(l=>l.trim());
  const reqs = getV('f-reqs').split('\n').filter(l=>l.trim());

  const DARK='1A1A16', GREEN='1A7A4A', GRAY='5A5850', LGRAY='F0EFE9', BC='E2E0D8';

  const p = (text, opts={}) => new Paragraph({
    spacing: { after: opts.after||80 },
    children: [new TextRun({ text, font:'Arial', ...opts })]
  });

  const secHead = text => new Paragraph({
    border: { bottom:{ style:BorderStyle.SINGLE, size:4, color:BC, space:4 } },
    spacing: { before:240, after:120 },
    children: [new TextRun({ text, font:'Arial', bold:true, size:20, color:DARK, allCaps:true })]
  });

  const blt = text => new Paragraph({
    numbering: { reference:'blt', level:0 },
    spacing: { after:60 },
    children: [new TextRun({ text, font:'Arial', size:22, color:GRAY })]
  });

  const sp = () => new Paragraph({ children:[new TextRun('')], spacing:{after:80} });

  const tagLine = (arr, sep) => new Paragraph({
    spacing:{after:80},
    children:[new TextRun({ text:arr.join(sep||'  ·  '), font:'Arial', size:22, color:'1558A0' })]
  });

  const children = [
    new Paragraph({
      spacing:{after:80},
      children:[new TextRun({ text:title, font:'Arial', bold:true, size:48, color:DARK })]
    }),
    new Paragraph({
      spacing:{after:60},
      children:[
        new TextRun({ text:'薪资：', font:'Arial', size:22, color:GRAY }),
        new TextRun({ text:salary, font:'Arial', size:22, bold:true, color:GREEN }),
        new TextRun({ text:'    地点：', font:'Arial', size:22, color:GRAY }),
        new TextRun({ text:locs.join(' / ')||'待定', font:'Arial', size:22, bold:true, color:DARK }),
        new TextRun({ text:'    社会招聘', font:'Arial', size:22, color:'D4380D' }),
      ]
    }),
    sp(),
    secHead('公司简介'),
    p('彩讯科技股份有限公司（300634.SZ）创立于2004年，国家高新技术企业，员工4000+人，五大研发中心。以 Rich AICloud 与 Rich AIBox 为核心，构建全栈 AI 能力体系，服务中国移动、南方电网、中国银行等行业头部企业。', {size:22, color:GRAY}),
    sp(),
    secHead('为什么选择彩讯'),
    blt('真实场景 — 代码直接跑在亿级用户生产环境，服务头部客户'),
    blt('GPU 自由 — 自有 RichAICloud 算力池，全链路自己跑，不是调 API'),
    blt('成长驱动 — 1v1 资深导师带教，成长看交付记录不看工龄'),
    blt('前沿同步 — 在研课题：多Agent协作涌现 / Test-Time Compute / 可信AI治理'),
    blt('长期回报 — A股期权激励 + 五城研发中心灵活选择 + 管理/专业双通道晋升'),
    sp(),
  ];

  if (S.major.length) { children.push(secHead('优先专业'), tagLine(S.major,'  ·  '), sp()); }
  if (S.kw.length) { children.push(secHead('岗位关键词'), tagLine(S.kw,'  |  '), sp()); }
  if (duties.length) { children.push(secHead('核心职责')); duties.forEach(d=>children.push(blt(d))); children.push(sp()); }
  if (reqs.length) { children.push(secHead('任职要求')); reqs.forEach(r=>children.push(blt(r))); children.push(sp()); }
  if (S.stack.length) { children.push(secHead('技术栈要求'), tagLine(S.stack,'  |  '), sp()); }
  if (S.bonus.length) { children.push(secHead('优先考虑'), tagLine(S.bonus,'  ·  '), sp()); }

  if (locs.length) {
    children.push(secHead('工作地点 · 办公地址'));
    locs.forEach(city => {
      const o = OFFICES[city];
      if (!o) return;
      children.push(new Paragraph({
        spacing:{after:40},
        children:[new TextRun({text:`${city}  ·  ${o.name}`, font:'Arial', bold:true, size:22, color:DARK})]
      }));
      children.push(new Paragraph({
        spacing:{after:20},
        children:[new TextRun({text:o.addr, font:'Arial', size:20, color:GRAY})]
      }));
      children.push(new Paragraph({
        spacing:{after:100},
        children:[new TextRun({text:o.detail, font:'Arial', size:18, color:'999488'})]
      }));
    });
    children.push(sp());
  }

  children.push(new Paragraph({
    border:{top:{style:BorderStyle.SINGLE, size:4, color:BC, space:4}},
    spacing:{before:200},
    children:[new TextRun({text:'彩讯科技股份有限公司  ·  300634.SZ  ·  社会招聘  ·  2026', font:'Arial', size:18, color:'999488'})]
  }));

  const doc = new Document({
    numbering:{config:[{reference:'blt',levels:[{level:0,format:LevelFormat.BULLET,text:'·',alignment:AlignmentType.LEFT,style:{paragraph:{indent:{left:440,hanging:220}}}}]}]},
    styles:{default:{document:{run:{font:'Arial',size:22}}}},
    sections:[{
      properties:{page:{size:{width:11906,height:16838},margin:{top:1440,right:1440,bottom:1440,left:1440}}},
      children
    }]
  });

  Packer.toBlob(doc).then(blob => {
    const a = document.createElement('a');
    a.href = URL.createObjectURL(blob);
    a.download = `彩讯社招JD_${title}_${new Date().toLocaleDateString('zh-CN').replace(/\//g,'-')}.docx`;
    a.click();
  });
}
</script>

<script>
(function(){
  var s = document.createElement('script');
  s.src = 'https://unpkg.com/docx@8.5.0/build/index.umd.min.js';
  document.head.appendChild(s);
})();
</script>
</body>
</html>
