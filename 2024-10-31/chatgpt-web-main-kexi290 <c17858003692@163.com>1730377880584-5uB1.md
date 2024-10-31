The changes involve adding new components and functionalities to the application, including:

1. **New Components**: The addition of new components for roles and chat, such as `RoleList`, `RoleDetail`, `DialogHead`, and `RoleContext`. These components are used to display a list of roles, show details for a selected role, and manage chat sessions.

2. **Role Management**: Roles are now defined in a JSON file and fetched via API. The `RoleList` component displays a list of roles, and clicking on a role navigates to a `RoleDetail` page for that role. This detail page includes a button to start a new chat session with that role.

3. **Chat Enhancements**: The `ChatStore` has been updated to manage chat sessions, including opening new sessions, sending messages, and deleting sessions. The `DialogHead` component has been added to allow adding new chat sessions.

4. **Routing Improvements**: New routes have been added for roles and chat, allowing for navigation between different role details and chat sessions.

5. **Styling and Layout**: New SCSS files have been added for styling components like `RoleList`, `RoleDetail`, and `DialogHead`.

6. **API Integration**: An API has been set up to fetch role data, although it is currently being mocked.

In summary, the changes focus on adding role-based chat functionality to the application, allowing users to select a role and have a conversation with it. The changes include new components, routing, state management, and styling.