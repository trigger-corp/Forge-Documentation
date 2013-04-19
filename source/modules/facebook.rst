.. _modules-facebook:

``facebook``: Facebook SDK access
=================================

The ``forge.facebook`` namespace allows access to the `native Facebook SDK <https://developers.facebook.com/docs/sdks/>`_, which provides similar functionality to the `JavaScript SDK <https://developers.facebook.com/docs/reference/javascript/>`_ with the additional feature of supporting SSO (Single Sign-On) between the users Facebook app and your Forge app.

You can see a demo app that makes use of the Facebook module `in this screencast <https://vimeo.com/62372298>`_, with the `code on Github <https://github.com/trigger-corp/scrumptious>`_.

.. important:: Using the Facebook module requires you to have a Facebook account and signup to `Facebook's developer platform <https://developers.facebook.com/>`_. Your relationship with Facebook is separate from your relationship with Trigger.io. If you include the Facebook module in your app, the App Id will report information about app installs and usage to Facebook with that information also made available on your dashboard at https://developers.facebook.com. You must disclose to your users that your app passes the App Id to you and Facebook.

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

.. note:: To use this module you will need to setup your app in Facebook. More information can be found in the Tips section below and at https://developers.facebook.com/

API
---

.. _modules-facebook-authorize:

``facebook.authorize``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Authorize the current user with Facebook, may show a login UI if new permissions are required, or a valid login token is not available (i.e. on first login).

The ``audience`` parameter is only used on iOS (due to differences in the Facebook SDK), but can be passed in on Android to no ill effect. It should be one of:

* "everyone" - by default, your app's updates are public
* "friends" - by default, the user's friends can see your your app's updates
* "only_me" - by default, just the user can see the updates
* "none" - no one can see the updates by default

The success callback will be called with information about the users access_token, you can store and use this token following the Facebook developer guidelines.

.. js:function:: facebook.authorize([permissions, ]success, error)

    :param array permissions: An optional array of permissions to request
    :param array audience: Optional string indicating who should see updates by default
    :param function(token_information) success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur


``facebook.hasAuthorized``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Takes the same options and returns the same data as ``facebook.authorize``, but will not prompt the user for login if required. Used to only log in a user if their interaction is not required.

For more information about the ``audience`` parameter, see the :ref:`modules-facebook-authorize`.

.. js:function:: facebook.hasAuthorized([permissions, ]success, error)

    :param array permissions: An optional array of permissions to request
    :param array audience: Optional string indicating who should see updates by default
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

Note that if the user hits "Cancel" in the dialog, your success callback will
still be called - with ``{}`` as its parameter. This is the behaviour of the
underlying Facebook SDK - for more information, see
http://stackoverflow.com/a/13729707/29903.

.. js:function:: facebook.ui(params, success, error)

    :param object params: Dictionary of paramters, must include ``method``
    :param function(response) success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

Tips
----

For a quick tutorial on setting up your app in Facebook to enable login and open graph API calls see our `demo app build instructions <https://github.com/trigger-corp/scrumptious#preparing-your-own-version-ready-for-deployment>`_

General
~~~~~~~

* To use the Facebook module a Facebook app needs to be created on https://developers.facebook.com/apps. Additionally, on the app configuration page, "Native iOS App" and "Native Android App" need to be enabled, and within each of those sections SSO should also be enabled.
* If a user revokes your apps access, or logs out from the Facebook app you may get OAuth errors returned from API calls, in this situation you should call ``forge.facebook.logout()`` and reauthorize the user.

Android
~~~~~~~

* On Android a hash of the key used to sign your app is required by Facebook to confirm your app should be allowed to access the Facebook API. The easiest way to configure this is to simply start using the Facebook API, any API methods will return an error message which includes the hash and the URL to visit to configure it.

iOS
~~~

* On iOS you must add your applications bundle id to the Facebook developer app settings page. You set a specific bundle id using the package_names module.
