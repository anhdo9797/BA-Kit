# PRD Template / Product Requirements Document (Screen-Spec Format)

---

## Metadata

| Attribute | Value |
|-----------|-------|
| **Template ID** | TMPL-PRD |
| **Category** | Template |
| **Load When** | Phase 1 (PRD Draft) and Phase 4 (PRD Final) of the Product Delivery Workflow |
| **Dependencies** | @ba-elicitation (Discovery Brief), @ba-writing (PRD Mode), @ba-ux (Wireframe), @ba-validation (PRD Review) |
| **Reference Samples** | `draft/[Foodlens] - Barcode & OCR Ingredients Scanner.pdf` (UI-heavy), `draft/[Foodlens] - Homepage.docx` (lists, history, empty state), `draft/[Foodlens] - Product Search.docx` (logic-heavy: search model, sorting, filtering) |
| **Output** | `outputs/<project>/<feature>/01-prd-draft/prd-v0.x.md` → `04-final/prd-v1.0.md` (+ `.docx`) |

> **RULE 1**: The PRD MUST follow this structure. Do NOT add generic sections
> (Success Metrics, NFR, Risks, Personas, Timeline...). Anything outside it goes to the
> Discovery Brief or Review Log.
>
> **RULE 2**: Before writing, read sibling PRDs of the same product (in `draft/` or provided by the user).
> Reuse their Vision text verbatim, their component names and their cross-reference targets.
>
> **RULE 3**: Think with the **Reasoning Framework (§3)**, not only the skeleton. A PRD that has every
> heading but skips the reasoning lenses is incomplete.

---

## 1. Document Structure (fixed order)

| # | Section | Required | Content |
|---|---------|----------|---------|
| 0 | **Cover** | ✅ | Company name, FEATURE NAME (UPPERCASE), Version, Date |
| — | **Table of contents** | Optional | Auto-generated in DOCX when the PRD has > 6 sections |
| 1 | **Changelog** | ✅ | Table: Version · Changelog · Author · Date |
| 2 | **Objectives & Highlight** | ✅ | Table: Vision · Goal · Design – Figma LINK |
| 3 | **Features** | ✅ | Table: Feature · Description · Purpose (bullets) |
| 4 | **Logic / Model sections** | When the feature has business logic | Data model, processing rules, matching/ranking, sorting, filtering, evaluation logic — written BEFORE the UI sections that use them |
| 5 | **Entry Point** | When the screen is reachable from elsewhere | Where/how the user reaches the feature and the initial state |
| 6 | **Shared behavior sections** | When several screens share it | e.g. Sticky Header: hành vi chung + thành phần |
| 7..n | **Screen / Component sections** | ✅ | One per screen, area of a screen (Header, Shortcuts, Recent Scans, Bottom navigation...), bottom sheet, pop-up or system state. Use Heading 3 for areas inside a screen |
| — | **Open Questions** | Draft only | `[TBD-xx]` list. MUST be empty and removed in PRD Final |

Date format: one format per document, consistent between Cover and Changelog (default `DD/MM/YYYY`, or follow the sibling PRDs).

---

## 2. Skeleton

````markdown
<!-- ===================== COVER ===================== -->
# [COMPANY]

# [FEATURE NAME IN UPPERCASE]

Version [X.Y]
[DD/MM/YYYY]

---

## Changelog

| Version | Changelog | Author | Date |
|---------|-----------|--------|------|
| 0.1 | Created the document | [Author] | [DD/MM/YYYY] |

---

## Objectives & Highlight

| | |
|---|---|
| **Vision** | [Product-level vision — copy verbatim from sibling PRDs of the same product.] |
| **Goal** | [Giúp người dùng <làm gì> <bằng cách nào>, thay vì <cách cũ/khó hơn>. Đồng thời <giá trị phụ>.] |
| **Design – Figma** | [LINK] |

---

## Features

| Feature | Description | Purpose |
|---------|-------------|---------|
| [Feature name] | [Cho phép người dùng ... / [Feature] là ..., nơi người dùng có thể ...] | • [Lợi ích cho user 1]<br>• [Lợi ích 2]<br>• [Giảm thao tác / thời gian ...] |

