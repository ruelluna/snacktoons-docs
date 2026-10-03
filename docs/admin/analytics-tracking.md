# Analytics & Tracking Settings

## Overview

The Analytics & Tracking system provides comprehensive tracking capabilities across the entire application. It includes global tracking settings in the General Settings panel, as well as granular tracking options for individual comics and chapters. This system allows administrators to implement various analytics platforms and track user behavior at multiple levels.

## View history (reading activity)

Use **Analytics → View history** in the admin panel to review chapter reads across all readers.

- Filter by **last read date range** or **comic**
- Search by reader email or session
- **Export reading history** to CSV for reporting (reader, comic, chapter, progress, IP, timestamps)

Per-reader history remains available on **Users → Readers → [reader] → Reading history**.

## General Settings Analytics Tab

### Accessing Analytics Settings

Open **Settings → General Settings**. The page opens as a **read-only view** of SEO, analytics, payouts, and the other setting groups. Click **Edit** to change values. Saving one tab (for example SEO or Analytics) does not require you to fill the other tabs — empty payout and economy fields keep their defaults.

After you save, you return to the view so you can confirm what is stored before editing again.

### Opening the Analytics group

On the edit form, open the **Analytics** tab to configure global tracking settings that apply across the entire application.

### Available Tracking Options

#### 1. Google Analytics ID
- **Field**: `google_analytics_id`
- **Format**: `G-XXXXXXXXXX` (Google Analytics 4 Measurement ID)
- **Purpose**: Enables Google Analytics tracking across all pages
- **Implementation**: Automatically loads Google Analytics 4 tracking code

**Example:**
```
G-ABC123DEF4
```

#### 2. Meta Pixel ID
- **Field**: `meta_pixel_id`
- **Format**: `123456789012345` (Facebook Meta Pixel ID)
- **Purpose**: Enables Facebook/Meta advertising tracking
- **Implementation**: Automatically loads Meta Pixel tracking code

**Example:**
```
123456789012345
```

#### 2b. Google Tag Manager Container ID
- **Field**: Google Tag Manager Container ID
- **Format**: `GTM-XXXXXXX`
- **Purpose**: Loads the official GTM snippet in the page head (and the noscript iframe after the body opens)
- **Notes**: Leave empty if you only need the GA4 Measurement ID above. You can use both: GTM for tags, GA4 for the built-in gtag snippet.

#### 2c. Meta Conversions API
- **Access token**: Server-side token from Meta Events Manager. The site never shows this value in logs or public pages.
- **Test event code**: Optional. Use while checking Test Events in Meta; clear it for production.
- **What is sent**: Registration as CompleteRegistration; subscription, chapter unlock, and coin package checkout as Purchase. The same `event_id` is pushed to `dataLayer` so GTM and CAPI can dedupe.

## SEO tab

Open **Settings → General Settings → Edit → SEO** to set the homepage document title, keywords, and extra metadata. The SEO title becomes the public `<title>` on the home page. Comic, chapter, and account pages still use their own titles. This is a single-domain site; change the public URL in application config, not by adding extra domains here.

#### 3. PostHog HTML Snippet
- **Field**: `posthog_html_snippet`
- **Format**: Complete PostHog initialization script
- **Purpose**: Enables PostHog analytics and product analytics
- **Implementation**: Injects PostHog script directly into page head

**Example:**
```html
<script>
  !function(t,e){var o,n,p,r;e.__SV||(window.posthog=e,e._i=[],e.init=function(i,s,a){function g(t,e){var o=e.split(".");2==o.length&&(t=t[o[0]],e=o[1]),t[e]=function(){t.push([e].concat(Array.prototype.slice.call(arguments,0)))}}(p=t.createElement("script")).type="text/javascript",p.async=!0,p.src=s.api_host+"/static/array.js",(r=t.getElementsByTagName("script")[0]).parentNode.insertBefore(p,r);var u=e;for(void 0!==a?u=e[a]=[]:a="posthog",u.people=u.people||[],u.toString=function(t){var e="posthog";return"posthog"!==a&&(e+="."+a),t||(e+=" (stub)"),e},u.people.toString=function(){return u.toString(1)+".people (stub)"},o="capture identify alias people.set people.set_once set_config register register_once unregister opt_out_capturing has_opted_out_capturing opt_in_capturing reset isFeatureEnabled onFeatureFlags getFeatureFlag getFeatureFlagPayload reloadFeatureFlags group updateEarlyAccessFeatureEnrollment getEarlyAccessFeatures getActiveMatchingSurveys getSurveys".split(" "),n=0;n<o.length;n++)g(u,o[n]);e._i.push([i,s,a])},e.__SV=1)}(document,window.posthog||[]);
  posthog.init('YOUR_API_KEY', {api_host: 'https://app.posthog.com'})
</script>
```

