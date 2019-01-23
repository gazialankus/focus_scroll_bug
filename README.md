# focus_scroll_bug

This demonstrates the bug tha I caught today. Normally, a `TextField` inside a `SingleChildScrollView` scrolls into view when keyboard appears after getting focus. It fails to scroll into view under these conditions: 

- The `TextField` has a `TextEditingController` with an initial value
- The `TextField` has a `FocusNode` that immediately makes a text selection upon focus.

This prevents the caret from ever showing. The scroll-into-view algorithm depends on the caret`s rect. 

I just fixed `flutter/packages/flutter/lib/src/widgets/editable_text.dart` so that it also uses the selection`s rect. I'll send a pull request soon. 