---

<!-- ============ LOGIC / MODEL SECTION (pattern: Product Search) ============ -->
## [Logic name, e.g. Search Model / Evaluation Logic]

1. Cấu trúc dữ liệu phục vụ [logic]

   | Nhóm | Trường dữ liệu | Mục đích |
   |------|----------------|----------|
   | Định danh | [field] | [vì sao cần] |

2. Logic xử lý [input]
   a. Điều kiện [xử lý]
      i. Input rỗng hoặc chỉ chứa khoảng trắng: [không gửi request]
      ii. [Ngưỡng hợp lệ, e.g. 3–100 ký tự]: [cho phép]
      iii. [Dưới ngưỡng]: [trạng thái chờ]
      iv. Khi người dùng xóa toàn bộ [input]: [quay về trạng thái mặc định]
   b. Chuẩn hóa [input]: [trim, gộp khoảng trắng, không phân biệt hoa thường, không loại bỏ ký tự có nghĩa]
3. [Matching / Ranking / Evaluation]
   a. Thứ tự ưu tiên: [A] -> [B] -> [C]
      i. [Mức 1 – tên]: [định nghĩa]
         1. Ví dụ: “[input]” -> “[kết quả]”
   b. Chú ý:
      i. [Không trùng lặp kết quả]
      ii. [Nguyên tắc không được vi phạm, e.g. exact match không bị đẩy xuống dưới partial match]
   c. Tiêu chí phụ (tie-breaker): [1] -> [2] -> [3]
      // [Phạm vi version: tiêu chí X có thể chưa bắt buộc ở ver đầu nếu chưa có dữ liệu ổn định]
4. [Sorting / Rule table]

   | [Option] | Quy tắc |
   |----------|---------|
   | [Default option] | Mặc định; [quy tắc] |

   a. Quy tắc xử lý dữ liệu thiếu: [item thiếu dữ liệu xếp cuối, không mặc định là tốt nhất]
   b. Khi bằng nhau: dùng [tiêu chí] làm tiêu chí phụ để giữ thứ tự ổn định
5. [Combination rules, e.g. Filtering]
   a. Khác nhóm: AND · Cùng nhóm: OR
   b. Ví dụ: [worked example with concrete values]
   c. Khi [input] thay đổi: [giá trị không còn hợp lệ bị bỏ chọn, kết quả cập nhật]

<!-- ===================== ENTRY POINT ===================== -->
## Entry Point

1. Người dùng có thể truy cập [màn hình] từ [vị trí: tab / button / deeplink]
2. Khi [hành động], [màn hình] được mở ở trạng thái [mặc định / mode được chọn sẵn]

<!-- ============ SCREEN / COMPONENT SECTION (pattern: Scanner) ============ -->
## [Screen / Component Name]

![[Screen name] – [state]](images/[screen-slug]-[state].png)
<!-- Callout numbers on the image MUST match the level-1 numbers below. -->

1. [UI element, e.g. “x” icon]
   a. Hiển thị [vị trí]
   b. Mặc định [trạng thái]
   c. Hành vi: nhấn vào [element] sẽ [kết quả]
2. [Element reused from another PRD]
   a. Tương tự như được định nghĩa tại [Product] - [Doc] > [Section]
   b. Khác biệt: [only the delta, e.g. Tiêu đề bottom sheet: “Shopping for”]
3. [Element that opens a bottom sheet / pop-up]
   a. Khi chọn, [bottom sheet] “[Title]” sẽ được mở ra
   ![[Bottom sheet]](images/[slug].png)
      i. Tiêu đề: “[Title]”
      ii. “x” icon: nhấn vào icon này hoặc nhấn ra ngoài sẽ đóng [bottom sheet], và không lưu những thay đổi (nếu có)
      iii. Trường nhập
         1. Placeholder: “[Placeholder]”
         2. Quy tắc
            a. Chỉ cho phép nhập [loại ký tự]
            b. Tối thiểu [N] ký tự: nếu ít hơn, nút [CTA] sẽ bị disable
            c. Tối đa [M] ký tự: không cho phép nhập thêm ([lý do])
      iv. CTA button
         1. Nhãn nút: “[Label]”
         2. Trạng thái: disable cho đến khi [điều kiện]
         3. Hành vi: nhấn vào nút này sẽ
            a. Chuyển button sang trạng thái loading
            b. Vô hiệu hóa toàn bộ action khác trên trang
            c. [Kết quả thành công]
            d. Hiển thị toast msg: “[Message]” ([N] giây, vuốt xuống để tắt[, kèm Undo])
