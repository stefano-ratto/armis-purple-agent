### 6. HTML Entity Encoding in Passwords
**Observation**: Passwords retrieved from APIs or databases might contain HTML entities (e.g., `&#2a` for `*`).
**Tactic**: If a password retrieved from a JSON response or HTML page fails to work, check for HTML entities and decode them (e.g., `&amp;` -> `&`, `&#2a` -> `*`) before using them in login forms.

### 7. Privileged Action Exploitation
**Observation**: Administrative or privileged actions (like deleting a case) might be available to specific users but hidden from the UI until logged in as that user.
**Tactic**: Once a privileged account is compromised (e.g., via IDOR-leaked credentials), explore all available dashboards and menus for new functionality that was previously inaccessible. Look for buttons, forms, or API calls that perform state-changing actions.