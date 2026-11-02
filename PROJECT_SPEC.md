# Font Finder — Project Specification

## 1. Project Overview

Font Finder is a lightweight Windows desktop application that identifies fonts from images by comparing visual glyph shapes.

The primary purpose is to identify the exact font used in an input image. If an exact match is unavailable, the application must display up to 20 visually similar fonts, ranked by similarity.

The application must work completely offline and must not require paid APIs, subscriptions, cloud services, or internet access during normal operation.

## 2. Main Priorities

Priority order:

1. Identify the exact font when it exists in the searchable font collection.
2. If no exact match is found, display up to 20 similar fonts.
3. Rank candidates by visual similarity.
4. Display a similarity score and a preview for each candidate.
5. Clearly distinguish confirmed matches from estimated matches.

Do not claim an exact match unless the evidence supports it.

## 3. Image Input

Support:

- PNG
- JPG / JPEG
- BMP
- Other formats only when supported by the selected free libraries.

The user must be able to:

- Browse and select an image.
- Drag and drop an image.
- Preview the selected image.
- Crop or select a region containing text.
- Optionally enter the text manually if OCR cannot recognize it.

Images may contain:

- Normal text
- Individual letters
- Logos
- Decorative lettering
- Graphic text
- Persian, Arabic, or English text

## 4. Language Support

The application must support:

- Persian
- Arabic
- English / Latin

Persian and Arabic processing must consider:

- Right-to-left text.
- Connected letters.
- Initial, medial, final, and isolated glyph forms.
- Dots and diacritical marks.
- Correct text shaping and rendering.

OCR must be optional and auxiliary. Visual font comparison is the core functionality.

## 5. Font Discovery

Search accessible font locations, including:

- Windows system fonts.
- Current-user installed fonts.
- Known font directories used by installed applications.
- Additional directories selected manually by the user.

Support TTF and OTF initially.

Support TTC and variable fonts if technically practical.

Never assume that every font embedded inside every installed application is accessible.

Avoid scanning protected locations without permission.

## 6. Font Matching Engine

The matching engine is the most important component.

It must use visual comparison, not OCR alone.

Consider:

- Glyph contours.
- Letter proportions.
- Stroke thickness.
- Curves and corners.
- Character spacing.
- Letter shapes.
- Dots and small details.
- Overall visual structure.

Use complementary image-processing and shape-comparison techniques.

Where text is available, render candidate fonts using the same text and compare the rendered results against the input image.

Where text is unavailable, attempt visual glyph and shape comparison.

If the image contains only a small number of letters, report uncertainty and show ranked candidates instead of promising a guaranteed identification.

For Persian and Arabic, use a rendering method that correctly handles shaping and right-to-left layout.

## 7. Results

The results screen must show:

- Exact match, when sufficiently supported.
- Up to 20 similar fonts.
- Font name.
- Similarity percentage or score.
- Visual preview.
- Font file location when accessible.
- A clear indication when a result is uncertain.

Allow the user to change the preview text.

## 8. User Interface

Create a simple, modern, lightweight desktop interface.

Main screen:

- Application title.
- Image selection area.
- Drag-and-drop support.
- Image preview.
- Optional text input.
- Search button.
- Progress indicator.
- Results list.

The interface should be easy to use for non-technical users.

Plan for Persian right-to-left interface support.

## 9. Technical Requirements

Target operating systems:

- Windows 7 SP1, if technically feasible.
- Windows 8, 10, and 11.

Prefer C# and WPF if compatible with the required Windows versions.

Before selecting a framework or runtime, verify:

- Windows 7 compatibility.
- Library compatibility.
- Offline deployment requirements.
- Installer size.
- Availability of free development tools.

Do not select a modern runtime that silently drops Windows 7 support.

If supporting Windows 7 requires a separate build or compromises functionality, explain this before implementation.

## 10. Cost and Offline Requirements

All development tools, libraries, and dependencies must be free to use.

Do not use:

- Paid APIs.
- Paid cloud services.
- Subscription-only services.
- Online font recognition services.
- Runtime internet dependencies.

The application must perform font scanning, image processing, matching, and preview generation locally.

Use