# djangowithawsstorage

Django S3 File Browser
Info:	S3 File Browser For Django.
Author:	Mehmet KAYKISIZ (http://github.com/mkaykisiz)
Django S3 File Browser is a simple web-based object browser for cloud-based blob datastores. Just add as an application to a Django project, add some settings, and you'll be able to browse cloud containers and implied subdirectories, as well as view / download objects.

Be sure to check out the following project resources:

GitHub page.
Quick Start
First, download library:

pip install djangoS3Browser
Add djangoS3Browser to INSTALLED_APPS:

INSTALLED_APPS = [
    ...
    'djangoS3Browser',
]
Then, make the necessary configurations for the Boto 3 library:

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
Next, do to Django S3 File Browser configuration:

S3_BROWSER_SETTINGS = "djangoS3Browser"
Next, add to TEMPLATES['OPTIONS'] in settings.py:

'libraries': {
    's3-load': 'djangoS3Browser.templatetags.s3tags',
},
Then, add to urls.py:

url(r'^' + settings.S3_BROWSER_SETTINGS + '/', include('djangoS3Browser.s3_browser.urls')),
Then, add this to the top of the page you want to add:

{% load s3tags %}
Finally, add this to the content of the page you want to add:

{% load_s3 %}
