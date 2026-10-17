# web-performance-optimization

A static page built with webpack 5, used as a playground for front-end performance techniques.

## Techniques applied

| Technique | Where |
|-----------|-------|
| Long-term caching with content-hashed file names (`[name].[contenthash].js/css`) | `src/webpack.common.js` output and MiniCssExtractPlugin |
| Vendor code split into its own chunk (`splitChunks.cacheGroups`) | `src/webpack.common.js` |
| CSS extracted to a file and minified | MiniCssExtractPlugin + CssMinimizerPlugin |
| Unused CSS removed (Bootstrap included) | PurgeCSSPlugin |
| JPEGs compressed at build time (sharp with mozjpeg, quality 75, progressive) and WebP variants generated with `?as=webp` | ImageMinimizerPlugin + sharp |
| Modern CSS with fallbacks | postcss-preset-env |
| One-year immutable `Cache-Control` for static assets, ETag removed | [.htaccess](.htaccess) |

## Getting started

```bash
npm install
npm run dev     # webpack-dev-server
npm run build   # production build into dist/
```

Deploy `dist/` together with `.htaccess` on Apache to get the caching headers.
