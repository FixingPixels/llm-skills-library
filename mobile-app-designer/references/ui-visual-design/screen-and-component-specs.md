# Screen and Component Specs

Reference for dimensions, safe areas, asset export, component structure, and design token vocabulary. Use before commissioning design work, handing off to a developer, or setting up a Figma file.

---

## iOS screen sizes (points, not pixels)

Design in points (pt). The device multiplier (@2x, @3x) produces pixels.

| Device | Screen size (pt) | Scale | Pixels |
|--------|-----------------|-------|--------|
| iPhone 16 Pro Max | 440×956 pt | @3x | 1320×2868 px |
| iPhone 16 / 15 Pro | 393×852 pt | @3x | 1179×2556 px |
| iPhone 16 Plus / 15 Plus | 430×932 pt | @3x | 1290×2796 px |
| iPhone 14 / 13 / 12 | 390×844 pt | @3x | 1170×2532 px |
| iPhone SE (3rd gen) | 375×667 pt | @2x | 750×1334 px |
| iPad Pro 12.9" | 1024×1366 pt | @2x | 2048×2732 px |
| iPad Pro 11" | 834×1194 pt | @2x | 1668×2388 px |
| iPad Air / mini | varies | @2x | varies |

**Design target**: 390×844pt (iPhone 14) is the standard base for most iOS designs. It covers most of the active install base and scales cleanly to smaller and larger devices with auto-layout.

**App Store screenshot dimensions**:
- iPhone 6.5" screenshots: 1290×2796px (required for most App Store submissions)
- iPhone 5.5" screenshots: 1242×2208px (older, but often still required)
- iPad 12.9" screenshots: 2048×2732px (if supporting iPad)

---

## Android screen sizes (dp, not pixels)

Design in dp (density-independent pixels). Android uses density buckets.

| Density bucket | Density | Scale | Common use |
|---------------|---------|-------|------------|
| mdpi | 160 dpi | @1x baseline | Rarely a design target |
| hdpi | 240 dpi | @1.5x | Older low-end devices |
| xhdpi | 320 dpi | @2x | Common mid-range |
| xxhdpi | 480 dpi | @3x | Most current mid/high-end |
| xxxhdpi | 640 dpi | @4x | High-end flagships |

**Common phone sizes in dp**:
- Standard range: 360×800 dp to 412×892 dp
- Safe design target: 360×800 dp (covers most of the Android install base)

**Play Store screenshot dimensions**: 1080×1920px minimum (portrait), up to 3840px longest side.

---

## Safe areas

Safe areas are regions of the screen guaranteed to be unobstructed by system UI. Content critical to usability (buttons, input fields, key information) must be within the safe area.

### iOS safe areas

| Element | Approximate height |
|---------|-------------------|
| Status bar (with Dynamic Island) | 59pt (iPhone 14 Pro and newer) |
| Status bar (without notch) | 44pt (iPhone SE) |
| Home indicator | 34pt at bottom |
| Tab bar (system) | 49pt + home indicator |
| Navigation bar (large title) | 96pt (includes status bar) |
| Navigation bar (small title) | 44pt (not including status bar) |

**Rule**: The UIKit/SwiftUI `safeAreaInsets` system handles this automatically for standard components. Custom layouts must respect it manually. In Figma, use the iOS UI kit frame templates which include safe area guidelines.

### Android safe areas

| Element | Approximate height |
|---------|-------------------|
| Status bar | 24dp |
| Navigation bar (gesture) | 20dp bottom |
| Navigation bar (3-button legacy) | 48dp bottom |
| App bar (standard) | 56dp |
| Bottom navigation bar | 56dp + navigation bar |

**Rule**: Use `WindowInsets` in Jetpack Compose or `fitSystemWindows` in XML layouts to handle insets automatically. In Figma, use Material Design 3 frame templates.

---

## Asset export

### iOS asset export

Every bitmap asset is exported at three scales. Name files with the scale suffix.

```
icon.png           (not used for app icon — see below)
icon@2x.png
icon@3x.png
```

**App icon export** — a single 1024×1024px PNG (no alpha channel, App Store requires solid background). Xcode generates all required sizes from this single asset. Do not add rounded corners — iOS applies them automatically.

**Image assets in Xcode**: Place in `.xcassets` as 1x / 2x / 3x variants. The system loads the correct scale for the device automatically.

**SF Symbols**: vector, no export needed — reference by name in code. Use the SF Symbols app to check availability by iOS version. Render at any point size; adjust weight via font weight API.

### Android asset export

Android uses density buckets. For launcher icons, use adaptive icons (foreground + background layers).

```
res/
  drawable-mdpi/   icon.png   (48×48px)
  drawable-hdpi/   icon.png   (72×72px)
  drawable-xhdpi/  icon.png   (96×96px)
  drawable-xxhdpi/ icon.png   (144×144px)
  drawable-xxxhdpi/icon.png   (192×192px)
```

**Vector drawables (Android)**: For icons and simple graphics, use SVG → import as Android Vector Drawable (`.xml`). Scales without density variants. Preferred over bitmaps for icons.

**Material Symbols / Icons**: vector, reference by name in code. Use `compose-material-icons` library or the Material Icons font.

### Cross-platform (React Native / Flutter)

**React Native**: Image assets at 1x/2x/3x using suffix convention. Icons typically as SVG via `react-native-svg`. App icon generated from a single high-res source via `react-native-asset` or Expo's asset pipeline.

