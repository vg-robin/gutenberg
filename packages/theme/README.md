# (Experimental) Theme

A theming package that's part of the WordPress Design System. It has two parts:

-   **Design Tokens**: A comprehensive system of design tokens for colors, spacing, typography, and more
-   **Theme System**: A flexible theming provider for consistent theming across applications

## Design Tokens

In the **[Design Tokens Reference](docs/ds-tokens.md)** document there is a complete reference of all available design tokens including colors, spacing, typography, and more.

## Theme Provider

The `ThemeProvider` is a React component that should wrap your application to provide design tokens and theme context to the child UI components.

```tsx
import { ThemeProvider } from '@wordpress/theme';

function App() {
	return (
		<ThemeProvider color={ { scheme: 'light', accent: 'blue' } }>
			{ /* Your app content */ }
		</ThemeProvider>
	);
}
```

The provider can be used recursively to override or modify the theme for a specific subtree.

```tsx
<ThemeProvider>
	{ /* system-themed UI components */ }
	<ThemeProvider color={ { scheme: 'dark' } }>
		{ /* dark-themed UI components */ }
		<ThemeProvider color={ { scheme: 'light' } }>
			{ /* light-themed UI components */ }
		</ThemeProvider>
		{ /* dark-themed UI components */ }
	</ThemeProvider>
	{ /* system-themed UI components */ }
</ThemeProvider>
```

The `ThemeProvider` redefines some of the design system tokens. Components consuming semantic design system tokens will automatically follow the chosen theme. Note that the tokens are defined and inherited using the CSS cascade, and therefore the DOM tree, not the React tree. This is very important when using React portals.

### Building

This package is built in two steps. When `npm run build` is run at the root of the repo, it will first run the "prebuild" step of this package, which is defined in the `build` script of this package's package.json.

This step will:

1. Generate primitive tokens.
2. Build CSS and JavaScript token files.
3. Update the design tokens documentation.
4. Format all generated files.

The files generated in this step will all be committed to the repo.

After the prebuild step, the package will be built into its final form via the repo's standard package build script.

## Contributing to this package

This is an individual package that's part of the Gutenberg project. The project is organized as a monorepo. It's made up of multiple self-contained software packages, each with a specific purpose. The packages in this monorepo are published to [npm](https://www.npmjs.com/) and used by [WordPress](https://make.wordpress.org/core/) as well as other software projects.

To find out more about contributing to this package or Gutenberg as a whole, please read the project's main [contributor guide](https://github.com/WordPress/gutenberg/tree/HEAD/CONTRIBUTING.md).

<br /><br /><p align="center"><img src="https://s.w.org/style/images/codeispoetry.png?1" alt="Code is Poetry." /></p>