4. [Error / edge case]
   a. Nếu [điều kiện lỗi], app hiển thị [dialog / toast / màn hình lỗi]
      i. Tiêu đề: “[Error title]”
      ii. Phụ đề: “[Error message]”
      iii. CTA button: [Try again] – [hành vi]

<!-- ============ LIST / COLLECTION SECTION (pattern: Homepage) ============ -->
## [List name, e.g. Recent Scans]

![[List] – [state]](images/[slug].png)

1. Mục đích: [list giúp người dùng làm gì]
2. Điều kiện để item được hiển thị:
   a. [Điều kiện dữ liệu 1]
   b. [Điều kiện 2]
   c. Phạm vi xét: [toàn bộ profile / chỉ profile đang chọn]
3. Danh sách [items]:
   a. Số lượng: tối đa [N] items; section chỉ hiển thị khi có ≥ [K] items, nếu 0–[K-1] -> [ẩn section / empty state]
   b. Sắp xếp: [tiêu chí] ([mới nhất → cũ nhất / A -> B])
   c. Mỗi item gồm:
      i. [Hình ảnh]: nếu lỗi, dùng ảnh mặc định của hệ thống
      ii. [Tên]: tối đa [1] dòng, dài hơn dùng (...)
      iii. [Field tùy chọn]: nếu không có, ẩn đi
      iv. [Trạng thái / giá trị tính toán]: [cách tính; snapshot hay live]
      v. [Thời gian]: theo bảng hiển thị

      | Khoảng thời gian | Hiển thị |
      |------------------|----------|
      | < 1 phút | Just now |

   d. Hành vi:
      i. Nhấn vào item: mở [màn hình] với [context được mang theo]; [section nào bị ẩn ở màn đích]
      ii. [Toggle icon]: Outline -> thêm; Filled -> xóa
      iii. Cuộn [ngang / dọc] để xem thêm
   e. Note: [vòng đời dữ liệu liên quan]
      i. Nếu [entity] bị đổi tên sau khi bản ghi được lưu: [hiển thị tên mới nhất]
      ii. Nếu [entity] bị xóa: [giữ tên cuối cùng / hiển thị dưới dạng {+N more} / vẫn tính vào tổng]
4. Nút [View all]: chỉ hiển thị khi có ≥ 1 item; hành vi: mở [màn hình danh sách đầy đủ]
5. Empty List
   a. Điều kiện hiển thị: [khi nào]
   b. Bao gồm: hình minh họa, Tiêu đề “[...]”, Phụ đề “[...]”
   c. Nút CTA: [Label] – Hành vi: mở [màn hình] – mode tự động chọn [mode]

<!-- ===================== DRAFT ONLY ===================== -->
## Open Questions

| ID | Section › Item | Question | Proposed default | Owner | Status |
|----|----------------|----------|------------------|-------|--------|
| TBD-01 | [Screen › 3.a.ii] | [Câu hỏi còn mở] | [Đề xuất] | [Who] | Open |
````

---

## 3. Reasoning Framework (think like the PRD author)

Apply every lens that fits to every section. Each lens is a set of questions the PRD must answer in text.

### L1. Purpose first
- Every section and every non-trivial element starts from **Mục đích**: why does this exist for the user?
- Goal sentence contrasts with the alternative: "giúp người dùng X, thay vì phải Y".

### L2. Visibility & conditions
- When is it shown / hidden? (`Điều kiện hiển thị`, `Chỉ hiển thị khi ...`, `ẩn đi khi ...`)
- Eligibility rules for items (data complete enough? status in an allowed set?).
- Thresholds: minimum count to show the section, maximum items displayed, what happens below the minimum.
- Scope of evaluation: all profiles vs. the currently selected profile vs. the active profile.