#### 4. Custom Tracking Scripts
- **Field**: `custom_tracking_scripts`
- **Format**: Any HTML/JavaScript tracking code
- **Purpose**: Load custom tracking scripts on all public pages
- **Implementation**: Injected into page head on all public pages

**Example:**
```html
<!-- Hotjar Tracking Code -->
<script>
  (function(h,o,t,j,a,r){
    h.hj=h.hj||function(){(h.hj.q=h.hj.q||[]).push(arguments)};
    h._hjSettings={hjid:1234567,hjsv:6};
    a=o.getElementsByTagName('head')[0];
    r=o.createElement('script');r.async=1;
    r.src=t+h._hjSettings.hjid+j+h._hjSettings.hjsv;
    a.appendChild(r);
  })(window,document,'https://static.hotjar.com/c/hotjar-','.js?sv=');
</script>

<!-- Mixpanel Tracking -->
<script>
  (function(f,b){if(!b.__SV){var e,g,i,h;window.mixpanel=b;b._i=[];b.init=function(e,f,c){function g(a,d){var b=d.split(".");2==b.length&&(a=a[b[0]],d=b[1]);a[d]=function(){a.push([d].concat(Array.prototype.slice.call(arguments,0)))}}var a=b;"undefined"!==typeof c?a=b[c]=[]:c="mixpanel";a.people=a.people||[];a.toString=function(a){var d="mixpanel";"mixpanel"!==c&&(d+="."+c);a||(d+=" (stub)");return d};a.people.toString=function(){return a.toString(1)+".people (stub)"};i="disable time_event track track_pageview track_links track_forms track_with_groups add_group set_group remove_group register register_once alias unregister identify name_tag set_config reset opt_in_tracking has_opted_in_tracking opt_out_tracking has_opted_out_tracking clear_opt_in_out_tracking start_batch_senders people.set people.set_once people.unset people.increment people.append people.union people.track_charge people.clear_charges people.delete_user people.remove".split(" ");
  for(h=0;h<i.length;h++)g(a,i[h]);var j="set set_once union unset remove delete".split(" ");a.get_group=function(){function b(c){d[c]=function(){call2_args=arguments;call2=[c].concat(Array.prototype.slice.call(call2_args,0));a.push([e,call2])}}var d={},e=["get_group"].concat(Array.prototype.slice.call(arguments,0));for(var c=0;c<j.length;c++)b(j[c]);return d};b._i.push([e,f,c])};b.__SV=1.2;e=f.createElement("script");e.type="text/javascript";e.async=!0;e.src="undefined"!==typeof MIXPANEL_CUSTOM_LIB_URL?
  MIXPANEL_CUSTOM_LIB_URL:"file:"===f.location.protocol&&"//cdn.mxpnl.com/libs/mixpanel-2-latest.min.js".match(/^\/\//)?"https://cdn.mxpnl.com/libs/mixpanel-2-latest.min.js":"//cdn.mxpnl.com/libs/mixpanel-2-latest.min.js";g=f.getElementsByTagName("script")[0];g.parentNode.insertBefore(e,g)}})(document,window.mixpanel||[]);
  mixpanel.init("YOUR_TOKEN");
</script>
```

#### 5. Purchase Conversion Tracking Scripts
- **Field**: `purchase_tracking_scripts`
- **Format**: Conversion tracking scripts
- **Purpose**: Load conversion tracking on successful purchase pages
- **Implementation**: Only loads on pages with routes containing "successful"

**Example:**
```html
<!-- Google Ads Conversion Tracking -->
<script>
  gtag('event', 'conversion', {
    'send_to': 'AW-CONVERSION_ID/CONVERSION_LABEL',
    'value': 1.0,
    'currency': 'USD'
  });
</script>

<!-- Facebook Conversion API -->
<script>
  fbq('track', 'Purchase', {
    value: 29.99,
    currency: 'USD'
  });
</script>
```

### Helper Functions

The system provides several helper functions to access tracking settings:

