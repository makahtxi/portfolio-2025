# Figma to Astro Case Study Workflow

This document outlines the workflow for converting Figma designs into Astro case study pages following the structure of `src/pages/orbit.astro`.

## Overview

Convert Figma pages (with autolayout) into Astro case studies using a hybrid approach:
- Map recognizable sections to existing Vue components
- Generate inline Tailwind/HTML for unique sections
- Preserve exact design specifications from Figma

## Prerequisites

1. Figma API access token (from Figma account settings)
2. Figma file with case study pages (one page per case study)
3. Figma designs using autolayout for structure
4. Node.js environment for conversion script
5. Existing Astro project with case study components

## Setup

### 1. Figma API Setup

#### 1.1 Get Access Token
- Go to Figma → Settings → Account → Personal Access Tokens
- Generate new token with read access
- Store in `.env` file: `FIGMA_ACCESS_TOKEN=your_token`

#### 1.2 Get File ID
- Open your Figma file
- Copy file ID from URL: `figma.com/file/{FILE_ID}/...`
- Store in `.env`: `FIGMA_FILE_ID=your_file_id`

#### 1.3 Figma File Organization
Each case study should be:
- A separate **page** in one Figma file
- Page name = case study slug (e.g., "orbit", "project-name")
- Top-level frames represent major sections

### 2. Figma Naming Conventions

#### 2.1 Component Frame Naming
Use specific naming patterns to map to existing Vue components:

**Hero Section:**
```
Frame: "Hero" or "CaseStudyHero"
  ├─ "Title" (text)
  ├─ "Subtitle" (text)
  ├─ "Disciplines" (frame with text children)
  ├─ "Metadata" (Year/Client info)
  └─ "HeroImage" (image)
```

**Problem/Solution:**
```
Frame: "Intro" or "CaseIntro"
  ├─ "Problem" (text block)
  └─ "Solution" (text block)
```

**Intro Gallery:**
```
Frame: "IntroGallery" or "IntroImagesGallery"
  ├─ Image frames
  ├─ "ButtonGroup" (optional)
  └─ Nested image frames
```

**Body Sections:**
```
Frame: "Body" or "CaseBody"
  ├─ "Section-FullWidth" → ContainerFull
  ├─ "Section-HalfWidth" → ContainerHalf
  ├─ "PostItNotes" → PostItNotes component
  ├─ "Features" → FeatureList component
  └─ "ImageGrid-2x2" → ImageGrid component
```

#### 2.2 Special Naming Patterns
- `Section-*` → Generates container component
- `PostIt-*` → Creates PostItNote with color from name
- `Feature-*` → Creates FeatureItem
- `Button-*` → Creates Button with variant from name
- `Image-*` → Creates ImageWrapper
- `Grid-*` → Creates ImageGrid with layout from name

### 3. Autolayout Mapping

Figma autolayout properties map directly to Tailwind/Flexbox:

| Figma Property | CSS/Tailwind |
|----------------|--------------|
| Horizontal direction | `flex-row` |
| Vertical direction | `flex-col` |
| Spacing between items | `gap-[X]` |
| Padding | `p-[X]` / `px-[X]` / `py-[X]` |
| Align items: Start | `items-start` |
| Align items: Center | `items-center` |
| Align items: End | `items-end` |
| Justify: Start | `justify-start` |
| Justify: Center | `justify-center` |
| Justify: End | `justify-end` |
| Justify: Space between | `justify-between` |

### 4. Conversion Script Architecture

#### 4.1 Script Structure
```
scripts/figma-to-astro/
├── index.js              # Main CLI script
├── figma-client.js       # Figma API wrapper
├── parser.js             # Parse Figma nodes
├── component-mapper.js   # Map to Vue components
├── style-converter.js    # Convert Figma styles to Tailwind
├── image-exporter.js     # Export and download images
├── astro-generator.js    # Generate .astro file
└── templates/            # Component templates
    ├── hero.js
    ├── intro.js
    └── body-sections.js
```

#### 4.2 Dependencies
```json
{
  "dependencies": {
    "axios": "^1.6.0",
    "dotenv": "^16.0.0",
    "fs-extra": "^11.1.0",
    "sharp": "^0.33.0"
  }
}
```

### 5. Component Mapping Strategy

#### 5.1 Recognition Rules

