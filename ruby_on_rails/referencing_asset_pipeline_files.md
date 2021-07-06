Accessing Assets in Production Processed by Sprockets Asset Pipeline 
================================================================================

When referencing image assets from a `.scss` file, use the `image-url` helper
method to generate a url to the asset after it's been processed by Sprockets.

In development, the local app server (often Puma) can find the source image
assets referenced by the static url. In production the source development
assets aren't available. So without the Sprockets generated URL, the server
will be trying to access assets in a location that only exist in development.

https://guides.rubyonrails.org/asset_pipeline.html#css-and-sass
