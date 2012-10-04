.. _modules-facebook:

``facebook``: Facebook SDK access
=================================

The ``forge.facebook`` namespace allows access to the native Facebook SDK, which provides similar functionality to the Javascript SDK with the additional feature of supporting SSO (Single Sign-On) between the users Facebook app and your Forge app.

Config
------

The ``facebook`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "facebook": {
                "appid": "123456789012345"
            }
        }
    }

API
---

``facebook.authorize``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Authorize the current user with Facebook, may show a login UI if new permissions are required, or a valid login token is not available (i.e. on first login).

The success callback will be called with information about the users access_token, you can store and use this token following the Facebook developer guidelines.

.. js:function:: facebook.authorize([permissions, ]success, error)

    :param array permissions: An optional array of permissions to request
    :param function(token_information) success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``facebook.logout``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Logout the current user and clear any cached login details.

.. js:function:: facebook.logout(success, error)

    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``facebook.api``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Make a Facebook Graph API call. See https://developers.facebook.com/docs/reference/javascript/FB.api/ for further details.

.. js:function:: facebook.api(path, [[method, ]params, ]success, error)

    :param string path: API path to call, i.e. ``"me/posts"``
    :param string method: Type of request, i.e. ``"GET"``
    :param object params: Additional parameters for the request, i.e. ``{limit: 5}``
    :param function(response) success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``facebook.ui``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Display a Facebook dialog UI. See https://developers.facebook.com/docs/reference/javascript/FB.ui/ for further details.

.. js:function:: facebook.api(params, success, error)

    :param object params: Dictionary of paramters, must include ``method``
    :param function(response) success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

Tips
----

General
~~~~~~~

* To use the Facebook module a Facebook app needs to be created on https://developers.facebook.com/apps. Additionally, on the app configuration page, "Native iOS App" and "Native Android App" need to be enabled, and within each of those sections SSO should also be enabled.
* If a user revokes your apps access, or logs out from the Facebook app you may get OAuth errors returned from API calls, in this situation you should call ``forge.facebook.logout()`` and reauthorize the user.

Android
~~~~~~~

* On Android a hash of the key used to sign your app is required by Facebook to confirm your app should be allowed to access the Facebook API. The easiest way to configure this is to simply start using the Facebook API, any API methods will return an error message which includes the hash and the URL to visit to configure it.

