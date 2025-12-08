# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal resume website built using Jekyll, based on the "Crisp Minimal Resume" theme. The resume is deployed to GitHub Pages and generates both a web version and PDF output.

## Architecture

### Data-Driven Design
The entire resume content is managed through YAML configuration:
- `_data/resume.yml`: Contains all resume content (contact, education, skills, experience, languages)
- `_config.yml`: Jekyll site configuration including title and color scheme
- Content is rendered through Liquid templates in `_layouts/resume.html`

### Layout Structure
- `_layouts/default.html`: Base HTML template with head and footer includes
- `_layouts/resume.html`: Resume-specific layout that iterates over data sections
- `_includes/head.html` and `_includes/foot.html`: Reusable header and footer components
- `index.html`: Entry point that uses the resume layout

### Styling
- SCSS files in `_sass/` directory:
  - `_main.scss`: Primary styles and color scheme definitions
  - `_body.scss`: Content and section styling
  - `_header.scss`: Header and contact information styling
  - `_footer.scss`: Footer styling
- Color scheme is configurable via `_config.yml` (currently set to "grape")
- Supports multiple color schemes from Open-Color and Nord

### Section Rendering
The resume layout renders sections dynamically:
1. Header with name, job title, and contact info
2. Education section
3. Skills section (organized by categories)
4. Experience section
5. Projects section (optional, currently commented out)
6. Languages section

Each section follows a consistent block structure with title, subtitle, and content.

## Common Development Commands

### Local Development
```bash
# Install dependencies
./script/bootstrap
# or manually:
gem install bundler
bundle install

# Serve locally with live reload
bundle exec jekyll serve --draft --future --livereload
# or using rake:
rake serve
```

### Building
```bash
# Build the site
bundle exec jekyll build

# Build and lint (CI workflow)
./script/cibuild
```

### Linting
```bash
# Lint SCSS files
bundle exec scss-lint --config=.scss-lint.yml
```

### Rake Tasks
- `rake serve`: Serve with draft and future posts, live reload enabled
- `rake sg`: Serve using gem-based config (`_config_gem.yml`)
- `rake sc`: Serve using colorful config
- `rake cleanup`: Remove built gem files

## Content Management

### Adding/Modifying Resume Content
All resume data lives in `_data/resume.yml`. The structure includes:
- `title`, `name`, `jobtitle`: Header information
- `contact`: Array of contact items with icon, text, and optional link
- `education`: Array of education entries
- `skills`: Array of skill categories with title and items
- `experience`: Array of work experience entries with HTML descriptions
- `languages`: Array of language proficiencies

### Adding New Sections
To add a new resume section:
1. Add the data structure to `_data/resume.yml`
2. Add the rendering logic to `_layouts/resume.html` following the existing section pattern
3. Optionally add specific styles to the appropriate SCSS file

### FontAwesome Icons
Contact section uses FontAwesome icons. Use `fa-` class names (e.g., `fa-envelope`, `fa-github`, `fa-linkedin`).

## Deployment

The site is automatically deployed to GitHub Pages via GitHub Actions (`.github/workflows/jekyll.yml`) when changes are pushed to the `master` branch. The workflow:
1. Checks out the code
2. Sets up Ruby 3.2.2
3. Installs dependencies with bundler
4. Builds the Jekyll site
5. Deploys to GitHub Pages

## Development Notes

- The codebase uses Jekyll 3.8 (specified in gemspec)
- This is both a personal resume site and a reusable Jekyll theme
- The `.tool-versions` file specifies the Ruby version for asdf users
- GitHub Pages compatibility is maintained via the `github-pages` gem
- The site excludes certain files from build (see `_config.yml` exclude list)