**Hero Component:**
- Detect by: Frame named "Hero" OR first frame with title + image
- Maps to: `<CaseStudyHero client:load>`
- Extracts: Title, subtitle, disciplines, year, client, hero image

**Intro Component:**
- Detect by: Frame named "Intro" OR frame with "Problem"/"Solution" children
- Maps to: `<CaseIntro client:load>`
- Extracts: Problem text, solution text

**Container Components:**
- Full width: Frame named "Section-Full" OR width > 90% parent
- Half width: Frame named "Section-Half" OR 2 children side-by-side
- Maps to: `<ContainerFull>` or `<ContainerHalf>`

**Special Components:**
- PostIt Notes: Frame named "PostIt*" OR callout-style boxes
- Features: Frame named "Features" OR list with icons/labels
- Image Grids: Frame named "Grid-*" OR regular grid layout

#### 5.2 Fallback Strategy
When no component match is found:
1. Generate Tailwind classes from autolayout
2. Create semantic HTML structure
3. Preserve text and image content
4. Add comment: `<!-- Generated from Figma: [frame name] -->`

### 6. Image Export Process

#### 6.1 Export Settings
```javascript
{
  format: 'png',
  scale: 2,           // 2x for retina displays
  constraint: {
    type: 'WIDTH',
    value: 1200       // Max width
  }
}
```

#### 6.2 Image Organization
```
public/images/[case-study-slug]/
├── hero.png
├── intro-01.png
├── intro-02.png
├── section-01.png
└── ...
```

#### 6.3 Naming Convention
- Extract from Figma layer name
- Sanitize (lowercase, replace spaces with hyphens)
- Add sequential numbers for unnamed images
- Preserve semantic meaning where possible

### 7. Execution Workflow

#### 7.1 CLI Commands
```bash
# List all pages in Figma file
npm run figma-export -- --list

# Export specific case study by page name
npm run figma-export -- --page="orbit"

# Export with custom output path
npm run figma-export -- --page="orbit" --output="src/pages/case-studies/"

# Dry run (preview without writing files)
npm run figma-export -- --page="orbit" --dry-run

# Export all pages
npm run figma-export -- --all
```

#### 7.2 Process Flow
1. Connect to Figma API with file ID
2. Fetch page structure by name
3. Parse all frames and nodes recursively
4. Identify component patterns
5. Export all images with proper naming
6. Convert styles to Tailwind classes
7. Generate Vue component structure
8. Create `.astro` file at specified path
9. Log summary and warnings

### 8. Style Conversion

#### 8.1 Typography
```javascript
// Figma → Tailwind mapping
fontSize: 44 → 'text-[44px]'
fontWeight: 700 → 'font-bold'
fontWeight: 600 → 'font-semibold'
fontWeight: 500 → 'font-medium'
fontFamily: 'Inter' → (default, no class needed)
textAlign: 'CENTER' → 'text-center'
```

#### 8.2 Colors
```javascript
// Extract from Figma fills
fills[0].color: {r, g, b, a}
→ Convert to hex or Tailwind color class
→ Check against existing Tailwind config
→ Use closest match or custom class
```

#### 8.3 Spacing & Layout
```javascript
// Autolayout properties
layoutMode: 'HORIZONTAL' → 'flex flex-row'
layoutMode: 'VERTICAL' → 'flex flex-col'
itemSpacing: 20 → 'gap-5'
paddingLeft: 16 → 'pl-4'
```

### 9. Generated Output Example

```astro
---
import BaseLayout from "../layouts/BaseLayout.astro";
import CaseStudyHero from "../components/CaseStudyHero.vue";
// ... other imports
---

<BaseLayout title="Project Name - Case Study">
  <CaseStudyHero client:load>
    <div class="flex flex-col md:flex-row justify-between h-fit mx-auto pt-28">
      <!-- Generated from Figma Hero frame -->
      <div class="flex flex-col w-full md:w-[45%]">
        <span class="text-2xl font-medium text-brand-color m-0">Case Study</span>
        <h1 class="text-[44px] font-bold m-0">Project Title</h1>
        <!-- ... -->
      </div>
      <img src="/images/project-name/hero.png" alt="Hero Image" />
    </div>

    <CaseIntro client:load>
      <!-- Problem/Solution from Figma -->
    </CaseIntro>
  </CaseStudyHero>

  <CaseBody client:load>
    <!-- Mapped sections -->
  </CaseBody>
</BaseLayout>
```

