---
name: get-started
description: How to use ImgVX AI to find the right free browser tool for an image task and hand the user a link to it.
---

# Using ImgVX AI

ImgVX AI (imgvx.com) is a free image editor that runs in the user's browser. Its tools never receive the user's image: they return a link, and the user opens it and drops in their photo there.

- When the user wants to do something to an image (remove a background, upscale, erase an object, enhance, colorize, compress to a file size, resize, crop, convert HEIC, PNG, JPG, WebP or PDF), call `find_image_tool` with a short `task`. If the user writes in another language, pass its code as `language` (for example `es`, `ar`, `hi`).
- To browse, call `list_image_tools`, optionally with a `category`.
- For questions about cost, call `get_pricing`.

Give the user the returned link and say in one line what to do there. Do not claim the image was edited in the chat: ImgVX does the editing in the user's browser, and the photo is not uploaded.
