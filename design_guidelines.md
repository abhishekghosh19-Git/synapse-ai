# Design Guidelines: Advanced Self-Evolving AI Agent Platform

## Design Approach
**Selected System:** Material Design 3 with custom adaptations for complex data visualization and agent reasoning displays. This choice supports the information-dense, utility-focused nature of an advanced AI development platform while maintaining modern aesthetics and excellent usability for technical users.

## Typography System

**Font Stack:** Inter for UI, JetBrains Mono for code/data displays

**Hierarchy:**
- Hero/Page Titles: 32px (2xl), semibold
- Section Headers: 24px (xl), semibold  
- Component Titles: 18px (lg), medium
- Body Text: 16px (base), regular
- Captions/Labels: 14px (sm), medium
- Code/Data: 14px (sm), JetBrains Mono regular

## Layout System

**Spacing Primitives:** Fibonacci sequence - use units 2, 3, 5, 8, 13, 21 consistently
- Micro spacing (elements): `p-2`, `gap-3`
- Component padding: `p-5`, `p-8`
- Section spacing: `py-13`, `py-21`
- Major separations: `gap-21`, `mb-21`

**Grid Structure:**
- Three-column desktop layout: Sidebar (280px) | Main Chat (flex-1) | Inspector Panel (360px)
- Responsive collapse: Panels overlay on tablet/mobile
- Container max-width: `max-w-screen-2xl` with `px-8`

## Core Component Library

### Navigation & Layout

**Primary Sidebar (Left)**
- Fixed position, full height
- Logo/branding at top (`h-13`)
- Model selector dropdown with status indicators
- Prompt technique library (collapsible tree structure)
- Integration connections list with toggle states
- Language selector at bottom
- Session history (scrollable middle section)

**Main Chat Area**
- Full-height scrollable container
- Messages with generous vertical spacing (`gap-8`)
- Input composer at bottom (sticky)
- Context compression indicator banner (dismissible)
- Floating action button for new session

**Inspector Panel (Right)**
- Tabbed interface: Reasoning Tree | Analytics | Memory | Settings
- Collapsible sections within tabs
- Real-time visualization canvas
- Compact data tables with zebra striping

### Chat Components

**Message Bubbles**
- User messages: Right-aligned, max-width 70%
- AI responses: Left-aligned, full-width
- Padding: `px-5 py-3`
- Border radius: `rounded-2xl`
- Elevation: subtle shadow for user, none for AI
- Generous whitespace between messages: `gap-8`

**Reasoning Display**
- Expandable/collapsible sections showing CoT steps
- Indented tree structure for ReAct loops (indent by `ml-8` per level)
- Tool call badges (pill-shaped, `rounded-full`)
- Timeline visualization for sequential reasoning
- Syntax highlighting for code blocks

**Input Composer**
- Multi-line textarea with auto-expand (max 200px)
- Technique selector (chip-based interface)
- Model switcher (inline dropdown)
- Attachment controls (icons only, `size-5`)
- Send button (primary CTA, `h-13 px-8`)

### Data Visualization

**Performance Dashboard**
- Grid layout: 2×2 on desktop, single column mobile
- Metric cards with large numbers (`text-4xl`)
- Sparkline charts (compact, `h-21`)
- Compression ratio gauge (circular progress)
- Exploration/exploitation balance bar chart

**Reasoning Tree Visualizer**
- Node-link diagram with pan/zoom
- Expandable nodes showing detailed reasoning
- Edge labels for tool calls/actions
- Color-coded node types (thought/action/observation)
- Minimap in corner for navigation

### Prompt Engineering Library

**Technique Selector**
- Modal overlay with search
- Categorized accordion sections
- Technique cards showing: Name, Description, Use Cases, Combinable With
- Multi-select with combination preview
- Quick templates (pre-configured combinations)
- Badge count showing active techniques

### Settings & Configuration

**Tabbed Settings Panel**
- General: Language, theme preferences, shortcuts
- Models: API keys, rate limits, fallback rules
- Compression: Threshold settings, semantic vs. fixed
- Learning: Meta-learning toggles, self-reflection depth
- Advanced: MDP parameters, exploration rate (ε), golden ratio coefficients

**Form Controls**
- Labels above inputs (14px medium)
- Helper text below (12px)
- Toggle switches for binary options
- Sliders for continuous values (with live preview)
- Grouped related settings in bordered sections (`rounded-lg`, `p-5`)

## Interaction Patterns

**Progressive Disclosure:** Complex features start collapsed, expand on demand
**Inline Editing:** Click-to-edit for session names, saved prompts
**Contextual Actions:** Hover reveals action buttons on messages/nodes
**Keyboard Navigation:** Full support with visual focus indicators
**Loading States:** Skeleton screens for data-heavy panels, typing indicators for AI responses

## Accessibility

**Focus Management:**
- Visible focus rings: 2px solid with `ring-offset-2`
- Skip-to-content links
- Logical tab order throughout complex layouts

**ARIA Labels:**
- All interactive elements labeled
- Live regions for AI response streaming
- Role assignments for custom components

**Semantic Structure:**
- Proper heading hierarchy
- Landmarks for major sections
- Descriptive button text (no icon-only without labels)

## Animations

**Use Sparingly:**
- Message appearance: Fade + slide up (150ms)
- Panel transitions: Slide (200ms ease-out)
- Tree expansion: Smooth height (200ms)
- Loading spinners: Subtle rotation
- NO auto-playing or distracting animations

## Images

**No hero image** - This is a productivity tool, not a marketing page. The main area immediately shows the functional chat interface.

**Icon Usage:**
- Heroicons throughout (via CDN)
- 20px (size-5) for inline actions
- 24px (size-6) for navigation
- 32px (size-8) for empty states

## Responsive Behavior

**Desktop (1280px+):** Three-column layout fully visible
**Tablet (768-1279px):** Sidebar + Main, Inspector overlays
**Mobile (<768px):** Full-screen Main with hamburger menu for Sidebar, bottom sheet for Inspector

**Touch Targets:** Minimum 44×44px for all interactive elements on mobile