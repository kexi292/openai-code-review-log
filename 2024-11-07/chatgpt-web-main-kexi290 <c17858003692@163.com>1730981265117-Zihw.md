Here's an overview of the changes made in the provided code:

1. **.gitignore**: Added `.venv` and `.env` to ignore virtual environment and environment variables.

2. **src/apis/index.tsx**: Added new `completions` API for fetching chat completions.

3. **src/app/components/dialog/dialog-message-actions.tsx**: Refactored the Action component into a more generic ChatAction component that can display both text and icon.

4. **src/app/components/dialog/dialog-message-item.tsx**: Added date display, copy, retry, and delete actions for messages.

5. **src/app/components/dialog/dialog-message.tsx**: Removed local state and directly used store state. Also, changed the way new messages are created.

6. **src/app/components/markdown/markdown.tsx**: Updated the loading icon.

7. **src/app/components/role/role-detail.tsx**: Changed the way new messages are created.

8. **src/app/icons/three_dot.svg**: Added a new loading icon.

9. **src/app/store/chat-store.ts**: Major refactoring to add streaming support for chat completions.

10. **src/app/styles/globals.scss**: Added new SCSS files for syntax highlighting and markdown styling.

11. **src/app/styles/highlight.scss**: New SCSS file for syntax highlighting.

12. **src/app/styles/markdown.scss**: New SCSS file for markdown styling.

13. **src/types/chat.ts**: Added `id` and `streaming` fields to the Message interface.

14. **src/utils/index.ts**: New utility functions for copying to clipboard and formatting objects as pretty-printed JSON.

The main focus of these changes was to add streaming support for chat completions, refactor components, and add new utility functions. The addition of new SCSS files will help improve the styling of markdown and code blocks.