#### Global Tracking Helpers
```php
// Check if any tracking is enabled
has_tracking_enabled()

// Get specific tracking settings
google_analytics_id()
meta_pixel_id()
gtm_container_id()
posthog_html_snippet()
custom_tracking_scripts()
purchase_tracking_scripts()

// Get all tracking settings
tracking_settings()
```

#### Comic/Chapter Tracking Helpers
```php
// Get tracking scripts for specific comic
comic_tracking_scripts($comicId)

// Get tracking scripts for specific chapter
chapter_tracking_scripts($chapterId)
```

## Comic-Specific Tracking

### Overview

Each comic can have its own custom tracking scripts that load only when users view that specific comic. This allows for targeted advertising and analytics for individual comics.

### Configuration

#### Accessing Comic Tracking Settings

1. Navigate to **Admin Panel > Comics**
2. Select a comic to edit
3. Go to the **Tracking & Analytics** section
4. Add custom tracking scripts

#### Implementation Details

- **Field**: `tracking_scripts` in the Comic model
- **Loading**: Scripts load when users visit the comic page
- **Scope**: Only affects the specific comic
- **Execution**: Scripts are injected into the page head

### Use Cases

#### Comic-Specific Advertising
```html
<!-- Target ads for specific comic genre -->
<script>
  gtag('config', 'G-XXXXXXXXXX', {
    'custom_map': {
      'comic_title': '{{ $comic->title }}',
      'comic_genre': '{{ $comic->genre }}'
    }
  });
</script>
```

#### Affiliate Tracking
```html
<!-- Track affiliate clicks for specific comic -->
<script>
  (function(e,t,n,r,i,s,o,u,a,f,c){e[r]=e[r]||function(){(e[r].q=e[r].q||[]).push(arguments)},s=t.createElement(n),o=t.getElementsByTagName(n)[0],s.async=1,s.src=i,s.charset="utf-8",o.parentNode.insertBefore(s,o),u=t.createElement(n),c=t.getElementsByTagName(n)[0],u.async=1,u.src=f,u.charset="utf-8",c.parentNode.insertBefore(u,c)})(window,document,"script","_euc","//cdn.eulerian.net/js/eu.js","//cdn.eulerian.net/js/eu.js");
  _euc.push(["ea", "YOUR_SITE_ID", "comic_view", {
    "comic_id": "{{ $comic->id }}",
    "comic_title": "{{ $comic->title }}"
  }]);
</script>
```

#### Custom Analytics Events
```html
<!-- Track comic-specific user behavior -->
<script>
  mixpanel.track('Comic Viewed', {
    'comic_id': '{{ $comic->id }}',
    'comic_title': '{{ $comic->title }}',
    'comic_category': '{{ $comic->category }}',
    'total_chapters': {{ $comic->chapters->count() }}
  });
</script>
```

## Chapter-Specific Tracking

### Overview

Individual chapters can have custom tracking scripts that load when users complete reading that specific chapter. This is perfect for chapter-specific promotions or conversion tracking.

### Configuration

#### Accessing Chapter Tracking Settings

1. Navigate to **Admin Panel > Chapters**
2. Select a chapter to edit
3. Go to the **Tracking & Analytics** section
4. Add custom tracking scripts

#### Implementation Details

- **Field**: `tracking_scripts` in the Chapter model
- **Loading**: Scripts load when users complete reading the chapter
- **Scope**: Only affects the specific chapter
- **Execution**: Scripts are injected into the page head

### Use Cases

#### Chapter Completion Tracking
```html
<!-- Track chapter completion for analytics -->
<script>
  gtag('event', 'chapter_completed', {
    'comic_title': '{{ $comic->title }}',
    'chapter_title': '{{ $chapter->title }}',
    'chapter_number': {{ $chapter->chapter_number }},
    'is_free': {{ $chapter->is_free ? 'true' : 'false' }}
  });
</script>
```

#### Chapter-Specific Promotions
```html
<!-- Show promotion after chapter completion -->
<script>
  fbq('track', 'ViewContent', {
    content_name: '{{ $comic->title }} - {{ $chapter->title }}',
    content_category: 'comic_chapter',
    content_type: 'chapter',
    value: {{ $chapter->is_free ? 0 : $chapter->coin_price }},
    currency: 'USD'
  });
</script>
```

