# Flutter: State Management & Architecture

## 1. Superior State: Riverpod
Always prefer `flutter_riverpod` for scalable apps avoiding passing boilerplate context down huge widget trees.

```dart
// Core rule: Avoid StatefulWidget when Riverpod can abstract the logic.
final counterProvider = StateProvider<int>((ref) => 0);

class CounterScreen extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final count = ref.watch(counterProvider);
    
    return Scaffold(
      body: Center(child: Text('$count')),
      floatingActionButton: FloatingActionButton(
        onPressed: () => ref.read(counterProvider.notifier).state++,
      ),
    );
  }
}
```

## 2. Clean Architecture Folder Structure
Flutter logic must reside outside the UI tree for testability.
*   `lib/`
    *   `src/features/` (Group by feature, not by layer: e.g., `auth`, `products`)
        *   `auth/presentation/` (Widgets, Controllers)
        *   `auth/application/` (Services, Logic)
        *   `auth/domain/` (Models)
        *   `auth/data/` (Repositories, API calls)
    *   `src/common_widgets/` (Reusable UI like specialized Buttons)
    *   `src/routing/` (GoRouter configurations)
    *   `src/theme/` (Colors, Typography matching Theme Vault)

## 3. Performance Strictness
- Heavy lists MUST use `ListView.builder` or `SliverList`. Avoid `SingleChildScrollView` + `Column` if items > 50.
- When creating animations, ALWAYS include `const` constructors on child widgets to prevent the framework from unnecesarily rebuilding complex vector layers inside animated builders.
