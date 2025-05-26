# Rails Application: Layouts and Stylesheets

## Concept of a Rails Application

A Rails application follows the Model-View-Controller (MVC) architectural pattern, providing a structured way to build web applications. Key characteristics include:

- **Convention over Configuration**: Rails has sensible defaults that reduce the need for configuration
- **DRY (Don't Repeat Yourself)**: Encourages code reuse and modularity
- **RESTful design**: Resources are typically modeled around REST conventions

## Layouts in Rails

Layouts are templates that wrap around your views to provide a consistent structure across multiple pages in your application.

### Key Aspects of Layouts:

1. **Default Layout**: `app/views/layouts/application.html.erb` is the default layout
2. **Yield Statement**: The `<%= yield %>` statement renders the content of individual views
3. **Controller-Specific Layouts**: You can create layouts specific to controllers (e.g., `app/views/layouts/admin.html.erb`)

### Example Layout Structure:

```erb
<!DOCTYPE html>
<html>
<head>
  <title>MyApp</title>
  <%= stylesheet_link_tag 'application' %>
  <%= javascript_include_tag 'application' %>
  <%= csrf_meta_tags %>
</head>
<body>
  <header>
    <!-- Common header content -->
  </header>
  
  <main>
    <%= yield %>  <!-- View content goes here -->
  </main>
  
  <footer>
    <!-- Common footer content -->
  </footer>
</body>
</html>
```

### Layout Inheritance:

- Layouts can be specified in controllers:
  ```ruby
  class AdminController < ApplicationController
    layout 'admin'
  end
  ```

- You can also use conditional layouts:
  ```ruby
  layout :resolve_layout
  
  def resolve_layout
    current_user.admin? ? "admin" : "application"
  end
  ```

## Stylesheets in Rails

Rails uses the Asset Pipeline to manage stylesheets, which provides:

1. **Concatenation**: Combines multiple files into one for reduced HTTP requests
2. **Minification**: Reduces file size by removing whitespace and comments
3. **Preprocessing**: Supports Sass/SCSS, CoffeeScript, etc.

### Stylesheet Organization:

- Default location: `app/assets/stylesheets/`
- Main file: `application.css` serves as the manifest
- Convention is to have:
  - `application.css` (manifest)
  - Controller-specific stylesheets (e.g., `products.css.scss`)
  - Shared components (e.g., `_variables.scss`, `_buttons.scss`)

### Manifest File Example (`application.css`):

```css
/*
 *= require_tree .
 *= require_self
 *= require custom
 */
```

### Using SCSS/Sass:

Rails supports Sass out of the box. Example:

```scss
// app/assets/stylesheets/application.scss

@import 'variables';
@import 'mixins';
@import 'layout';
@import 'components/*';
```

### Asset Helpers in Views:

Rails provides helpers to reference assets:

```erb
<%= stylesheet_link_tag 'application', media: 'all' %>
<%= stylesheet_link_tag 'print', media: 'print' %>
```

### CSS Framework Integration:

Many Rails apps use CSS frameworks like Bootstrap:

1. Add to Gemfile: `gem 'bootstrap'`
2. Rename `application.css` to `application.scss`
3. Import Bootstrap:

```scss
@import "bootstrap";
```

## Best Practices

1. **Layouts**:
   - Keep shared HTML structure in layouts
   - Use content_for to inject content into specific layout sections
   - Consider using partials for reusable components

2. **Stylesheets**:
   - Organize with a modular approach (SMACSS, BEM)
   - Use controller-specific stylesheets when appropriate
   - Leverage Sass features like variables and mixins
   - Keep vendor styles separate from your custom styles

This structure helps maintain clean separation of concerns while providing a consistent look and feel across your Rails application.