# Simple Calendar SDD Overview

## Roles & Responsibility Model
1. **Senior Architect / Experience Strategist**  
   - Owns the product vision, ensures accessibility, performance, and harmony between views.  
   - Coordinates UI patterns and ensures drag/drop + modal + export workflows align with the spec.
2. **UI Web Designer**  
   - Defines the visual system (spacing, typography, light/dark tokens, block states, hover/drag cues).  
   - Produces the polished statics that the implementer turns into CSS/HTML.
3. **Frontend Implementer**  
   - Builds the HTML/CSS/JS to match the approved spec, including ISO week calculations, modal autosave, drag-drop markers, spacer blocks, and export guardrails.  
   - Ensures exported imagery doesn’t leak UI controls.
4. **Quality Assurance / Implementation Reviewer**  
   - Tests every change against the spec (dark mode legibility, drag behavior, block ordering, modal autosave and delete, export output).  
   - Provides the final sign-off before changes are released.

## Experience Spec Highlights
- **Header**: Displays `WXX — Month YYYY`, a week-selector (prev/next/week dropdown), and year pill. Action buttons (dark toggle, export PNG/PDF, Add block) should look like pills, adapt to dark mode, and remain accessible.
- **Calendar Grid**: 7 columns; weekend columns have a subtle darker background. Each column header shows date/day and a “+ Add” pill aligning top-right.
- **Task Blocks**: Rounded pastel squares with a small floating edit icon. Titles and descriptions use semantic vars (`--card-title`, `--card-desc`) so both light/dark modes remain legible. Spacer blocks render as dashed top/bottom lines with centered label text.
- **Drag & Drop**: Show a dashed drop marker while dragging, allow dropping onto any day (including weekends), and place cards in the intended order (not just append). The drop marker color adapts from `--border`.
- **Modal**: Opens from “Add” button or card click, defaults to the selected day, autosaves on each change, and requires only a title. Includes delete action when editing and closes on background click, saving pending edits automatically.
- **Exports**: Capture the calendar wrapper without UI controls (hide “+ Add”/edit icons). PNG/PDF commands rely on bundled `html2canvas` and `jsPDF` with error alerts if they fail.
- **Dark Mode**: Entire page switches to dark variables, ensuring headers, cards, buttons, and descriptions use high-contrast colors. Global tokens drive these color changes so new components automatically inherit the correct palette.

