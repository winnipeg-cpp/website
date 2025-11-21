# Newsletter Subscription Setup Guide

This guide explains how to set up email newsletter subscriptions for the Winnipeg C++ Developers website.

## Overview

The website includes a flexible newsletter subscription form that works with static Hugo sites. The form appears at the bottom of blog posts and can be configured to work with various email service providers.

## Supported Providers

The subscription form supports three types of providers:

1. **Buttondown** - Privacy-focused, simple, free for up to 100 subscribers
2. **Mailchimp** - Popular email marketing service with extensive features
3. **Custom** - Any other service with a form endpoint

## Quick Start with Buttondown (Recommended)

Buttondown is recommended for its simplicity and privacy focus. Here's how to set it up:

### Step 1: Create a Buttondown Account

1. Go to [buttondown.email](https://buttondown.email)
2. Sign up for a free account
3. Choose your newsletter username (e.g., `winnipeg-cpp`)

### Step 2: Configure Hugo

Add the following to your `hugo.toml` file:

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

### Step 3: Configure Buttondown to Send Emails

1. Log in to your Buttondown dashboard
2. Go to **Settings** → **Basics**
3. Add your newsletter RSS feed URL: `https://winnipeg-cpp.github.io/website/index.xml`
4. Enable **"Send an email when new items appear in RSS feed"**
5. Customize your email template as desired

### Step 4: Test the Subscription

1. Build and preview your site: `hugo server -D`
2. Navigate to any blog post
3. You should see the subscription form at the bottom
4. Test subscribing with your email
5. Check that you receive a confirmation email from Buttondown

## Alternative: Mailchimp Setup

If you prefer Mailchimp:

### Step 1: Get Your Mailchimp Form URL

1. Log in to Mailchimp
2. Go to **Audience** → **Signup forms** → **Embedded forms**
3. Copy the form action URL (looks like: `https://yourname.us1.list-manage.com/subscribe/post?u=xxx&id=yyy`)

### Step 2: Configure Hugo

```toml
[params.newsletter]
  enabled = true
  provider = "mailchimp"
  title = "Subscribe to our newsletter"
  description = "Get notified about new C++ meetups and articles"
  placeholder = "your@email.com"
  buttonText = "Subscribe"
  
  [params.newsletter.mailchimp]
    actionUrl = "https://yourname.us1.list-manage.com/subscribe/post?u=xxx&id=yyy"
    botField = "b_xxx_yyy"  # Bot protection field name from Mailchimp
```

### Step 3: Set Up RSS-to-Email in Mailchimp

1. In Mailchimp, go to **Campaigns** → **Email**
2. Create a new **RSS Campaign**
3. Add your RSS feed: `https://winnipeg-cpp.github.io/website/index.xml`
4. Configure when and how often to send (e.g., daily, weekly)
5. Design your email template

## Alternative: Custom Service

For other email services (Substack, ConvertKit, etc.):

```toml
[params.newsletter]
  enabled = true
  provider = "custom"
  title = "Subscribe to our newsletter"
  description = "Stay updated with new posts"
  
  [params.newsletter.custom]
    actionUrl = "https://your-service.com/subscribe"
    emailFieldName = "email"  # The name attribute for the email input
    
    # Optional: Add hidden fields required by your service
    [[params.newsletter.custom.hiddenFields]]
      name = "list_id"
      value = "12345"
    [[params.newsletter.custom.hiddenFields]]
      name = "source"
      value = "website"
```

## Privacy and Security

### Email List Privacy

- **Hidden by default**: Email addresses are stored securely by your chosen provider and are never exposed publicly
- **No emails in repository**: The subscription form only sends data to the external service; no emails are stored in the GitHub repository
- **Subscriber control**: All recommended services (Buttondown, Mailchimp) include unsubscribe links in every email

### Best Practices

1. **Privacy Policy**: Add a privacy policy link to your website explaining how subscriber data is used
2. **GDPR Compliance**: Both Buttondown and Mailchimp are GDPR-compliant
3. **Double Opt-in**: Enable double opt-in in your service settings to confirm subscriptions
4. **Unsubscribe**: Always include an easy way for subscribers to unsubscribe

## Customization

### Form Placement

The subscription form appears at the bottom of all blog posts by default. To customize:

Edit `layouts/partials/extend_footer.html`:

```html
{{- /* Show on all pages */ -}}
{{- partial "subscribe_form.html" . }}

{{- /* Show only on home page */ -}}
{{- if .IsHome }}
  {{- partial "subscribe_form.html" . }}
{{- end }}

{{- /* Show on posts with specific tag */ -}}
{{- if in .Params.tags "meetup" }}
  {{- partial "subscribe_form.html" . }}
{{- end }}
```

### Styling

The form uses CSS variables from the PaperMod theme and adapts to light/dark mode automatically. To customize styles, add CSS to `layouts/partials/extend_head.html`:

```html
<style>
.newsletter-subscribe {
  /* Your custom styles */
}
</style>
```

## Disabling the Newsletter Form

To temporarily disable the form:

```toml
[params.newsletter]
  enabled = false
```

## Testing

### Local Testing

```bash
# Preview with drafts
hugo server -D

# Build production version
hugo --gc --minify
```

### Checklist

- [ ] Form appears on blog posts
- [ ] Form styling matches site theme (light/dark mode)
- [ ] Email validation works
- [ ] Submission redirects properly
- [ ] Confirmation email is received
- [ ] Unsubscribe link works
- [ ] Mobile layout is responsive

## Sending Emails for New Posts

Once subscribers are in your list:

### With Buttondown

1. Buttondown will automatically detect new posts via RSS
2. It will send an email to all subscribers
3. You can customize the email template in Buttondown settings

### With Mailchimp

1. Set up an RSS-to-Email campaign
2. Configure the frequency (e.g., send when new posts are published)
3. Customize the email design

### Manual Sending

All services also allow you to manually compose and send emails to your list.

## Troubleshooting

### Form Not Appearing

- Check `hugo.toml` has `enabled = true`
- Verify you're viewing a blog post (not the home page)
- Check browser console for JavaScript errors

### Submissions Not Working

- Verify the action URL is correct
- Check that the email field name matches your provider
- Test in an incognito window (browser extensions may interfere)

### Emails Not Sending

- Verify RSS feed is accessible: `https://winnipeg-cpp.github.io/website/index.xml`
- Check RSS-to-Email settings in your provider dashboard
- Some services have delays; wait 15-30 minutes after publishing

## Resources

- [Buttondown Documentation](https://docs.buttondown.email/)
- [Mailchimp RSS Campaigns](https://mailchimp.com/help/share-your-blog-posts-with-mailchimp/)
- [Hugo Configuration](https://gohugo.io/getting-started/configuration/)

## Support

If you encounter issues:

1. Check this documentation
2. Review your provider's documentation
3. Open an issue on the [website repository](https://github.com/winnipeg-cpp/website/issues)
