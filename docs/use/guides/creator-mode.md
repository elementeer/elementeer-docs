# Creator Mode

Creator Mode is Elementeer's page composition system. It lets your AI agent build complete Elementor pages by assembling sections from your template library, matching section types to structural requirements, and importing content from structured descriptions.

## How Creator Mode Works

Instead of placing individual widgets, Creator Mode operates at the section level:

1. You describe what you need ("a landing page with a hero, three feature columns, and a CTA")
2. The agent analyzes your template library for matching sections
3. The agent assembles the sections into a complete page
4. Optional: the agent customizes content within each section

## Section-Type Matching

The Creator Mode engine understands structural roles and matches them to templates:

| Structural Role | Template Types | Expected Widgets |
|----------------|---------------|-----------------|
| `hero` | Hero sections | Heading, text, button, background image |
| `features` | Feature grids, icon boxes | Grid columns with icon boxes |
| `cta` | Call to action | Heading, text, large button |
| `testimonials` | Testimonial carousels, grids | Testimonial widgets |
| `pricing` | Pricing tables | Pricing table widgets |
| `contact` | Contact forms, maps | Form widget, Google Maps |
| `team` | Team member grids | Image boxes, social icons |
| `stats` | Counter sections | Counter/number widgets |
| `faq` | FAQ, accordion | Accordion widget |
| `content` | Text sections | Rich text, headings |
| `gallery` | Image galleries, sliders | Gallery, carousel widgets |

## Building a Page with Creator Mode

From your AI agent:

```
Create a homepage using Creator Mode: hero section with headline "Build Faster with Elementor",
three feature cards for Speed, Design, and Integration, a customer testimonial section,
and a CTA to sign up.
```

The agent:

1. Calls `elementeer_list_templates` filtered by type `section`
2. Matches structural roles to available templates
3. Calls `elementeer_create_page` with the assembled structure
4. Optionally customizes content in each section using `elementeer_update_element`

## Import from Description

Creator Mode can generate page structures from free-text descriptions:

```
I need a service page. It should have a hero with the service name and a brief description,
a section for our process (3 steps), client results with numbers, and a contact form.
```

The agent maps the description to structural roles and finds matching templates. If an exact match isn't available, it finds the closest structural match and adapts.

## Creative Mode vs Precision Mode

Creator Mode operates in two styles:

### Creative Mode

The agent selects templates based on structural fit and aesthetic quality. Best for exploration and rapid prototyping. The agent makes judgment calls about which template variant to use.

### Precision Mode

You specify exact template IDs or names. The agent uses only those templates with no substitutions. Best for production pages where you need predictable results.

```
Build a landing page using exactly:
- Template ID 42 for the hero (Hero Dark V2)
- Template ID 87 for features (Icon Grid 3-Col)
- Template ID 15 for the CTA (CTA Gradient)
```

## Content Injection

Creator Mode can populate section content from structured data:

```json
{
  "hero": {
    "heading": "Build Faster with Elementor",
    "subheading": "The agent-native approach to Elementor site management",
    "button_text": "Get Started",
    "button_url": "/pricing"
  },
  "features": [
    {
      "title": "Speed",
      "description": "Ship sites in hours, not days",
      "icon": "fa-bolt"
    },
    {
      "title": "Design",
      "description": "Pixel-perfect templates, every time",
      "icon": "fa-paint-brush"
    }
  ],
  "cta": {
    "heading": "Ready to build faster?",
    "button_text": "Start Free Trial"
  }
}
```

The agent injects this data into the assembled sections, updating heading text, replacing images, and setting button URLs.

## Post-Creation Cleanup

After Creator Mode builds a page, run these verification steps:

```
Run an SEO check on the new homepage and optimize meta tags.
```

The agent calls `elementeer_analyze_seo` to check heading hierarchy, meta completeness, and image alt text on the newly created page.
