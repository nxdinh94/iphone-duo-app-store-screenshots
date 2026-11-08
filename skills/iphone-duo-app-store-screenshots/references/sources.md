# iPhone Duo screenshot references

## Apple requirements and export checks

App Store Connect accepts 1–10 screenshots per device size in PNG or JPEG (.png, .jpg, .jpeg), with no alpha channel or transparency. Dimensions below are width × height. The Figma columns are optional canvas sizes derived by dividing the upload pixels by three. Export those canvases at 3×, or create canvases at the upload pixel dimensions and export at 1×. Use Apple's upload dimensions even when hardware panel specifications differ. [Apple screenshot specifications](https://developer.apple.com/help/app-store-connect/reference/app-information/screenshot-specifications)

| Display | Portrait upload | Landscape upload | Portrait canvas at 3× | Landscape canvas at 3× |
| --- | --- | --- | --- | --- |
| Outer, folded | 1398 × 2034 | 2034 × 1398 | 466 × 678 | 678 × 466 |
| Inner, unfolded | 2007 × 2853 | 2853 × 2007 | 669 × 951 | 951 × 669 |

Apple announced Duo submission support in October 2026. Apple's screenshot specifications list an April 2027 requirement for apps using the iOS 27.1 SDK or later. Confirm current requirements for the actual build and listing in App Store Connect. [Apple submission announcement](https://developer.apple.com/news/?id=kkphp5qo)

For Figma, use an opaque rectangular export frame and keep rounded device art inside it. If a PNG still contains alpha, flatten it against the artwork's intended background and write a file with no alpha channel. On macOS inspect the actual file with:

```sh
sips -g format -g pixelWidth -g pixelHeight -g hasAlpha "01-duo-inner-portrait.png"
```

Match the intended row and orientation, confirm `format` is `png` or `jpeg`, and require `hasAlpha: no`. Confirm the app UI and caption are readable in the final thumbnail. For real captures and App Store preview placement, see [Apple's iPhone Duo preparation guide](https://developer.apple.com/iphone-duo/prepare/) and [App Store asset guidance](https://developer.apple.com/app-store/asset-best-practices/). For use of captions and overlays, see [App Review Guideline 2.3.3](https://developer.apple.com/help/app-review/guideline-reference/2-3-3-screenshots).

## Screen size inside device artwork

Use these screen-content artboards when placing the app inside a device frame. The bezel, shadow, headline, and background are outside this rectangle. The final upload canvas is sized independently using the upload table above.

| Device state and visible display | Screen base, width × height (px) | Equivalent artboard at 3× |
| --- | --- | --- |
| Closed portrait, outer | 1398 × 2034 | 466 × 678 |
| Closed landscape, outer | 2034 × 1398 | 678 × 466 |
| Open portrait, inner | 2007 × 2853 | 669 × 951 |
| Open landscape, inner | 2853 × 2007 | 951 × 669 |

For a partially folded pose showing the inner display, start from the corresponding full inner artboard, then apply the matching frame’s fold or perspective to the screen and device together. A fold does not turn the full inner screen into an outer screen or give each half the outer display dimensions. These are composition bases, not measured hardware panel sizes or new screenshot upload categories.

Size the screen first and fit the device frame around it. Scale both uniformly for placement: a Closed portrait screen at 50% is 699 × 1017 px, excluding its bezel. Record the base size and placement scale in the editable artwork or export list. If a supplied capture or frame has incompatible proportions, obtain the correct capture or frame rather than squeezing, stretching, or cropping away app UI. Keep upright and landscape app layouts distinct; do not rotate a landscape capture to invent the upright layout.

The [Appetite UI walkthrough](https://www.appetiteui.com/blog/iphone-duo-app-store-screenshots) explains these four artboard sizes and scaled screen placement inside a marketing canvas. Use it for composition sizing and Apple’s current specification for submission requirements. The bundled frame sheet provides pose guidance; its printed outlines do not override the dimensions above.

## Figma and composition references

- **iPhone Duo Adaptive Design Starter Kit by Noah Elhadedy.** Use its device frames and guides for the fold, safe areas, camera, and adaptive navigation as layout references. Confirm derived and illustrative values against Apple where relevant. The author lists CC BY 4.0. Credit the creator if adapting kit assets. The linked Figma node was inaccessible during collection, so the kit summary comes from the author's public overview. [Requested Figma node](https://www.figma.com/design/nuqkxa6UwYvSpqWfQiPbo0/iPhone-Duo-Adaptive-Design-Starter-Kit--Community-?node-id=1-4&p=f&t=dladVtRVaIMBc1hz-0), [author overview and license](https://noahelhadedy.com/resources/iphone-duo-adaptive-design-starter-kit).
- **Appetite UI's Duo screenshot walkthrough.** Use it for 3× frame setup and diagnosing PNG exports with alpha. Build the composition for the captured orientation. Use Apple's current specifications for submission requirements. [Appetite UI walkthrough](https://www.appetiteui.com/blog/iphone-duo-app-store-screenshots).
- **SnapMonk's folded and unfolded walkthrough.** Use its continuity example and side-by-side caption and device arrangement as optional composition ideas. Its upload status predates Apple's launch announcement, and the generator described there produces standard 6.9-inch images. [SnapMonk Duo walkthrough](https://snapmonk.com/blog/iphone-duo-app-store-screenshots).
- **SnapMonk's general size guide.** Use it for thumbnail readability and the distinction between stills and video previews. Its required-device table differs from current App Store Connect Help. [SnapMonk size guide](https://snapmonk.com/guides/app-store-screenshot-sizes).
- **User-supplied example.** The Files image demonstrates a centered device, a short headline, and a supporting line on a quiet background. Use it for visual hierarchy when requested. Use the target app's own captures, copy, and branding for deliverables. [Attached visual reference](duo-composition-example.png).
- **User-supplied Duo frame sheet.** Read the left column for device outlines, the middle for screen-only views, and the right for safe areas and fold guides. The first row is Closed portrait and the second is Closed landscape. Match the outline and corner proportions, then place the real app capture inside it. Keep the camera and status area from the capture. Leave the sheet’s labels, placeholders, and guide overlays out of the export. [Duo device frame sheet](duo-device-frame-reference.png).