**Flutter**: Assets declared in `pubspec.yaml`; resolution-aware images use `1.5x/2.0x/3.0x/4.0x` directories. Icons via `flutter_svg` or Material/Cupertino icon sets.

---

## Component spec format

When handing off a component to a developer (or receiving specs from a designer), document each component with:

```
COMPONENT: [Name — e.g., "Primary Button"]
STATE: [default | pressed | disabled | loading]

SIZE:
  - Height: 48pt (iOS) / 48dp (Android)
  - Min width: 120pt
  - Padding: 16pt horizontal, 0pt vertical (height is fixed)
  - Corner radius: 12pt

TYPOGRAPHY:
  - Label: Body Semibold, 16pt, tracking 0
  - Color (default): white (#FFFFFF)
  - Color (disabled): text-secondary token

COLOR:
  - Background (default): primary-500 token (#0A84FF)
  - Background (pressed): primary-600 token
  - Background (disabled): neutral-200 token

ICON (optional):
  - Size: 20×20pt
  - Position: leading, 8pt gap to label
  - Source: SF Symbol "plus" / Material "add"

ACCESSIBILITY:
  - Minimum touch target: 44×44pt (iOS) / 48×48dp (Android) — larger than the visual size; extend hit area
  - accessibilityLabel: "[Button label] button" — set explicitly if icon-only
  - accessibilityTraits: .button (iOS) / Role.Button (Android)

ANIMATION:
  - Press: 0.95 scale, 100ms ease-in-out
  - Disabled: no animation
```

Every component that will be implemented needs a spec. Components without specs produce inconsistent implementations across screens.

---

## Design token vocabulary

Tokens are the named values that the design system uses throughout. Define them once; reference them everywhere.

### Color tokens

```
Structure: [category]-[scale]

Primary:     primary-50 through primary-900 (10 steps)
Neutral:     neutral-50 through neutral-900
Semantic:    error, warning, success, info (+ -light, -dark variants)

Surface:     surface-base, surface-elevated-1, surface-elevated-2, surface-sheet
Text:        text-primary, text-secondary, text-tertiary, text-disabled, text-inverse
Border:      border-default, border-strong, border-subtle
Interactive: interactive-default, interactive-hover, interactive-pressed, interactive-disabled

Dark mode: each token has a light-mode and dark-mode value.
           In Figma: use Color Styles with light/dark modes.
           In code: use semantic color names that resolve to different values in light/dark.
```

### Typography tokens

```
Display:     display-lg, display-md, display-sm   (hero text, marketing)
Heading:     heading-1, heading-2, heading-3       (screen titles, section headers)
Body:        body-lg, body-md, body-sm             (main content)
Label:       label-lg, label-md, label-sm          (buttons, tabs, labels)
Caption:     caption-lg, caption-md               (supporting text, metadata)

Each token defines: font-family, font-size, font-weight, line-height, letter-spacing
```

### Spacing tokens

```
Base unit: 4pt / 4dp

Named scale:
  space-1:  4pt
  space-2:  8pt
  space-3:  12pt
  space-4:  16pt
  space-5:  20pt
  space-6:  24pt
  space-8:  32pt
  space-10: 40pt
  space-12: 48pt
  space-16: 64pt
```

### Radius tokens

```
radius-none:  0pt
radius-sm:    4pt   (inputs, chips)
radius-md:    8pt   (cards, buttons)
radius-lg:    12pt  (primary buttons, sheets)
radius-xl:    16pt  (large cards, modals)
radius-2xl:   24pt  (bottom sheets)
radius-full:  9999pt (pills, avatars, toggles)
```

### Shadow / elevation tokens

```
iOS (using UIKit shadows):
  shadow-sm:  0 1pt 2pt rgba(0,0,0,0.08)
  shadow-md:  0 2pt 8pt rgba(0,0,0,0.12)
  shadow-lg:  0 4pt 16pt rgba(0,0,0,0.16)
  shadow-xl:  0 8pt 32pt rgba(0,0,0,0.20)

Android (Material elevation — surfaces gain lightening in dark mode):
  elevation-1: 1dp
  elevation-2: 3dp
  elevation-3: 6dp
  elevation-4: 8dp
  elevation-5: 12dp
```

---

## Common spec mistakes

- **Designing in pixels, not points.** Pixel values for iOS are meaningless unless you specify the device scale. Always design in points.
- **Ignoring safe areas.** Buttons at the bottom of a screen that don't account for the home indicator are unreachable on modern iPhones.
- **App icon with transparency.** App Store requires a solid background. No alpha channel.
- **App icon with rounded corners applied in design.** iOS applies rounded corners automatically. A design file with rounded corners will double-round on device.
- **Designing touch targets at icon size.** A 24×24pt icon still needs a 44×44pt touch area around it. These are different things.
- **Missing dark mode versions.** Designed in light mode, never tested in dark mode — common and immediately visible to users who use dark mode.
- **Token mismatch between design and code.** Designer uses a color called "Blue" in Figma; developer implements a different hex. Establish named tokens and keep them in sync.
- **Not specifying component states.** Default state designed; pressed, disabled, and loading states not specified. Developers will implement these inconsistently or poorly.
- **Bitmap icons instead of vectors.** Bitmap icons at small sizes degrade. Use SVG/vector for all icons.
