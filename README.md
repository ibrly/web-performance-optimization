# web-performance-optimization

A static page built with webpack 5, used as a playground for front-end performance techniques.

## Techniques applied

| Technique | Where |
|-----------|-------|
| Long-term caching with content-hashed file names (`[name].[contenthash].js/css`) | `src/webpack.common.js` output and MiniCssExtractPlugin |
| Vendor code split into its own chunk (`splitChunks.cacheGroups`) | `src/webpack.common.js` |
| CSS extracted to a file and minified | MiniCssExtractPlugin + CssMinimizerPlugin |
| Unused CSS removed (Bootstrap included) | PurgeCSSPlugin |
| Images compressed at build time (mozjpeg, pngquant, svgo) and WebP variants generated | ImageMinimizerPlugin |
| Modern CSS with fallbacks | postcss-preset-env |
| One-year immutable `Cache-Control` for static assets, ETag removed | [.htaccess](.htaccess) |

## Getting started

```bash
npm install
npm run dev     # webpack-dev-server
npm run build   # production build into dist/
```

Deploy `dist/` together with `.htaccess` on Apache to get the caching headers.

> On Apple Silicon, `imagemin-mozjpeg` may fail to install because its prebuilt binary is x86-only. Switching the image minimizer to `sharp` is on the roadmap.
