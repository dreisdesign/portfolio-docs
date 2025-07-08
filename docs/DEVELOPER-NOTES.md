# Developer Notes

This document contains deep technical implementation notes, browser-specific workarounds, and advanced build pipeline details for the portfolio system. For design, content, and UI guidelines, see [DESIGN-SYSTEM.md](DESIGN-SYSTEM.md).

---

## Browser-Specific Fixes

### Safari Layout Compatibility

#### Issue: "Up Next" Cards Loading Narrow
Safari's layout engine sometimes incorrectly calculates grid/flexbox dimensions on initial page load, causing the "Up Next" project cards to render too narrow. The cards would resize correctly on hover or page refresh, indicating a layout calculation timing issue.

#### Solution: Force Layout Recalculation
Implemented `safari-layout-fix.js` with a simple but effective approach:

```javascript
// Wait for complete page load
window.addEventListener('load', () => {
  setTimeout(() => {
    const container = document.querySelector('.next-project-container');
    if (container) {
      // Force complete layout recalculation by hiding/showing container
      const display = container.style.display;
      container.style.display = 'none';
      container.offsetHeight; // Force reflow
      container.style.display = display;
    }
  }, 100);
});
```

**Key principles:**
- **Safari-only targeting:** Uses user agent detection to avoid unnecessary processing in other browsers
- **Complete page load:** Waits for `window.load` event to ensure all assets are loaded
- **Simple force reflow:** Temporarily hides container to force Safari to recalculate entire layout
- **Minimal timeout:** 100ms delay ensures timing is right for Safari's layout engine

### Zoomable Image Safari Fixes
Safari also had issues with image zoom functionality where images would become aliased after zooming and centering was broken. This was resolved in `zoomable-image.js` by:
- Resetting transforms before applying new zoom transforms
- Using explicit centering calculations rather than relying on Safari's transform-origin
- Ensuring image quality is maintained during zoom operations
- **Using zoom-optimized image variants** for better performance and quality
- **Grayblue placeholder loading animation** that's comfortable and non-motion-based

### Zoom-Optimized Image Pipeline & Loading Experience
The build system now creates compressed zoom variants and provides a comfortable loading experience:
- **Source:** Original high-resolution images (typically large, upscaled files)
- **Zoom Variants:** `{basename}-zoom.png` files created by Sharp with quality: 95, compressionLevel: 6
- **File Size Reduction:** Typically 60-70% smaller than originals while maintaining zoom quality
- **Fallback Chain:** Zoom variant → Original PNG → Currently displayed image
- **Build Integration:** Missing zoom variants are auto-detected and regenerated during builds

**Loading Animation:**
- **First zoom:** Shows a grayblue (`--grayblue`) placeholder in the exact shape of the original image
- **High-res fade-in:** Smooth opacity transition from placeholder to final image (0.5s)
- **Subsequent zooms:** Simple "Loading..." text indicator with faster fade-in (0.4s)
- **Transparent image support:** Offwhite (`--offwhite`) background with subtle shadow and rounded corners
- **Comfortable UX:** No blur or motion effects that could cause dizziness

The zoom-optimized approach significantly reduces bandwidth usage for zoomable images while maintaining the high quality needed for detailed examination of portfolio work.

---

## Video Performance Optimizations (2025-01-16)

### Immediate Code Improvements - IMPLEMENTED & TESTED
- **Intelligent preloading**: Videos now preload metadata when they come into viewport (-200px margin)
- **Progressive loading**: Videos in prominent view (70%+ visible) preload full data after 1 second delay
- **Real progress indication**: Progress bar shows actual buffering progress instead of simulated loading
- **Better loading detection**: Multiple fallback event listeners (`loadeddata`, `canplay`, `progress`) for more reliable loading
- **Increased timeout**: Extended fallback timeout to 8 seconds for large files
- **Result**: Significantly faster video loading experience - videos now load "really fast" per user testing

### Performance Issues Identified
- Video files are 1MB-21MB (most 3-8MB) - too large for web
- High resolution (1080p+) and bitrate (2.1-2.3 Mbps) for short demos
- No web optimization in current workflow

### Video Optimization Script - OPTIONAL FURTHER IMPROVEMENT
Created `/bin/optimize-videos.sh` to compress existing videos for even better performance:
- Reduces bitrate to 1.2 Mbps (web-optimized)
- Limits max width to 1280px
- Uses efficient H.264 encoding with faststart
- Creates backups before optimization
- Targets 50-80% file size reduction

To run: `./bin/optimize-videos.sh`

*Note: Current loading performance is already fast due to preloading optimizations. Video compression would provide additional bandwidth savings and faster initial page loads.*

### Recommended Workflow Changes
1. Export videos at 720p-1080p max with 1-1.5 Mbps bitrate
2. Use H.264 codec with "fast start" enabled
3. Consider WebM format for additional compression
4. Implement responsive video sources for different screen sizes

---

*For the main build pipeline, see [BUILD-PIPELINE.md](BUILD-PIPELINE.md).*