#### Conversion Tracking
```html
<!-- Track conversions for premium chapters -->
<script>
  if (!{{ $chapter->is_free ? 'true' : 'false' }}) {
    gtag('event', 'purchase', {
      'transaction_id': 'chapter_{{ $chapter->id }}',
      'value': {{ $chapter->coin_price }},
      'currency': 'USD',
      'items': [{
        'item_id': '{{ $chapter->id }}',
        'item_name': '{{ $comic->title }} - {{ $chapter->title }}',
        'item_category': 'comic_chapter',
        'price': {{ $chapter->coin_price }},
        'quantity': 1
      }]
    });
  }
</script>
```

## Frontend Implementation

### Global Tracking Loading

Tracking scripts are loaded in the main application layout (`resources/views/app.blade.php`):

```php
<!-- Google Analytics -->
@if (google_analytics_id())
    <script async src="https://www.googletagmanager.com/gtag/js?id={{ google_analytics_id() }}"></script>
    <script>
        window.dataLayer = window.dataLayer || [];
        function gtag(){dataLayer.push(arguments);}
        gtag('js', new Date());
        gtag('config', '{{ google_analytics_id() }}');
    </script>
@endif

<!-- Meta Pixel -->
@if (meta_pixel_id())
    <script>
        !function(f,b,e,v,n,t,s) {
            // Meta Pixel implementation
        }(window, document, 'script', 'https://connect.facebook.net/en_US/fbevents.js');
        fbq('init', '{{ meta_pixel_id() }}');
        fbq('track', 'PageView');
    </script>
@endif

<!-- PostHog Analytics -->
@if (posthog_html_snippet())
    {!! posthog_html_snippet() !!}
@endif

<!-- Custom Tracking Scripts -->
@if (custom_tracking_scripts())
    {!! custom_tracking_scripts() !!}
@endif

<!-- Purchase Conversion Tracking Scripts -->
@if (purchase_tracking_scripts() && (request()->routeIs('*.successful*') || request()->routeIs('*.successful-*')))
    {!! purchase_tracking_scripts() !!}
@endif
```

### Comic-Specific Tracking Loading

Comic tracking scripts are loaded in the comic view component (`resources/js/Pages/Comic/Show.vue`):

```javascript
// Load comic-specific tracking scripts
const loadComicTrackingScripts = () => {
  if (props.comic.tracking_scripts) {
    // Create a script element and inject the tracking scripts
    const scriptElement = document.createElement('div');
    scriptElement.innerHTML = props.comic.tracking_scripts;
    document.head.appendChild(scriptElement);

    // Also execute any script tags that might be in the tracking scripts
    const scripts = scriptElement.querySelectorAll('script');
    scripts.forEach(script => {
      const newScript = document.createElement('script');
      if (script.src) {
        newScript.src = script.src;
      } else {
        newScript.textContent = script.textContent;
      }
      document.head.appendChild(newScript);
    });
  }
}
```

### Chapter-Specific Tracking Loading

Chapter tracking scripts are loaded in the chapter view component (`resources/js/Pages/Comic/Chapter/Show.vue`):

```javascript
// Load chapter-specific tracking scripts
const loadChapterTrackingScripts = () => {
  if (props.chapter.tracking_scripts) {
    // Create a script element and inject the tracking scripts
    const scriptElement = document.createElement('div');
    scriptElement.innerHTML = props.chapter.tracking_scripts;
    document.head.appendChild(scriptElement);

    // Also execute any script tags that might be in the tracking scripts
    const scripts = scriptElement.querySelectorAll('script');
    scripts.forEach(script => {
      const newScript = document.createElement('script');
      if (script.src) {
        newScript.src = script.src;
      } else {
        newScript.textContent = script.textContent;
      }
      document.head.appendChild(newScript);
    });
  }
}
```

## Event Tracking

### Built-in Events

The system automatically tracks various events:

#### Page View Events
- **Comic Page Views**: Tracked when users visit comic pages
- **Chapter Page Views**: Tracked when users visit chapter pages
- **Custom Page Views**: Enhanced with comic/chapter metadata

#### User Interaction Events
- **Chapter Reading**: Tracked when users complete reading chapters
- **Comic Favoriting**: Tracked when users favorite/unfavorite comics
- **Chapter Purchases**: Tracked when users purchase premium chapters
- **Chapter Navigation**: Tracked when users navigate between chapters

#### Conversion Events
- **Subscription Purchases**: Tracked on successful subscription pages
- **Coin Purchases**: Tracked on successful coin purchase pages
- **Cart Purchases**: Tracked on successful cart checkout pages

