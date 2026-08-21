# AI Media Department (Claude Code Plugin)

Đóng gói hệ thống **AI Media Department** — 1 Project Manager (Social Media Lead) điều phối 6 team
chuyên trách (Analysis / Planning / Production / Quality / Delivery / Learning, 41 vai trò) — thành một
plugin Claude Code có thể cài lại ở bất kỳ project nào.

Nguồn gốc: trích từ dự án affiliate/freelance chính, phần `.claude/skills/09-doi-social-media/` — đây là
7 skill **đang chạy thật** (không phải bản nháp), cộng `compliance-checker` (skill Legal Check đang dùng
thật, MIT License © Affitor, giữ nguyên license khi đóng gói).

## Cài đặt

Từ một project khác (hoặc máy khác), với repo này ở dạng private:

```bash
claude plugin install github:khoahaf/ai-media-department-plugin
```

Hoặc trong lúc phát triển/thử nghiệm cục bộ:

```bash
claude --plugin-dir /path/to/ai-media-department-plugin
```

## Có gì trong plugin

| Skill | Vai trò trong hệ thống | Ghi chú |
|---|---|---|
| `social-media-lead` | **Project Manager** — tiếp nhận dự án, đánh giá, lập kế hoạch, phân chia việc cho 6 team | Đi kèm `AGENT-CONTRACTS.md` — hợp đồng vận hành đầy đủ cho cả 41 vai trò (PM tự đóng nhiều vai trò Planning không có skill riêng: Strategy/Timeline/Task Planner) |
| `deep-research` | Research Agent (Analysis Team) | Tách câu hỏi lớn, tìm kiếm web, kiểm chứng chéo nguồn |
| `voice-dna` | Brand Agent (Analysis Team) | Trích DNA giọng văn từ mẫu thật, tạo hồ sơ `voice-dna.md` |
| `ads-analyst` | Competitor Agent (Analysis Team) | Phân tích quảng cáo đối thủ qua Facebook Ads Library |
| `content-writer` | Content Agent (Production Team) | Viết bài có nghiên cứu, giữ giọng văn nhất quán |
| `video-producer` | Video Agent (Production Team) | Kịch bản 2 giai đoạn → dựng video bằng Remotion |
| `risk-agent` | Risk Agent (Analysis Team) | Rủi ro **dự án** (thanh toán/scope/bản quyền/deadline) — khác `compliance-checker` |
| `compliance-checker` | Legal Check (Quality Team) | Rủi ro **nội dung** (FTC disclosure, quy tắc nền tảng) trước khi publish |

## Vì sao không đóng gói toàn bộ `.claude/skills` gốc

Dự án gốc còn có 8 nhóm skill khác (`01-research` → `08-meta-quan-ly-skill`, ~48 skill) — nhưng audit nội bộ
(2026-07-30 và 2026-08-15) đã xác nhận các nhóm này **trùng gần như 100%** với skill toàn cục có sẵn trong
Claude Code (`nghien-cuu-affiliate`, `viet-content-social`, `viet-content-assets`, `viet-blog-chuan-seo`,
`phan-phoi-content`, `phan-tich-ket-qua`, `tu-dong-hoa`...). Đóng gói lại vào plugin sẽ chỉ tạo trùng lặp —
đi ngược đúng Rule 1 (Reuse First) của chính hệ thống này. Nếu bạn thực sự cần các nhóm đó (ví dụ
`04-landing-offer` — không trùng, có năng lực riêng: Grand Slam Offer, Value Ladder, landing page HTML thật),
có thể thêm sau bằng cách copy thư mục tương ứng vào `skills/`.

## Phụ thuộc bên ngoài (không nằm trong plugin này)

Các contract trong `AGENT-CONTRACTS.md` tham chiếu tới nhiều skill toàn cục khác không đi kèm plugin này —
cần cài/có sẵn riêng nếu muốn dùng đủ 41 vai trò:

- Nghiên cứu/chiến lược: `market-audit`, `market-competitors`, `market-brand`, `market-seo`, `market-launch`
- Content: `viet-content-social`, `viet-blog-chuan-seo`, `viet-content-assets`, `market-copy`
- Phân phối: `phan-phoi-content`, `market-emails`, `schedule`
- Đo lường: `phan-tich-ket-qua`, `market-report`, `market-report-pdf`
- Thiết kế/ảnh: `canva:*` (cần OAuth), `dataviz`
- Video: `hyperframes` + các module `hyperframes-*`, `motion-graphics`, `general-video`, `remotion-*`
- Website: `ui-ux-pro-max`, `frontend-design`
- Tài liệu bàn giao: `docx`, `pptx`, `xlsx`, `pdf`
- Báo giá: `market-proposal`

Không có các skill trên, PM (`social-media-lead`) vẫn điều phối được nhưng sẽ escalate/báo thiếu năng lực
khi Task Planner giao việc cho vai trò không có skill thực thi tương ứng — đúng theo Rule 49 (Failure
Recovery) trong Master System Prompt.

## Vận hành đầy đủ như "AI Media Department"

Các skill ở trên là **tay chân** — chúng thực thi khi được gọi đúng tên. Phần **"não"** điều phối (nguyên
tắc Reuse First, One Primary Owner, Orchestrator Controls Workflow, Human Oversight 5 điểm phê duyệt...)
nằm trong [`docs/MASTER-SYSTEM-PROMPT.md`](docs/MASTER-SYSTEM-PROMPT.md) — vốn là **global CLAUDE.md** cá
nhân của tác giả, được sao chép nguyên văn vào đây để plugin mang theo được, không phụ thuộc máy gốc.

Để có đầy đủ hành vi Project Manager + 6 team như dự án gốc, dán nội dung file đó vào `CLAUDE.md` (project
hoặc global) của nơi bạn cài plugin này. Nếu chỉ cần gọi từng skill riêng lẻ (ví dụ chỉ dùng
`content-writer` để viết bài), không bắt buộc phải làm bước này.

## Giấy phép

Toàn bộ nội dung trong repo này là tài sản riêng của tác giả, **trừ** `skills/compliance-checker/` —
skill này giữ nguyên MIT License gốc của Affitor (xem `skills/compliance-checker/LICENSE.txt`).