### 10. Configuration File

Create `figma-export.config.js`:

```javascript
module.exports = {
  // Component mapping rules
  componentMap: {
    'Hero': 'CaseStudyHero',
    'Intro': 'CaseIntro',
    'Section-Full': 'ContainerFull',
    'Section-Half': 'ContainerHalf',
    'PostIt-*': 'PostItNote',
    'Features': 'FeatureList',
  },

  // Image export settings
  images: {
    format: 'png',
    scale: 2,
    maxWidth: 1200,
    outputPath: 'public/images',
  },

  // Style preferences
  styles: {
    useCustomColors: true,
    roundSpacing: true,  // Round to nearest Tailwind value
    preserveFontSizes: true,  // Use exact px values
  },

  // Output settings
  output: {
    path: 'src/pages',
    fileExtension: '.astro',
    addComments: true,  // Add Figma reference comments
  }
};
```

### 11. Edge Cases & Handling

#### 11.1 Complex Layouts
- **Nested autolayout**: Preserve hierarchy, map to nested divs
- **Absolute positioning**: Convert to absolute positioning classes
- **Overlapping elements**: Use z-index and relative positioning

#### 11.2 Text Handling
- **Rich text**: Parse bold, italic, links
- **Text overflow**: Add appropriate classes (truncate, line-clamp)
- **Multi-line**: Preserve line breaks or convert to paragraphs

#### 11.3 Component Props
- **Button variants**: Extract from layer name or color
- **Image rounding**: Map corner radius to Tailwind rounded classes
- **Shadows**: Convert to Tailwind shadow classes

### 12. Manual Review Checklist

After automatic conversion:

- [ ] All images exported and paths correct
- [ ] Component hierarchy matches Figma structure
- [ ] Responsive behavior preserved (md: breakpoints)
- [ ] Colors match Figma design
- [ ] Typography sizes and weights correct
- [ ] Spacing and gaps accurate
- [ ] Vue components have `client:load` directive
- [ ] Special components (PostIt, Features) mapped correctly
- [ ] Links and buttons functional
- [ ] Alt text added for accessibility

### 13. Iteration & Refinement

After first conversion:

1. **Compare output to Figma**: Verify visual accuracy
2. **Test responsive behavior**: Check mobile/tablet views
3. **Update mapping rules**: Add new pattern recognitions
4. **Refine style conversion**: Adjust Tailwind mappings
5. **Document custom patterns**: Note any manual adjustments needed
6. **Update config file**: Add project-specific rules

### 14. Advanced Features (Future)

- **Component variants detection**: Recognize and apply Vue component variants
- **Animation extraction**: Map Figma prototyping to CSS animations
- **Responsive breakpoints**: Extract Figma responsive settings
- **Design tokens**: Sync Figma styles to Tailwind config
- **Incremental updates**: Re-export only changed sections
- **Figma plugin**: UI within Figma for one-click export

### 15. Maintenance

- Keep Figma API client updated
- Document naming conventions for team
- Maintain example Figma pages as reference
- Version control the config file
- Update component mappings as Vue components evolve

---

## Next Steps

1. ✅ Set up Figma API access and credentials
2. ✅ Document current Figma file structure and naming
3. 🔄 Develop core conversion script modules
4. 🔄 Test with orbit case study as reference
5. 🔄 Refine component mapping rules
6. 🔄 Create config file with project-specific settings
7. ⏳ Build remaining script features
8. ⏳ Test with all case study pages
9. ⏳ Document any edge cases or manual steps required

## Figma Design Guidelines

To ensure smooth conversion, follow these guidelines in Figma:

### Layout
- Use autolayout for all containers
- Keep consistent spacing values (multiples of 4)
- Group related elements in named frames

### Naming
- Use descriptive frame names
- Follow component naming patterns
- Name images semantically

### Components
- Use Figma components for repeated elements
- Keep hierarchy shallow where possible
- Organize with clear parent-child relationships

### Text
- Use consistent text styles
- Avoid manual text formatting where possible
- Keep copy in editable text layers

### Images
- Use high-quality images (will be exported at 2x)
- Ensure proper image fills (not background fills with images)
- Name image layers descriptively
