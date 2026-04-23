# Project: Authentication Pages

## Pages

### login.html
- **Purpose**: User sign-in page
- **Components**:
  - Email input (required)
  - Password input (required)
  - "Remember me" checkbox
  - "Forgot password?" link
  - Primary "Sign In" button
  - Social login buttons: Google, GitHub, Facebook (inline SVG icons)
  - Footer link: "Don't have an account? Sign up" (links to register.html)
- **Result**: On submit, form validates required fields before submission

### register.html
- **Purpose**: User registration page
- **Components**:
  - Full Name (required)
  - Email (required, regex validated)
  - Password (required, min 8 chars)
  - Confirm Password (required, must match)
  - Phone (optional, max 10 digits, numeric-only)
  - Gender (optional, dropdown: Male/Female/Other)
  - Address (optional)
  - Terms of Service checkbox (required)
  - Primary "Create Account" button
  - Footer link: "Already have an account? Sign in" (links to login.html)
- **Result**: On submit, validates all fields; shows inline error messages on failure

## Design Rules

### Color Theme
| Variable | Value | Usage |
|---|---|---|
| `--bg-base` | `#090A14` | Page background |
| `--bg-card` | `#1f2937` | Card / form background |
| `--primary` | `#DF6B33` | CTA buttons, links, focus rings |
| `--primary-hover` | `#c55a2a` | Hover state for primary |
| `--border` | `#374151` | Borders, dividers |
| `--input-bg` | `#374151` | Input background |
| `--input-border` | `#4b5563` | Input border |
| `--text-white` | `#ffffff` | Primary text |
| `--text-gray` | `#9ca3af` | Secondary text, labels |
| `--text-muted` | `#6b7280` | Placeholder text, muted text |
| `--error` | `#ef4444` | Validation error messages |

### Fonts
- **Headings** (h1-h6): `Poppins`, weight 700–800
- **Body**: `Inter`, weight 400
- Load via Google Fonts: `https://fonts.googleapis.com/css2?family=Inter:wght@400&family=Poppins:wght@700;800&display=swap`

### Icons
- **Library**: Lucide Icons (CDN: `https://unpkg.com/lucide@0.379.0/dist/umd/lucide.js`)
- **Usage**: Initialize with `lucide.createIcons()` after DOM load
- **Social icons**: Use inline SVG (Google G, GitHub mark, Facebook F) for branded accuracy

### CSS Approach
- Pure CSS (no Tailwind CDN to avoid production warnings)
- CSS Variables for all theme values
- Single HTML file, no build step required
- Box-shadow uses `rgb(0 0 0 / 0.3)` syntax for consistency

### Responsive Breakpoints
| Breakpoint | Behavior |
|---|---|
| `≤ 480px` | Card padding reduced; form-row switches to column layout |
| `≤ 360px` | Further card padding and title size reduction |

### Form Validation
- Client-side JavaScript validation
- Inline error messages (`.form-error`) shown/hidden via `.visible` class
- Error state on inputs via `.error` class (red border)
- `autocomplete` attributes for browser autofill support

### Accessibility
- `aria-label` on icon-only buttons
- `.sr-only` class for screen reader text
- `autocomplete` attributes on form fields
- Focus rings using box-shadow (no default outline)

### Navigation Links
- Always provide reciprocal links between related pages:
  - login.html → register.html ("Don't have an account?")
  - register.html → login.html ("Already have an account?")

### File Structure
```
login.html      — Sign in page
register.html   — Registration page
charts.html     — E-Commerce Analytics Dashboard
CLAUDE.md       — This documentation file
```

---

## Charts Dashboard (charts.html)

### Purpose
E-Commerce analytics dashboard displaying sales revenue, business results, and marketing performance data using Recharts and tables.

### Sections

#### 1. KPI Summary Cards (4 cards)
| KPI | Value | Change |
|---|---|---|
| Total Revenue | $826,900 | +12.5% vs last year |
| Total Orders | 5,451 | +8.3% vs last year |
| Conversion Rate | 3.84% | +0.6% vs last month |
| Avg. Order Value | $151.70 | -2.1% vs last month |

Each card has: label, icon (inline SVG), value, change indicator (up/down arrow + percentage).

#### 2. Sales Revenue (Recharts)
- **Bar Chart**: Monthly revenue for last 12 months (May–Apr)
- **Line Chart**: Toggleable dual-line (Revenue + Orders)
- Tab switcher: Bar / Line
- Custom tooltip matching dark theme

#### 3. Revenue by Category (Recharts PieChart)
- 5 categories: Electronics (38%), Fashion (24%), Home & Living (18%), Beauty (12%), Sports (8%)
- Donut chart with legend

#### 4. Business Results (Recharts)
- **Area Chart**: Revenue vs. Profit gradient fill
- **Bar Chart**: Toggleable revenue/profit bars
- Tab switcher: Area / Bar
- 12 months of data with linear gradient fills

#### 5. Top Products Table
Columns: Rank, Product Name, Category (badge), Units Sold, Revenue, Growth (%)
5 products: Wireless Earbuds Pro, Smart Watch Series X, Premium Laptop Stand, Running Shoes Ultra, Moisturizing Cream 500ml.

#### 6. Marketing Campaigns Table
Columns: Campaign Name, Channel (badge), Spend, Conversions, ROI, Status
6 campaigns across Email, Google Ads, Facebook, Instagram, Partners.

### Tech Stack
- **Chart.js 4.4.0** (CDN UMD) — stable, no React/Babel dependency
- **Vanilla JavaScript** — no JSX, no build step, no transpilation
- **Inline SVG icons** — Lucide CDN not needed for this page
- **Google Fonts**: Inter (400, 500, 600) + Poppins (600, 700, 800)

### Design Adherence
- Same CSS Variables as auth pages (bg-base, primary, card, border, text-*)
- Same responsive breakpoints (1024px, 640px, 400px)
- Page navigation links to login.html and register.html
- Chart.js global defaults set to match dark theme (color, font)
- Custom tooltip styling matching dark theme via Chart.js `tooltipDefaults` object
- Badge component with color variants (orange, green, blue, yellow, purple)
