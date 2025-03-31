# Webflow to Calendly Integration

A lightweight JavaScript solution that automatically redirects users to Calendly after submitting any Webflow form. The script intelligently detects form fields (email, name, message) and passes them to your Calendly booking page.

## Features

- 🔄 **Centralized Integration**: Works with all forms on your Webflow site automatically
- 🔍 **Smart Field Detection**: Automatically identifies email, name, and message fields
- ⚙️ **Simple Configuration**: One-time setup with minimal configuration
- 🚫 **Selective Integration**: Easily exclude specific forms if needed
- 🚀 **Lightweight**: Minified version under 2KB

## Installation

Add the following script to your Webflow site's custom code section (Site Settings → Custom Code → Footer):

```html
<script src="https://cdn.jsdelivr.net/gh/amit-wisemonk/webflow-calendly-integration@main/calendly-integration.min.js"></script>
```

For better cache control and version management, use:

```html
<script src="https://cdn.jsdelivr.net/gh/amit-wisemonk/webflow-calendly-integration@main/calendly-integration.min.js?v=1.0.0"></script>
```

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
2. Listens for form submissions
3. Intelligently identifies common form fields:
   - Email field (required for redirection to work)
   - Name field (optional)
   - Message field (optional, passed as the first custom question)
4. Redirects to your Calendly URL with all data pre-filled

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
4. Add a custom question (the script sends the message as `a1` parameter)

## Field Detection

The script automatically detects:

- **Email fields**: By input type, name, id, or placeholder text containing "email"
- **Name fields**: By input name, id, or placeholder text containing "name" (excluding "lastname" and "company name")
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

## Advanced Customization

If you need more control, you can fork this repository and modify the field detection logic or add additional parameters to Calendly.

## License

MIT License - Feel free to use and modify for your projects.

---

Created and maintained by [Wisemonk](https://wisemonk.co/)
