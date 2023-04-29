#yazılım #python

-   Documentation version: **3.2**

# [Managing static files (e.g. images, JavaScript, CSS)](#managing-static-files-e-g-images-javascript-css "Permalink to this headline")

Websites generally need to serve additional files such as images, JavaScript, or CSS. In Django, we refer to these files as “static files”. Django provides [`django.contrib.staticfiles`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#module-django.contrib.staticfiles "django.contrib.staticfiles: An app for handling static files.") to help you manage them.

This page describes how you can serve these static files.

## [Configuring static files](#configuring-static-files "Permalink to this headline")

1.  Make sure that `django.contrib.staticfiles` is included in your [`INSTALLED_APPS`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-INSTALLED_APPS "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-INSTALLED_APPS").
    
2.  In your settings file, define [`STATIC_URL`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_URL "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_URL"), for example:
    
```python
STATIC_URL = '/static/'
```
    
3.  In your templates, use the [`static`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/templates/builtins/#std:templatetag-static "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/templates/builtins/#std:templatetag-static") template tag to build the URL for the given relative path using the configured [`STATICFILES_STORAGE`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATICFILES_STORAGE "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATICFILES_STORAGE").
    
```python
{% load static %}
<img src="{% static 'my_app/example.jpg' %}" alt="My image">
```
    
4.  Store your static files in a folder called `static` in your app. For example `my_app/static/my_app/example.jpg`.
    

Serving the files

In addition to these configuration steps, you’ll also need to actually serve the static files.

During development, if you use [`django.contrib.staticfiles`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#module-django.contrib.staticfiles "django.contrib.staticfiles: An app for handling static files."), this will be done automatically by [`runserver`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/django-admin/#django-admin-runserver "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/django-admin/#django-admin-runserver") when [`DEBUG`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-DEBUG "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-DEBUG") is set to `True` (see [`django.contrib.staticfiles.views.serve()`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#django.contrib.staticfiles.views.serve "django.contrib.staticfiles.views.serve")).

This method is **grossly inefficient** and probably **insecure**, so it is **unsuitable for production**.

See [Deploying static files](https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/ "https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/") for proper strategies to serve static files in production environments.

Your project will probably also have static assets that aren’t tied to a particular app. In addition to using a `static/` directory inside your apps, you can define a list of directories ([`STATICFILES_DIRS`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATICFILES_DIRS "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATICFILES_DIRS")) in your settings file where Django will also look for static files. For example:

```python
STATICFILES_DIRS = [
    BASE_DIR / "static",
    '/var/www/static/',
]
```

See the documentation for the [`STATICFILES_FINDERS`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATICFILES_FINDERS "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATICFILES_FINDERS") setting for details on how `staticfiles` finds your files.

Static file namespacing

Now we _might_ be able to get away with putting our static files directly in `my_app/static/` (rather than creating another `my_app` subdirectory), but it would actually be a bad idea. Django will use the first static file it finds whose name matches, and if you had a static file with the same name in a _different_ application, Django would be unable to distinguish between them. We need to be able to point Django at the right one, and the best way to ensure this is by _namespacing_ them. That is, by putting those static files inside _another_ directory named for the application itself.

You can namespace static assets in [`STATICFILES_DIRS`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATICFILES_DIRS "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATICFILES_DIRS") by specifying [prefixes](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#staticfiles-dirs-prefixes "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#staticfiles-dirs-prefixes").

## Serving static files during development[¶](#serving-static-files-during-development "Permalink to this headline")

If you use [`django.contrib.staticfiles`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#module-django.contrib.staticfiles "django.contrib.staticfiles: An app for handling static files.") as explained above, [`runserver`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/django-admin/#django-admin-runserver "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/django-admin/#django-admin-runserver") will do this automatically when [`DEBUG`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-DEBUG "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-DEBUG") is set to `True`. If you don’t have `django.contrib.staticfiles` in [`INSTALLED_APPS`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-INSTALLED_APPS "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-INSTALLED_APPS"), you can still manually serve static files using the [`django.views.static.serve()`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/views/#django.views.static.serve "django.views.static.serve") view.

This is not suitable for production use! For some common deployment strategies, see [Deploying static files](https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/ "https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/").

For example, if your [`STATIC_URL`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_URL "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_URL") is defined as `/static/`, you can do this by adding the following snippet to your urls.py:

```python
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    # ... the rest of your URLconf goes here ...
] + static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```

Note

This helper function works only in debug mode and only if the given prefix is local (e.g. `/static/`) and not a URL (e.g. `http://static.example.com/`).

Also this helper function only serves the actual [`STATIC_ROOT`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_ROOT "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_ROOT") folder; it doesn’t perform static files discovery like [`django.contrib.staticfiles`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#module-django.contrib.staticfiles "django.contrib.staticfiles: An app for handling static files.").

## Serving files uploaded by a user during development[¶](#serving-files-uploaded-by-a-user-during-development "Permalink to this headline")

During development, you can serve user-uploaded media files from [`MEDIA_ROOT`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-MEDIA_ROOT "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-MEDIA_ROOT") using the [`django.views.static.serve()`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/views/#django.views.static.serve "django.views.static.serve") view.

This is not suitable for production use! For some common deployment strategies, see [Deploying static files](https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/ "https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/").

For example, if your [`MEDIA_URL`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-MEDIA_URL "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-MEDIA_URL") is defined as `/media/`, you can do this by adding the following snippet to your [`ROOT_URLCONF`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-ROOT_URLCONF "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-ROOT_URLCONF"):

```python
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    # ... the rest of your URLconf goes here ...
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

Note

This helper function works only in debug mode and only if the given prefix is local (e.g. `/media/`) and not a URL (e.g. `http://media.example.com/`).

## Testing[¶](#testing "Permalink to this headline")

When running tests that use actual HTTP requests instead of the built-in testing client (i.e. when using the built-in [`LiveServerTestCase`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../topics/testing/tools/#django.test.LiveServerTestCase "django.test.LiveServerTestCase")) the static assets need to be served along the rest of the content so the test environment reproduces the real one as faithfully as possible, but `LiveServerTestCase` has only very basic static file-serving functionality: It doesn’t know about the finders feature of the `staticfiles` application and assumes the static content has already been collected under [`STATIC_ROOT`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_ROOT "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_ROOT").

Because of this, `staticfiles` ships its own [`django.contrib.staticfiles.testing.StaticLiveServerTestCase`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#django.contrib.staticfiles.testing.StaticLiveServerTestCase "django.contrib.staticfiles.testing.StaticLiveServerTestCase"), a subclass of the built-in one that has the ability to transparently serve all the assets during execution of these tests in a way very similar to what we get at development time with `DEBUG = True`, i.e. without having to collect them using [`collectstatic`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#django-admin-collectstatic "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#django-admin-collectstatic") first.

## Deployment[¶](#deployment "Permalink to this headline")

[`django.contrib.staticfiles`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#module-django.contrib.staticfiles "django.contrib.staticfiles: An app for handling static files.") provides a convenience management command for gathering static files in a single directory so you can serve them easily.

1.  Set the [`STATIC_ROOT`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_ROOT "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_ROOT") setting to the directory from which you’d like to serve these files, for example:
    
```python
STATIC_ROOT = "/var/www/example.com/static/"
```
    
2.  Run the [`collectstatic`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#django-admin-collectstatic "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#django-admin-collectstatic") management command:
    
```bash
$ python manage.py collectstatic
```
    
    This will copy all files from your static folders into the [`STATIC_ROOT`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_ROOT "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_ROOT") directory.
    
3.  Use a web server of your choice to serve the files. [Deploying static files](https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/ "https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/") covers some common deployment strategies for static files.
    

## [Learn more](#learn-more "Permalink to this headline")

This document has covered the basics and some common usage patterns. For complete details on all the settings, commands, template tags, and other pieces included in [`django.contrib.staticfiles`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#module-django.contrib.staticfiles "django.contrib.staticfiles: An app for handling static files."), see [the staticfiles reference](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/ "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/").

[Overriding templates](https://docs.djangoproject.com/en/3.2/howto/static-files/../overriding-templates/ "https://docs.djangoproject.com/en/3.2/howto/static-files/../overriding-templates/")

[Deploying static files](https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/ "https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/")

—_____________________________________—

-   Belge sürümü: **3.2**

# [Statik dosyaları yönetme (ör. resimler, JavaScript, CSS)](#managing-static-files-e-g-images-javascript-css "Bu başlığa kalıcı bağlantı")

Web sitelerinin genellikle resimler, JavaScript veya CSS gibi ek dosyalar sunması gerekir. Django'da bu dosyalara "statik dosyalar" diyoruz. Django, [`django.contrib.staticfiles`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#module-django.contrib "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#module-django.contrib") sağlar .staticfiles "Django.contrib.staticfiles: Statik dosyaları işlemek için bir uygulama.") onları yönetmenize yardımcı olur.

Bu sayfa, bu statik dosyaları nasıl sunabileceğinizi açıklar.

## [Statik dosyaları yapılandırma](#configuring-static-files "Bu başlığa kalıcı bağlantı")

1.  "Django.contrib.staticfiles" dosyasının [`INSTALLED_APPS`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/ "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/") içinde bulunduğundan emin olun. settings/#std:ayar-INSTALLED_APPS).
    
2.  Ayarlar dosyanızda [`STATIC_URL`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_URL "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_URL") öğesini tanımlayın ), Örneğin:
    
```python
STATIC_URL = '/static/'
```
    
3.  Şablonlarınızda [`static`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/templates/builtins/#std:templatetag "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/templates/builtins/#std:templatetag") kullanın yapılandırılmış [`STATICFILES_STORAGE`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref") kullanarak verilen göreli yol için URL oluşturmak için -static) şablon etiketi /settings/#std:ayar-STATICFILES_STORAGE).
    
    ```
    {% yük statik %}
    <img src="{% static 'my_app/example.jpg' %}" alt="Resimim">
    ```
    
4.  Statik dosyalarınızı uygulamanızda 'statik' adlı bir klasörde saklayın. Örneğin, "my_app/static/my_app/example.jpg".
    

Dosyaları sunmak

Bu yapılandırma adımlarına ek olarak, aslında statik dosyaları da sunmanız gerekecektir.

Geliştirme sırasında [`django.contrib.staticfiles`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#module "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#module") kullanırsanız -django.contrib.staticfiles "Django.contrib.staticfiles: Statik dosyaları işlemek için bir uygulama."), bu otomatik olarak [`runserver`](https://docs.djangoproject.com/en/3.2/howto "https://docs.djangoproject.com/en/3.2/howto") tarafından yapılacaktır. /static-files/../../ref/django-admin/#django-admin-runserver) [`DEBUG`](https://docs.djangoproject.com/en/3.2/howto/static-files "https://docs.djangoproject.com/en/3.2/howto/static-files") olduğunda /../../ref/settings/#std:setting-DEBUG) "True" olarak ayarlandığında (bkz. [`django.contrib.staticfiles.views.serve()`]([https://docs.djangoproject](https://docs.djangoproject "https://docs.djangoproject"). com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#django.contrib.staticfiles.views.serve "django.contrib.staticfiles.views.serve")).

Bu yöntem **oldukça verimsizdir** ve muhtemelen **güvensizdir**, dolayısıyla **üretim için uygun değildir**.

Üretim ortamlarında statik dosyalar sunmaya yönelik uygun stratejiler için [Statik dosyaları dağıtma](https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/ "https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/") bölümüne bakın.

Projeniz muhtemelen belirli bir uygulamaya bağlı olmayan statik varlıklara da sahip olacaktır. Uygulamalarınızın içinde bir "static/" dizini kullanmaya ek olarak, bir dizin listesi tanımlayabilirsiniz ([`STATICFILES_DIRS`]([https://docs.djangoproject.com/en/3.2/howto/static-files/](https://docs.djangoproject.com/en/3.2/howto/static-files/ "https://docs.djangoproject.com/en/3.2/howto/static-files/").. /../ref/settings/#std:setting-STATICFILES_DIRS)) ayarlar dosyanızda Django'nun statik dosyaları da arayacaktır. Örneğin:

```
STATICFILES_DIRS = [
    BASE_DIR / "statik",
    '/var/www/statik/',
]
```

için [`STATICFILES_FINDERS`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATICFILES_FINDERS "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATICFILES_FINDERS") ayarına ilişkin belgelere bakın. "staticfiles"ın dosyalarınızı nasıl bulduğuna ilişkin ayrıntılar.

Statik dosya ad alanı

Artık statik dosyalarımızı (başka bir 'my_app' alt dizini oluşturmak yerine) doğrudan 'my_app/static/' içine koymaktan _kurtulabiliriz_, ancak bu aslında kötü bir fikir olurdu. Django bulduğu ve adı eşleşen ilk statik dosyayı kullanır ve _farklı_ bir uygulamada aynı ada sahip statik bir dosyanız olsaydı, Django bunları ayırt edemezdi. Django'yu doğru yere yönlendirebilmemiz gerekiyor ve bunu sağlamanın en iyi yolu onları _isim-aralığı_ kullanmaktır. Yani, bu statik dosyaları uygulamanın kendisi için adlandırılan _başka bir_ dizine koyarak.

Statik varlıkları [`STATICFILES_DIRS`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATICFILES_DIRS "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATICFILES_DIRS") içinde adlandırabilirsiniz. [önekler](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#staticfiles-dirs-prefixes "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#staticfiles-dirs-prefixes").

## Geliştirme sırasında statik dosyalar sunma[¶](#serving-static-files-development "Bu başlığa kalıcı bağlantı")

[`Django.contrib.staticfiles`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#module-django "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#module-django") kullanıyorsanız. contrib.staticfiles "Django.contrib.staticfiles: Statik dosyaları işlemek için bir uygulama.") yukarıda açıklandığı gibi, [`runserver`]([https://docs.djangoproject.com/en/3.2/howto/static-files/](https://docs.djangoproject.com/en/3.2/howto/static-files/ "https://docs.djangoproject.com/en/3.2/howto/static-files/"). ./../ref/django-admin/#django-admin-runserver), [`DEBUG`]([https://docs.djangoproject.com/en/3.2/howto/static-files/](https://docs.djangoproject.com/en/3.2/howto/static-files/ "https://docs.djangoproject.com/en/3.2/howto/static-files/"). ./../ref/settings/#std:setting-DEBUG) "Doğru" olarak ayarlandı. [`INSTALLED_APPS`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/ "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/") içinde `django.contrib.staticfiles` yoksa #std:setting-INSTALLED_APPS), yine de [`django.views.static.serve()`](https://docs.djangoproject.com/en/3.2/howto/static-files "https://docs.djangoproject.com/en/3.2/howto/static-files") kullanarak statik dosyaları manuel olarak sunabilirsiniz. /../../ref/views/#django.views.static.serve "Django.views.static.serve") görünümü.

Bu, üretim kullanımı için uygun değildir! Bazı yaygın dağıtım stratejileri için bkz. [Statik dosyaları dağıtma](https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/ "https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/").

Örneğin, [`STATIC_URL`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_URL "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_URL") tanımlıysa `/static/` olarak, urls.py'nize aşağıdaki parçacığı ekleyerek bunu yapabilirsiniz:

```
django.conf içe aktarma ayarlarından
django.conf.urls.static'ten içe aktarma statik

url kalıpları = [
    # ... URLconf'unuzun geri kalanı buraya gelir ...
] + statik(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```

Not

Bu yardımcı işlev yalnızca hata ayıklama modunda ve yalnızca belirtilen önek yerelse (ör. `/static/`) ve bir URL değil (ör.

Ayrıca bu yardımcı işlev yalnızca gerçek [`STATIC_ROOT`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_ROOT "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_ROOT") sunar. ) dosya; [`django.contrib.staticfiles`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles") gibi statik dosya keşfi gerçekleştirmez /#module-django.contrib.staticfiles "django.contrib.staticfiles: Statik dosyaları işlemek için bir uygulama.").

## Geliştirme sırasında bir kullanıcı tarafından yüklenen dosyaların sunulması[¶](#serving-files-uploaded-by-a-a-development "Bu başlığa kalıcı bağlantı")

Geliştirme sırasında, [`MEDIA_ROOT`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std") adresinden kullanıcı tarafından yüklenen medya dosyalarını sunabilirsiniz. :setting-MEDIA_ROOT) [`django.views.static.serve()`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/views "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/views") kullanarak /#django.views.static.serve "Django.views.static.serve") görünümü.

Bu, üretim kullanımı için uygun değildir! Bazı yaygın dağıtım stratejileri için bkz. [Statik dosyaları dağıtma](https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/ "https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/").

Örneğin, [`MEDIA_URL`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-MEDIA_URL "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-MEDIA_URL") tanımlıysa `/media/` olarak, [`ROOT_URLCONF`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ "https://docs.djangoproject.com/en/3.2/howto/static-files/../../") dizininize aşağıdaki snippet'i ekleyerek bunu yapabilirsiniz. ref/settings/#std:setting-ROOT_URLCONF):

```
django.conf içe aktarma ayarlarından
django.conf.urls.static'ten içe aktarma statik

url kalıpları = [
    # ... URLconf'unuzun geri kalanı buraya gelir ...
] + statik(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

Not

Bu yardımcı işlev yalnızca hata ayıklama modunda ve yalnızca belirtilen önek yerelse (ör. `/media/`) ve bir URL değil (ör. `http://media.example.com/`) çalışır.

## Test[¶](#testing "Bu başlığa kalıcı bağlantı")

Yerleşik test istemcisi yerine gerçek HTTP isteklerini kullanan testleri çalıştırırken (yani yerleşik [`LiveServerTestCase`](https://docs.djangoproject.com/en/3.2/howto/static-files/ "https://docs.djangoproject.com/en/3.2/howto/static-files/") kullanırken ../../topics/testing/tools/#django.test.LiveServerTestCase "django.test.LiveServerTestCase")) statik varlıkların içeriğin geri kalanı boyunca sunulması gerekir, böylece test ortamı gerçek olanı aslına uygun olarak yeniden üretir ancak 'LiveServerTestCase' yalnızca çok temel statik dosya sunma işlevine sahiptir: 'staticfiles' uygulamasının bulucu özelliğini bilmez ve statik içeriğin ['STATIC_ROOT'] altında toplandığını varsayar (https: [//docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_ROOT](//docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_ROOT "//docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_ROOT")).

Bu nedenle, "staticfiles" kendi [`django.contrib.staticfiles.testing.StaticLiveServerTestCase'](https://docs.djangoproject.com/en/3.2/howto/static-files/../../) dosyasını gönderir. ref/contrib/staticfiles/#django.contrib.staticfiles.testing.StaticLiveServerTestCase "django.contrib.staticfiles.testing.StaticLiveServerTestCase"), yürütme sırasında tüm varlıklara şeffaf bir şekilde hizmet etme yeteneğine sahip yerleşik sınıfın bir alt sınıfıdır. bu testler, geliştirme sırasında` DEBUG = True `ile elde ettiğimize çok benzer, yani onları [`collectstatic`]([https://docs.djangoproject.com/en/3.2/howto/](https://docs.djangoproject.com/en/3.2/howto/ "https://docs.djangoproject.com/en/3.2/howto/") kullanarak toplamak zorunda kalmadan) static-files/../../ref/contrib/staticfiles/#django-admin-collectstatic) önce.

## Dağıtım[¶](#deployment "Bu başlığa kalıcı bağlantı")

[`django.contrib.staticfiles`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#module-django.contrib.staticfiles "Django.contrib.staticfiles: Statik dosyaları işlemek için bir uygulama."), statik dosyaları kolayca sunabilmeniz için tek bir dizinde toplamak için bir kolaylık yönetimi komutu sağlar.

1.  [`STATIC_ROOT`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_ROOT "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std:setting-STATIC_ROOT") ayarını şu şekilde yapın: bu dosyaları sunmak istediğiniz dizin, örneğin:
    
    ```
    STATIC_ROOT = "/var/www/example.com/static/"
    ```
    
2.  [`collectstatic`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#django-admin-collectstatic "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/#django-admin-collectstatic") yönetimini çalıştırın emretmek:
    
    ```
    $ python manager.py toplama statik
    ```
    
    Bu, statik klasörlerinizdeki tüm dosyaları [`STATIC_ROOT`](https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std "https://docs.djangoproject.com/en/3.2/howto/static-files/../../ref/settings/#std") içine kopyalayacaktır: ayar-STATIC_ROOT) dizini.
    
3.  Dosyaları sunmak için seçtiğiniz bir web sunucusunu kullanın. [Statik dosyaları dağıtma](https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/ "https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/") statik dosyalar için bazı yaygın dağıtım stratejilerini kapsar.
    

## Daha fazla bilgi edinin[¶](#learn-more "Bu başlığa kalıcı bağlantı")

Bu belge, temel bilgileri ve bazı yaygın kullanım kalıplarını kapsamaktadır. Tüm ayarlar, komutlar, şablon etiketleri ve [`django.contrib.staticfiles`]([https://docs.djangoproject.com/en/3.2/howto/static-files/](https://docs.djangoproject.com/en/3.2/howto/static-files/ "https://docs.djangoproject.com/en/3.2/howto/static-files/").. /../ref/contrib/staticfiles/#module-django.contrib.staticfiles "Django.contrib.staticfiles: Statik dosyaları işlemek için bir uygulama."), bkz. [staticfiles referansı]([https://docs.djangoproject](https://docs.djangoproject "https://docs.djangoproject"). com/en/3.2/howto/static-files/../../ref/contrib/staticfiles/).

[Şablonları geçersiz kılma](https://docs.djangoproject.com/en/3.2/howto/static-files/../overriding-templates/ "https://docs.djangoproject.com/en/3.2/howto/static-files/../overriding-templates/")

[Statik dosyaları dağıtma](https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/ "https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/")