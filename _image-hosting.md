# Notes on how images are hosted for personal reference

## AWS S3 bucket info

- S3 bucket is `assets.ansonj.org`
- Region is `us-east-2`

For HTTPS, you can use:

> https://s3.us-east-2.amazonaws.com/assets.ansonj.org/construction.png

For HTTP, you can use:

> http://s3.us-east-2.amazonaws.com/assets.ansonj.org/construction.png
>
> or
>
> http://assets.ansonj.org.s3.us-east-2.amazonaws.com/construction.png

## Adding a new object

1. Strip EXIF location data if needed.
1. Upload the object.
1. Update metadata to add a system defined `Cache-Control` key with value `max-age=31536000`.
    - Hat tip to [this article](https://michaelsoolee.com/aws-s3-images-cache-policy/) for the suggestion on reducing S3 costs.

## CNAME magic

You can add a CNAME to your custom domain to do some redirection magic, but it doesn't seem like that works for redirecting to a path with a slash in it. In other words, I could redirect `assets.ansonj.org` to `assets.ansonj.org.s3.us-east-2.amazonaws.com` and use the second HTTP path above. But, I can't redirect anything to the HTTPS path.

Since I prefer my site to be pure HTTPS, I'm not going to deal with CNAME adjustments.

## Image URLs in my Jekyll source

In case I decide to change anything later, I've added an `asset_url_prefix` property to `_config.yml`. Image URLs are then generated using `{{ 'construction.png' | prepend: site.asset_url_prefix }}`.