### Custom Event Examples

#### Google Analytics Events
```javascript
// Track comic page view
gtag('event', 'page_view', {
  page_title: comic.title,
  page_location: window.location.href,
  custom_map: {
    'comic_title': comic.title,
    'comic_category': comic.categories?.map(c => c.name).join(', '),
    'comic_status': comic.status,
    'total_chapters': comic.chapters?.length || 0
  }
});

// Track chapter completion
gtag('event', 'chapter_read', {
  'comic_title': comic.title,
  'chapter_title': chapter.title,
  'chapter_number': chapter.chapter_number,
  'is_free': chapter.is_free,
  'user_type': auth.user ? 'authenticated' : 'anonymous'
});
```

#### Meta Pixel Events
```javascript
// Track content view
fbq('track', 'ViewContent', {
  content_name: comic.title,
  content_category: 'comic',
  content_type: 'comic',
  value: comic.price || 0,
  currency: 'USD'
});

// Track purchase
fbq('track', 'Purchase', {
  content_name: `${comic.title} - ${chapter.title}`,
  content_category: 'comic_chapter',
  value: chapter.coin_price || 0,
  currency: 'USD'
});
```

## Best Practices

### Performance Optimization
- **Script Loading**: Use async/defer attributes for external scripts
- **Minification**: Minify custom tracking scripts
- **Conditional Loading**: Only load scripts when needed
- **Error Handling**: Implement proper error handling for tracking failures

### Privacy Compliance
- **GDPR Compliance**: Ensure tracking scripts respect user privacy
- **Cookie Consent**: Implement cookie consent for tracking scripts
- **Data Minimization**: Only collect necessary data
- **User Control**: Provide options to opt-out of tracking

### Security Considerations
- **Script Validation**: Validate custom tracking scripts
- **CSP Headers**: Implement Content Security Policy
- **HTTPS**: Use HTTPS for all tracking endpoints
- **Input Sanitization**: Sanitize user inputs in tracking data

### Testing and Validation
- **Test Scripts**: Test tracking scripts in development environment
- **Validation Tools**: Use browser developer tools to validate tracking
- **Analytics Verification**: Verify events in analytics dashboards
- **Cross-browser Testing**: Test tracking across different browsers

## Troubleshooting

### Common Issues

#### Scripts Not Loading
1. **Check Settings**: Verify tracking settings are saved correctly
2. **Clear Cache**: Clear application cache after updating settings
3. **Browser Console**: Check browser console for JavaScript errors
4. **Network Tab**: Verify scripts are being loaded in network tab

#### Events Not Tracking
1. **Script Loading**: Ensure tracking scripts are loaded before events
2. **Event Timing**: Verify events are triggered after page load
3. **Data Format**: Check event data format matches platform requirements
4. **Ad Blockers**: Disable ad blockers for testing

#### Performance Issues
1. **Script Optimization**: Optimize and minify custom scripts
2. **Loading Strategy**: Use appropriate loading strategies (async/defer)
3. **Resource Monitoring**: Monitor script loading performance
4. **Caching**: Implement proper caching for tracking resources

### Debug Tools

#### Browser Developer Tools
- **Console**: Check for JavaScript errors
- **Network Tab**: Monitor script loading
- **Application Tab**: Check for tracking cookies
- **Performance Tab**: Monitor script performance

#### Analytics Debugging
- **Google Analytics Debugger**: Chrome extension for GA debugging
- **Facebook Pixel Helper**: Chrome extension for Meta Pixel debugging
- **PostHog Debug Mode**: Enable debug mode in PostHog
- **Custom Debug Logging**: Add console.log statements for debugging

## Support

For technical support with Analytics & Tracking:

1. **Check Documentation**: Review this guide for common solutions
2. **Test Scripts**: Use browser developer tools to test tracking
3. **Verify Settings**: Ensure tracking settings are configured correctly
4. **Contact Development**: Provide specific error details and tracking configurations

### Testing Checklist
- [ ] Global tracking scripts load on all pages
- [ ] Purchase tracking scripts load on success pages
- [ ] Comic-specific scripts load on comic pages
- [ ] Chapter-specific scripts load on chapter pages
- [ ] Events are firing correctly in analytics platforms
- [ ] No JavaScript errors in browser console
- [ ] Tracking respects user privacy settings