### L3. State machine of each element
- Default state on entry; every state (empty, enabled, disabled, loading, error, max reached, permission denied).
- Toggles in **both** directions (Outline → add, Filled → remove; OFF → AUTO → ON).
- Anti-spam: during processing, ignore new triggers and disable other actions.

### L4. Input & processing logic
- Empty / whitespace-only input, below-min, valid range, above-max (with the reason for limits).
- Normalization (trim, merge spaces, case-insensitive, keep meaningful characters).
- Clearing the input returns to the default state — never processes an empty value.

### L5. Ordering, priority & tie-breakers
- Explicit priority chain `A -> B -> C` with a definition and an **Ví dụ** per level.
- Tie-breaker chain to keep results stable; principle sentences that must never be violated.
- When the user applies an explicit sort, which default ranking is dropped.

### L6. Missing / bad data
- Image error → default system image; optional field missing → hide; long text → max lines + (...).
- Items missing the sort key go last and are never treated as "best"/"most popular".
- Data source and field mapping when it matters (e.g. parent vs child values of `food_groups_tags`).

### L7. Combination rules
- Multi-select within a group = OR; across groups = AND — always with a worked example of concrete values.
- When upstream input changes (new keyword), dependent selections that become invalid are removed and results refresh.

### L8. Entity lifecycle & history consistency
- Create / rename / delete / undo of related entities (profile, favorite, history record).
- Snapshot vs live: which values are frozen at save time (overall fit status) and which follow the latest data (renamed profile name).
- Deleted entities in history: keep last name, display rule (`{+N more}`, disabled + tag "Profile deleted"), still counted in totals.
- Deleting one thing must state what is NOT deleted (history and favorites kept).

### L9. Sync & persistence
- Shared settings stay in sync across every screen that shows them (Homepage, Camera, Profile, Search) and survive tab switches and app restarts.
- Limits that may change are remote config with a stated Default.

### L10. Navigation & context hand-off
- Destination + preset state ("mở màn hình camera – mode tự động chọn [Barcode]").
- What context travels with the user (selected profiles) and what changes on the destination (section "Try these instead" hidden).
- Back / close / outside tap / swipe-down behavior and whether changes are saved.

### L11. Feedback
- Exact copy for toast / dialog / inline message, duration in seconds, dismiss gesture, Undo and what Undo restores (position + all data).

### L12. Reuse across PRDs
- Shared components are defined once; other PRDs reference `[Product] - [Doc] > [Section]` and describe only the delta.
- Before writing a component, check whether a sibling PRD already defines it.

### L13. Version scope
- Mark criteria that are not mandatory in v1 (`// có thể chưa bắt buộc ở ver đầu nếu chưa có dữ liệu ổn định`) instead of silently dropping them.
- Ranges like "5–10" are not decisions: pick a value or raise a TBD.

---

## 4. Writing Conventions (MUST follow)

### 4.1 Language
- Descriptions, rules, behaviors: **Vietnamese**.
- UI copy (titles, subtitles, placeholders, button labels, toast/error messages): **English**, exactly as on screen, in “smart quotes”.
- Technical / product terms stay English: barcode, OCR, toast, bottom sheet, pop-up, CTA, remote config, profile, tab, scan, loading, enable/disable, sticky, exact/prefix/partial match.

### 4.2 Numbering hierarchy
`1.` → `a.` → `i.` → `1.` → `a.` → `i.` (repeat). In UI sections, level-1 items are **UI elements in on-screen order**
(top → bottom, left → right) and MUST match the callout numbers on the wireframe/design image.

