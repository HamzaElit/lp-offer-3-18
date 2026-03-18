---
trigger: always_on
---

---



## Figma MCP usage

- When user provides any Figma link, always use Figma MCP first to extract layout, spacing, typography, and design tokens.
- Do not copy Figma literally; adapt to project conventions and existing tokens/utilities.
- If a needed color token is missing, add it to `scss/variables-site/_variables-site.scss` before using it.


## SCSS standards

- Mobile-first is mandatory.
- Use breakpoint mixins from `scss/mixins/_mixins-master.scss` (`xs-up`, `sm-up`, `md-up`, `lg-up`, `xl-up`, `xxl-up`) for progressive enhancement.
- Prefer CSS variables from `scss/variables-site/_variables-site.scss` for colors, spacing, radii, and typography values.
- Reuse helpers from `scss/helpers/_helpers.scss`; if a utility is repeatedly needed and does not exist, add a general helper class there.
- Do not redefine heading/body font sizes if already defined in `scss/variables-site/_variables-site.scss` typography tokens; reuse existing typography tokens/styles.


## Typography & Fonts

- Primary font: `sofia-pro` for body and most titles.
- Secondary/Accent font: `Ekamai` should only be used if specified in the Figma design (typically for decorative titles or specific emphasis).
- Use CSS variables `--font-text` and `--font-titles` for consistency. If `Ekamai` is required, verify if it should be set as the new `--font-titles` or used as a one-off class.

## Layout behavior

- Prefer CSS Grid for section composition.
- Allow grid item order to change on mobile when needed for better content flow.
- Use section headers when they improve structure and readability.

## HTML and SCSS writing pattern

- Follow a consistent BEM-like section pattern: `.section-name`, `.section-name__element`, and optional `.layout-2`, `.layout-3`.
- Keep HTML semantic and minimal, and keep styling nested under the section root in SCSS.

**Section Structure Pattern (HTML):**

```html
<section class="section-name">
	<div class="section-name__container container">
		<header class="section-name__header">
			<h2 class="section-name__title">Title</h2>
			<p class="section-name__subtitle">Subtitle</p>
		</header>
		<div class="section-name__content">
			<!-- Content -->
		</div>
	</div>
</section>
```

**Section Style Pattern (SCSS):**

```scss
.section-name {
	&__container {
		display: grid;
		gap: var(--inner-spacing);
	}

	&__header {
		display: grid;
		gap: 1.2rem;
	}

	// Do not redefine heading sizes if already provided in typography tokens.
	&__title {
		color: var(--Deep-Blue);
	}

	&__content {
		display: grid;
		gap: 2rem;
	}

	&.layout-2 {
		.section-name__container {
			@include md-up {
				grid-template-columns: 1fr 1fr;
			}
		}
	}

	&.layout-3 {
		.section-name__container {
			@include lg-up {
				grid-template-columns: repeat(3, 1fr);
			}
		}
	}
}
```