# Angular Material Template Theme

The purpose of this repo is to help you get up and running with a customized Angular Material theme. These can be copied into any new project in order to get started faster.

- Provides out-of-the-box light and dark themes set by `preferred-color-scheme` media queries. Uses Angular Material's own light and dark palettes for foreground, background, and divider colors, providing consistency with Angular Material components.
- Choose the primary, accent, and warn palettes you want to use, along with their hues to get a theme tailored to your color choices.
- Choose the font families to use for your theme's typography.
- Palettes are not only applied to Angular Material components, but are also exposed in CSS custom properties for you to use throughout your project's styles.
- Core stylesheet built upon [Josh W. Comeau's fantastic modern CSS reset](https://www.joshwcomeau.com/css/custom-css-reset), adapted for an Angular app.

## Usage

This should work with Angular Material 13.x and 14.x.

### Set up

First thing's first: [bootstrap your Angular project](https://angular.io/guide/setup-local) and [install Angular Material](https://material.angular.io/guide/getting-started) (if you haven't already).

- When bootstrapping your Angular project, choose SCSS as your stylesheet format.
- When installing Angular Material, choose the Custom theme when prompted by the CLI.

### Copy the files

This is more easily used with brand new projects, as some of these files (such as `styles.scss` may overwrite existing files).

- For a new project, simply copy the contents of the `src` directory to the `src` directory of your Angular project.
- For an existing project, you may need to manually merge the contents of `styles.scss` into your existing `styles.scss` (as well as any modules that share the same name as existing ones in your project).

### Customize your preferences

Open `src/styles/_preferences.scss` and follow the steps in the comments to:

1. Define your [Angular Material palettes](https://material.angular.io/guide/theming#predefined-palettes): primary, accent, and warn.
2. Define the hues for each palette's light and dark themes.

- Each palette has a default, light, and dark hue. These are used to style different aspects of Angular material components.
- This may take some trial and error to find the best combinations for your chosen palettes, though the defaults should be a good start.
- Please be sure to test for accessible color contrast, too! (Strive for a WCAG 2.0 AA ratio.)

3. Define the font families you want to use in your theme's [typography](https://material.angular.io/guide/typography).

The theme system will take care of the rest!

### Recommended: add `stylePreprocessorOptions`

Ideally the `src/styles` directory should be added to the [`stylePreprocessorOptions`](https://angular.io/guide/workspace-config#style-preprocessor-options) in `angular.json` (for both the `build` and `test` options):

```json
{
  "stylePreprocessorOptions": {
    "includePaths": ["src/styles"]
  }
}
```

In your component styles, this allows you to include the modules in that directory by name only -- no need to provide relative paths!

```scss
@use "mixins";

// vs.

@use "../../styles/mixins";
```

### What's included

- `src/styles.scss`: simple starter stylesheet. Provides the basics for a light/dark theme.
- `src/styles/_mixins.scss`: a starting point for your own mixins. Comes with the `mat-toolbar-top-padding` mixin. If you like to use fixed-position `<mat-toolbar>` components, this adds precise top-padding to your content containers so the toolbar won't overlap.
- `src/styles/_preferences.scss`: this is where you can customize the palettes, hues, and typography for your Angular app.
- `src/styles/_variables.scss`: this contains all of the CSS custom properties that are available to use. In addition to typrography properties, you'll find the following for light and dark themes:
  - Theme colors: good for most use cases, these provide the values for background, foreground, and divider colors. And, for each color palette, the default, light, and dark hues along with their corresponding contrast colors.
  - Color primatives: these provide the specific hues available in each of your color palettes. They correspond to the values used in the Material Design color system (i.e. 50, 100-900, A100, A200, A400, A700).
- `src/theme`: in this directory are the modules that do all the heavy lifting. They take your preferences and crank out your theme. You are welcome to modify these for advanced customizations, but you probably won't need to.
  - `_dark.scss`: defines the dark theme
  - `_light.scss`: defines the light theme
  - `_material.scss`: applies your themes to Angular Material
  - `_reset.scss`: the CSS reset styles
  - `_typography.scss`: defines the typography theme
