# Django File Browser implementation with AWS S3 Storage

Django S3 File Browser is a web-based object browser for cloud-based blob datastores. 

You must add this as an application to a Django project, apply settings, and you'll be able to browse cloud containers and implied subdirectories, as well as view / download objects.

## Quick Start

First, download library:

```
pip install djangoS3Browser
```

Add djangoS3Browser to INSTALLED_APPS:

```
INSTALLED_APPS = [
    ...
    'djangoS3Browser',
]
```

Then, make the necessary configurations for the Boto 3 library:

```
AWS_ACCESS_KEY_ID = "AWS_ACCESS_KEY_ID"
AWS_SECRET_ACCESS_KEY = "AWS_SECRET_ACCESS_KEY"
AWS_STORAGE_BUCKET_NAME = "AWS_STORAGE_BUCKET_NAME"
AWS_AUTO_CREATE_BUCKET = True
AWS_QUERYSTRING_AUTH = False

# AWS cache settings, don't change unless you know what you're doing:
AWS_EXPIRY = 60 * 60 * 24 * 7

# Revert the following and use str after the above-mentioned bug is fixed in
# either django-storage-redux or boto
control = 'max-age=%d, s-maxage=%d, must-revalidate' % (AWS_EXPIRY, AWS_EXPIRY)
AWS_HEADERS = {
    'Cache-Control': bytes(control, encoding='latin-1')
}
```


