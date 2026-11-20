# 开源项目发布与敏感凭据防护 (Release Safety & Secret Protection)

本文档定义开源项目在涉及版本发布、外部凭证与 CI/CD 流程时的安全标准。

---

## 1. 凭据泄露防护 (Zero Secret Exposure)

在开源项目中，任何凭据泄露（即使在几秒后撤回）都会被自动化网络爬虫捕获：
1. **预提交检查**：在执行 `git add` 或准备对外提交时，必须确认以下文件不被追踪：
   - `.env`, `.env.local`, `.env.*`
   - `id_rsa`, `*.pem`, `*.key`
   - 包含硬编码 API 密钥、Access Token、Database Password 的配置文件
2. **Gitignore 规范**：若发现项目中缺少对敏感文件的忽略，应主动在 `.gitignore` 中补充规则。

---

## 2. 生产发版核验流程 (Release Checklist)

当维护者授权执行发版时，Agent 需按照以下核验清单快速检查：
1. **工作区状态**：工作树干净，无未提交的脏改动。
2. **测试状态**：全量单元测试与构建无报错通过。
3. **版本号一致性**：`package.json` / `Cargo.toml` / `pyproject.toml` 中的版本号与当前发版目标一致。
4. **变更日志 (CHANGELOG)**：相关变动已简要汇总。
