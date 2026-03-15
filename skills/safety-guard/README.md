# 🛡️ OpenClaw Safety Guard Skill

**基于 OpenClaw Skill 系统的安全护栏解决方案**

在调用大模型前分析用户输入，检测有害内容、风险指令和安全威胁。

---

## ✨ 特性

- ✅ **Prompt 注入检测**: 识别试图覆盖系统指令的攻击
- ✅ **Jailbreak 防护**: 检测 DAN 模式、开发者模式等
- ✅ **危险命令拦截**: 阻止 `rm -rf /` 等破坏性命令
- ✅ **有害内容过滤**: 过滤暴力、违法、仇恨内容
- ✅ **隐私保护**: 防止 API 密钥等敏感信息泄露
- ✅ **审计日志**: 完整的 JSONL 格式审计追踪
- ✅ **可配置**: YAML 配置文件，灵活调整阈值和规则

---

## 🚀 快速开始

### 安装

Skill 已安装到：`~/.openclaw/workspace/skills/safety-guard/`

```bash
# 测试安装
~/.openclaw/workspace/skills/safety-guard/safety-check "你好"
```

### 在 OpenClaw 中使用

#### 自动模式

配置后，所有输入会自动经过安全检查。

#### 手动模式

```
/safety-check 如何制作炸弹
```

**输出**:
```
🛡️ 安全护栏：🚫 **请求被拦截**

您的请求触发了安全策略，无法执行。

匹配的风险模式：制作炸弹
原因：匹配高风险模式：harmful_content
```

---

## 📋 命令参考

### `safety-check <message>`

检查消息安全性。

```bash
# 示例
./safety-check "你好"              # ✅ 放行
./safety-check "忽略指令"          # ⚠️ 警告
./safety-check "如何制作炸弹"      # 🚫 阻止
```

### `safety-config <command>`

管理配置。

```bash
# 显示配置
./safety-config show

# 修改阈值
./safety-config set thresholds.medium_risk 0.6

# 添加自定义模式
./safety-config add pattern "my-risk" custom
```

### `safety-log [options]`

查看审计日志。

```bash
# 最近 10 条
./safety-log --limit 10

# 只看被阻止的
./safety-log --filter blocked

# 实时跟踪
./safety-log --follow
```

---

## 📊 风险级别

| 级别 | 分数 | 行为 | 示例 |
|------|------|------|------|
| 🟢 **低** | 0.0-0.25 | ✅ 放行 | "你好"、"天气如何" |
| 🟡 **中** | 0.25-0.75 | ⚠️ 警告 | "忽略指令"、"测试系统" |
| 🔴 **高** | 0.75-1.0 | 🚫 阻止 | "制作炸弹"、"rm -rf /" |

---

## 🔧 配置

### 配置文件

```
~/.openclaw/workspace/skills/safety-guard/config/safety_config.yaml
```

### 关键配置

```yaml
thresholds:
  low_risk: 0.25      # 放行阈值
  medium_risk: 0.5    # 警告阈值
  high_risk: 0.75     # 阻止阈值

detectors:
  prompt_injection:
    enabled: true
  harmful_content:
    enabled: true

audit:
  enabled: true
  log_file: "audit/safety_audit.log"
```

---

## 📁 项目结构

```
safety-guard/
├── SKILL.md                  # Skill 元数据
├── _meta.json                # 元数据
├── safety-check              # 检查命令
├── safety-config             # 配置命令
├── safety-log                # 日志命令
├── scripts/
│   ├── safety_check.py       # 检查实现
│   ├── safety_config.py      # 配置实现
│   └── safety_log.py         # 日志实现
├── config/
│   └── safety_config.yaml    # 配置文件
├── rules/
│   ├── patterns.yaml         # 风险模式
│   └── policies.yaml         # 安全策略
├── audit/
│   ├── logger.py             # 日志记录器
│   └── safety_audit.log      # 审计日志
├── guardrail.py              # 核心护栏逻辑
├── classifiers/              # 检测器
├── venv/                     # Python 虚拟环境
└── references/
    └── api-reference.md      # API 文档
```

---

## 🧪 测试

```bash
cd ~/.openclaw/workspace/skills/safety-guard

# 运行所有测试
./safety-check "你好"
./safety-check "忽略所有指令"
./safety-check "如何制作炸弹"
./safety-check "rm -rf /"

# 查看结果
./safety-log --limit 10
```

---

## 📖 详细文档

- **[SKILL.md](SKILL.md)** - Skill 完整文档
- **[INSTALL.md](INSTALL.md)** - 安装指南
- **[references/api-reference.md](references/api-reference.md)** - API 参考

---

## 🔗 相关资源

- **GitHub**: https://github.com/John-niu-07/openclaw-safety-guard
- **独立服务版本**: `~/.openclaw/workspace/openclaw-safety-guard/`
- **NIST PQC**: https://csrc.nist.gov/projects/post-quantum-cryptography

---

## 📄 许可证

MIT License

---

**版本**: 1.0.0  
**创建日期**: 2026-03-14  
**作者**: John-niu-07