### 4.3 Fixed labels
| Label | Use for |
|-------|---------|
| `Mục đích:` | Why the section/element exists |
| `Điều kiện hiển thị:` / `Điều kiện để ...:` | Visibility / eligibility |
| `Hiển thị ...` | Position / visibility |
| `Mặc định ...` | Default state on entry |
| `Bao gồm:` | Anatomy of a card / banner / item |
| `Hành vi:` | What happens on tap / swipe / auto-trigger |
| `Tiêu đề:` / `Phụ đề:` | Title / subtitle copy |
| `Placeholder:` / `Text hướng dẫn:` / `Nội dung:` | Input placeholder / helper text / message body |
| `Nhãn nút:` | Button label |
| `Số lượng:` / `Sắp xếp:` / `Thứ tự ...` | Count limits / sort order / state cycle |
| `Quy tắc` | Validation or business rules |
| `Trạng thái:` | Enabled / disabled / loading / hidden conditions |
| `Ví dụ:` | Concrete example (input -> output) |
| `Chú ý:` / `Note:` / `//` | Principles, lifecycle edge cases, notes for dev & QA |

### 4.4 Notation
- Buttons / tabs / modes: `[Save]`, `[Home]`, `[Barcode]`. Icons: `“x” icon`, `icon Edit`.
- Variables: `{Profile Name}`, `{x}`, `{+N more}` — always define what the variable equals.
- Remote config: `Số lượng maximum được remote config (Default = 5)`.
- Cross-reference: `[Product] - [Doc name] > [Section / Screen N – Name]`.
- Rationale for a limit in parentheses: `Tối đa 100 ký tự (tránh input quá dài gây lỗi xử lý)`.
- Mapping rules (time formats, sort options, status labels) as a 2-column table.

---

## 5. Versioning

| Phase | Version | Status |
|-------|---------|--------|
| 1 – PRD Draft | 0.1, 0.2 ... | Draft (Open Questions section present) |
| 3 – Review | 0.x (+1 per review round) | In Review — every accepted comment logged in Changelog |
| 4 – PRD Final | 1.0 | Final — Open Questions removed, wireframes replaced by final design |
| Change after Final | 1.1, 1.2 ... | Changelog describes the delta |

---

## 6. PRD Quality Checklist (used by @ba-validation in Phase 3)

| # | Check | Pass Criteria |
|---|-------|---------------|
| 1 | Structure | Sections in §1 order; logic sections before the UI sections that use them |
| 2 | Objectives | Vision matches sibling PRDs; Goal states the user benefit vs. alternative; Figma link (Final) |
| 3 | Features table | Every feature has Description + Purpose bullets and ≥1 section |
| 4 | Screen coverage | Every screen/state in the wireframe has a section; every UI section has an image |
| 5 | Callout match | Level-1 numbers = image callouts, same order |
| 6 | Reasoning lenses | Every applicable lens L1–L13 answered (§3) |
| 7 | Copy | All UI copy in English, quoted; no empty or truncated sentences (“Thông báo lỗi:” with nothing after) |
| 8 | Numbers | Concrete values; no vague words (nhanh, hợp lý, phù hợp, tối ưu, ở mức phù hợp) and no undecided ranges (5–10) |
| 9 | System states | Permissions, loading/anti-spam, empty, not found, error, limit reached covered |
| 10 | Consistency | No copy-paste leftovers (wrong screen name, line belonging to another element); same element behaves the same everywhere; scope statements do not contradict each other |
| 11 | Cross-references | Every `[Product] - [Doc] > [Section]` target exists; only the delta is described |
| 12 | Open Questions / Design sync | Final: zero TBD; copy & layout match Figma |

---

## Related BA-Kit Agents

| Phase | Agent | Role |
|-------|-------|------|
| 0 Discovery | `@ba-master` → `@ba-elicitation` | Interview, Discovery Brief |
| 1 PRD Draft | `@ba-writing` (PRD Mode) | Fill this template with the Reasoning Framework |
| 2 Wireframe | `@ba-ux` (Wireframe Mode) | Markdown wireframe → HTML (Figma only on explicit confirmation) |
| 3 Review | `@ba-validation` (PRD Review Mode) | Checklist §6 + Review Log |
| 4 Final | `@ba-writing` + `@ba-consistency` | PRD ↔ Figma sync, v1.0 |
| 5 Development | `@ba-export`, `@ba-test-gen`, `@ba-jira` | DOCX, test cases, tickets |
