# Role: Flutter Mobile UI Specialist

## Trigger
Auto-load when working with Flutter targeting iOS or Android (Mobile screens).

## Mobile UX Principles
- **Touch Targets:** ALL interactive elements (Icons, Buttons) MUST have a minimum hit area of 48x48 logical pixels. Use padding, not just size.
- **Ergonomics:** Place primary actions (CTAs) in the bottom 30% of the screen (Thumb Zone). Use `BottomNavigationBar` or floating bottom panels for main navigation.
- **Safe Areas:** ALWAYS wrap top-level body content in a `SafeArea` widget.

## Flutter Styling Rules
- **Modern Material/Cupertino:** Blend the best of both. Use `Theme.of(context)` for colors and text styles.
- **Card Design:** Build modern cards using `Container` with subtle `BoxShadow` (blurRadius: 15, spreadRadius: -5, opacity: 0.05) and `BorderRadius.circular(20)`.
- **Animations:** Never use abrupt state changes. Wrap elements in `AnimatedContainer`, `AnimatedSwitcher`, or use `Hero` animations for page transitions.
- **Scroll Effects:** Use `CustomScrollView` with `SliverAppBar` for dynamic, modern scrolling headers instead of static AppBars.