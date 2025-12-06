# AI Resume & Cover Letter Generator - Design Guidelines

## Design Approach
**System**: Modern SaaS Productivity Design inspired by Linear, Notion, and Grammarly
**Rationale**: As a professional document generation tool, the interface must prioritize clarity, efficiency, and trust. The design should feel polished and credible while guiding users smoothly through a multi-step process.

---

## Typography System
- **Primary Font**: Inter (Google Fonts)
- **Secondary Font**: Source Serif Pro for document previews
- **Hierarchy**:
  - Page Headlines: text-4xl font-semibold (48px)
  - Section Titles: text-2xl font-semibold (24px)
  - Form Labels: text-sm font-medium uppercase tracking-wide
  - Input Text: text-base (16px)
  - Helper Text: text-sm opacity-70
  - Preview Text: text-base leading-relaxed

---

## Layout System
**Spacing Primitives**: Use Tailwind units of 2, 4, 6, 8, 12, and 16 (e.g., p-4, gap-6, my-12)

**Container Strategy**:
- Main content: max-w-7xl mx-auto px-6
- Form sections: max-w-3xl for optimal reading and input
- Document previews: max-w-4xl to simulate 8.5x11" paper proportions
- Split views (form + preview): 60/40 layout on desktop, stack on mobile

---

## Core Components

### Multi-Step Form Interface
**Progress Indicator**: Horizontal stepper at top showing 5 steps:
1. Personal Info → 2. Experience → 3. Education & Skills → 4. Job Details → 5. Generate

- Active step: bold with visual indicator
- Completed steps: checkmark icon
- Clickable to navigate between steps
- Fixed at top with subtle shadow on scroll

**Form Cards**: Each section in elevated card (shadow-md, rounded-lg, p-8)
- Grouped input fields with clear labels
- Auto-save indicator (small "Saved" text with checkmark)
- Field validation inline with helpful error messages
- Character counters for text areas

### Input Components
**Text Inputs**: Full-width with label above
- Border on all sides, focus state with ring
- Height: h-12 for single-line, min-h-24 for textareas
- Placeholder text descriptive and helpful

**Skill Tags**: Pill-style chips with remove icon
- Add via input + "Add Skill" button or Enter key
- Display in flex-wrap grid below input

**Date Ranges**: Two inputs side by side (Start - End) with "Present" checkbox option

**Job Description Input**: Large textarea (min-h-48) with:
- Paste detection helper text
- Word count indicator
- Optional "Analyze Job" button for AI insights

### Document Preview Panel
**Desktop**: Fixed right sidebar (sticky position) showing live preview
**Mobile**: Toggle button to switch between form and preview

Preview styling:
- White background simulating paper (shadow-lg)
- Padding: p-12 to simulate margins
- Template selector tabs above preview (Modern, Classic, Minimal)
- Zoom controls (100%, 125%, 150%)

### Generation Results View
**Two-Column Layout**:
- Left: Generated resume preview
- Right: Generated cover letter preview
- Both full-height, scrollable independently

**Action Bar** (sticky top): 
- "Download Resume" button (primary)
- "Download Cover Letter" button (primary)
- "Edit Resume" button (secondary outline)
- "Edit Cover Letter" button (secondary outline)
- "Start Over" button (ghost)
- Format dropdown (PDF, DOCX)

### Editing Interface
**Split Editor**: 
- Left panel: Rich text editor with formatting toolbar (bold, italic, bullet lists, headings)
- Right panel: Live rendered preview
- Floating save button (bottom-right)
- "Regenerate Section" buttons for AI refinement of specific parts

**Toolbar**: Sticky at editor top with:
- Format controls (B, I, U, list icons)
- Section headers dropdown
- AI assistant button ("Improve this section")

### Navigation
**Top Bar**: Full-width, minimal height (h-16)
- Logo/brand left
- Navigation minimal (this is a single-purpose app)
- User menu right (if authentication added)

**Bottom Navigation** (form steps):
- "Back" button (outline, left)
- "Save & Continue" button (primary, right)
- Center: step indicator (e.g., "Step 2 of 5")

---

## Key Screens Layout

### Landing Page
- Hero section (70vh): Bold headline "AI-Powered Resume & Cover Letter Generator", subheadline, primary CTA "Get Started Free"
- No background image, use subtle gradient or geometric shapes
- Features grid: 3 columns showcasing key benefits (icon + title + description)
- How It Works: 4-step visual timeline
- Social proof: Testimonials in 2-column cards
- Final CTA section with secondary benefits list

### Form Flow
- Single-column centered layout
- Progress stepper always visible at top
- One section visible at a time
- Generous spacing between form groups (gap-8)

### Results/Preview Page
- Full viewport height
- Dual document view on desktop
- Action buttons always accessible (sticky)
- Download modal with format selection and final customization options

---

## Animations & Interactions
**Minimal, purposeful only**:
- Smooth transitions between form steps (slide effect)
- Loading states during AI generation (skeleton screens for document preview)
- Success confirmations (subtle checkmark animations)
- No parallax, no scroll-triggered animations
- Button hover states: standard brightness/shadow changes

---

## Accessibility
- All form inputs with proper labels and aria-labels
- Keyboard navigation throughout multi-step form
- Focus indicators clearly visible
- Error messages announced to screen readers
- Color not sole indicator of validation state
- Sufficient contrast ratios for all text

---

## Images
**No large hero image required** - this is a productivity tool focused on functionality. Use subtle illustrations or abstract shapes if visual interest needed in landing hero section.

**Icons**: Use Heroicons throughout for consistency (form icons, navigation, status indicators)

---

## Key Design Principles
1. **Progressive Disclosure**: Show only what's needed at each step
2. **Instant Feedback**: Auto-save, validation, live preview all provide immediate response
3. **Professional Credibility**: Clean, sophisticated design that reflects the quality of output
4. **Guided Flow**: Clear next steps and progress indicators throughout
5. **Flexible Yet Focused**: Allow customization without overwhelming users