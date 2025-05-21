# Webflow to Calendly Integration

A lightweight JavaScript solution that automatically redirects users to Calendly after submitting any Webflow form. The script intelligently detects form fields (email, name, message) and passes them to your Calendly booking page.

## Features

- 🔄 **Centralized Integration**: Works with all forms on your Webflow site automatically
- 🔍 **Smart Field Detection**: Automatically identifies email, name, and message fields
- ⚙️ **Simple Configuration**: One-time setup with minimal configuration
- 🚫 **Selective Integration**: Easily exclude specific forms if needed
- 🚀 **Lightweight**: Minified version under 2KB

## Prerequisites

Before you begin, ensure you have the following:

*   A **Webflow account** with an active website.
*   A **Calendly account** where you want to direct users.

## Installation

Add the following script to your Webflow site's custom code section (Site Settings → Custom Code → Footer):

```html
<script src="https://cdn.jsdelivr.net/gh/amit-wisemonk/webflow-calendly-integration@main/calendly-integration.min.js"></script>
```

For better cache control and version management, use:

```html
<script src="https://cdn.jsdelivr.net/gh/amit-wisemonk/webflow-calendly-integration@main/calendly-integration.min.js?v=1.0.0"></script>
```

Using a versioned link (e.g., `?v=1.0.0`) is recommended as it helps ensure that updates to the script are picked up by browsers, bypassing cached older versions.

## Configuration

The script has three main configuration variables at the top of the file:

```javascript
// CONFIGURATION - Edit these values
const CALENDLY_URL = "https://calendly.com/fiza-wisemonk/wisemonk";
const DEBUG = false;
const EXCLUDE_FORM_ATTRIBUTE = "data-no-calendly";
```

### CALENDLY_URL (Required)

Change this to your Calendly booking link.

Example:
```javascript
const CALENDLY_URL = "https://calendly.com/your-username/your-event-type";
```

### DEBUG (Optional)

Set to `true` to enable console logging for troubleshooting.

```javascript
const DEBUG = true; // Set to true to see debugging info in the console
```

### EXCLUDE_FORM_ATTRIBUTE (Optional)

The attribute used to exclude forms from the Calendly redirection.

Default:
```javascript
const EXCLUDE_FORM_ATTRIBUTE = "data-no-calendly";
```

## How It Works

The script:

1. Automatically detects all forms on your Webflow site
2. Listens for form submissions.
   - A 500ms delay is introduced after submission to allow Webflow's native form handling to complete before redirection.
3. Intelligently identifies common form fields:
   - Email field (required for redirection to work)
   - Name field (optional)
   - Message field (optional, passed as the first custom question)
4. Redirects to your Calendly URL, pre-filling standard fields (name, email) and passing the message content as a custom answer (specifically as the `a1` parameter).

## Excluding Specific Forms

If you have forms that should NOT redirect to Calendly, add this custom attribute:

```html
<form data-no-calendly="true">
  <!-- Form contents -->
</form>
```

In Webflow:
1. Select the form element
2. In the Settings panel, go to the Custom Attributes section
3. Add `data-no-calendly` as the name and `true` as the value

## Setting Up Calendly Custom Questions

To receive the message field as a custom question in Calendly:

1. Log in to your Calendly account
2. Go to Event Types → Select your event
3. Go to "Invitee Questions"
4. Add a custom question (the script sends the message as `a1` parameter).
   - For best results, set the question type to "Text (multiple lines)".
   - You can title this question something like "Your Message" or "Additional Details".

## Field Detection

The script automatically detects:

- **Email fields**: By input type, name, id, or placeholder text containing "email"
- **Name fields**: By input name, id, or placeholder text containing "name". The script specifically excludes terms like "lastname", "surname", or "company name" to target the primary contact name (e.g., first name or full name).
- **Message fields**: By textarea elements or inputs with name/id/placeholder containing "message" or "comment"

## Troubleshooting

### Redirection Not Working

- Check if your form has at least one email field
- Ensure your Calendly URL is correct in the configuration
- Set `DEBUG = true` to see detailed logs in the browser console

### Forms Being Incorrectly Redirected

- Add the `data-no-calendly="true"` attribute to exclude specific forms

### Incorrect Field Detection

- The script tries to detect fields automatically, but if it's not working as expected, you may need to ensure your form fields have appropriate names, IDs, or placeholders.

## Limitations

*   **JavaScript Dependent:** The integration relies on client-side JavaScript. If a user has JavaScript disabled in their browser, the redirection to Calendly will not occur.
*   **Standard Form Structures:** The script is designed for forms with common field naming conventions (e.g., input fields with `name`, `id`, or `placeholder` attributes like 'email', 'name'). Highly customized or complex form structures might require modifications to the script's field detection logic.
*   **Submission Timing:** The 500ms delay before redirection is generally sufficient for Webflow's native form processing. However, for forms with very heavy client-side processing or slow third-party script interactions, this delay might occasionally be too short, potentially interrupting the original form submission.
*   **No Server-Side Fallback:** This is a purely client-side integration. There's no server-side mechanism to ensure the Calendly redirection if the client-side script fails.

## Advanced Customization

If you need more control, you can fork this repository and modify the field detection logic or add additional parameters to Calendly.

## Contributing

Contributions are welcome! If you have suggestions for improvements, new features, or find bugs, please feel free to:

1.  Fork the repository.
2.  Create a new branch for your changes.
3.  Make your modifications.
4.  Submit a pull request with a clear description of your changes.

Alternatively, you can also open an issue to discuss potential changes or report problems.

## Security and Privacy

*   **Client-Side Processing:** This script operates entirely on the client-side (in the user's browser). It reads form data locally and redirects the user to Calendly.
*   **No Data Storage:** The script itself does not store any form data. Data is passed directly to Calendly's secure booking page.
*   **Calendly's Policies:** Once redirected, data handling is subject to Calendly's privacy policy and security measures.

## License

MIT License - Feel free to use and modify for your projects.
