# Newsletter Configuration Examples

This file contains example configurations for different newsletter providers.
Copy the relevant section to your `hugo.toml` file and customize as needed.

## Buttondown (Recommended)

```toml
[params.newsletter]
  enabled = true
  provider = "buttondown"
  title = "Subscribe to our newsletter"
  description = "Get notified when we publish new posts about C++ development in Winnipeg"
  placeholder = "your@email.com"
  buttonText = "Subscribe"
  note = "We respect your privacy. Unsubscribe at any time."
  
  [params.newsletter.buttondown]
    username = "winnipeg-cpp"  # Replace with your Buttondown username
```

## Mailchimp

```toml
[params.newsletter]
  enabled = true
  provider = "mailchimp"
  title = "Join our mailing list"
  description = "Stay updated with C++ meetups and articles"
  placeholder = "Enter your email address"
  buttonText = "Subscribe"
  note = "Your privacy matters. Unsubscribe anytime."
  
  [params.newsletter.mailchimp]
    actionUrl = "https://yourname.us1.list-manage.com/subscribe/post?u=xxx&id=yyy"
    botField = "b_xxx_yyy"
```

## Custom Provider (Substack, ConvertKit, etc.)

```toml
[params.newsletter]
  enabled = true
  provider = "custom"
  title = "Subscribe for updates"
  description = "Get the latest C++ content delivered to your inbox"
  placeholder = "your.email@example.com"
  buttonText = "Sign Up"
  
  [params.newsletter.custom]
    actionUrl = "https://your-service.com/subscribe"
    emailFieldName = "email"
    
    # Optional: Add hidden fields if your service requires them
    [[params.newsletter.custom.hiddenFields]]
      name = "list_id"
      value = "12345"
    [[params.newsletter.custom.hiddenFields]]
      name = "source"
      value = "website"
```

## Minimal Configuration

```toml
[params.newsletter]
  enabled = true
  provider = "buttondown"
  
  [params.newsletter.buttondown]
    username = "your-username"
```

## Customization Options

All text fields are optional and have sensible defaults:

- `title`: Heading above the form (default: none)
- `description`: Description text (default: none)
- `placeholder`: Email input placeholder (default: "Enter your email")
- `buttonText`: Subscribe button text (default: "Subscribe")
- `note`: Small print below the form (default: none)

## Disabling the Newsletter

To disable the newsletter form:

```toml
[params.newsletter]
  enabled = false
```

Or simply comment out the entire `[params.newsletter]` section.
