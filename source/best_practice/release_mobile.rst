.. _release_mobile:

Releasing your mobile apps
=============================

After you have finished using ``forge build`` and ``forge run`` to create your app, the next step is to prepare packaged output ready for submission to the app store of your choice.

We help you with this process on the Android and iOS platforms with the ``forge package`` command.

Updating existing apps
--------------------------------------------------------------------------------
If you are using Forge to update an existing app which was not built on the platform, you will need to specify the package name manually, to match the one you had in your old app. To do this, see :ref:`package_names <modules-package_names>` in the configuration documentation.

Android
--------------------------------------------------------------------------------
On Android, use ``forge package android``. You can run ``forge package android --help`` to see all available command line options.

To package Android apps, you need to have created a "keystore" with which to sign your app. You should keep this keystore safe, and observe the normal password safety precautions to prevent others from being to update your own apps.

.. _releasing-keystore:

Creating a keystore
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Full instructions on creating a keystore are available here: http://developer.android.com/guide/publishing/app-signing.html, in the "Obtain a suitable private key" section.

You will need the ``keytool`` command, which is provided by Java.

For example, you might use a command something like this::

    keytool -genkey -alias MY_KEY_NAME \
      -keypass MY_KEY_PASSWORD -validity 20000 \
      -keystore my_keystore.keystore \
      -storepass MY_KEYSTORE_PASSWORD

Here, the uppercase parameters should be replaced with passwords and names of your choosing; the passwords can be the same, if you wish.

That command will create a file called ``my_keystore.keystore`` in the current directory, which we will use in the next step.

Creating an APK
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
After you have created your keystore, you can use ``forge package android`` to produce an APK file, ready for submission to the Android Market.

For example to use the keystore we created in the previous step, we would run something like this::

    forge package android \
      --android.profile.keystore my_keystore.keystore \
      --android.profile.storepass MY_KEYSTORE_PASSWORD \
      --android.profile.keypass MY_KEY_PASSWORD \
      --android.profile.keyalias MY_KEY_NAME

.. note:: For a convenient way to specify and these options in a file, see :ref:`parameters-in-a-file`.

A ``release`` directory has now been created; you will find your release-ready APK file in the ``android`` sub-directory.


iOS
--------------------------------------------------------------------------------
For the iOS devices, creating a packaged IPA file serves two purposes:

#. creating an installable IPA which you can run on your own devices, or send to testers for them to test.
#. creating a IPA which is ready to submit to the App Store.

In the first situation, you need to create and use a development provisioning profile, with all the devices for which the IPA is enabled specified in it.

For the second situation, you need to create and use a release provisioning profile, and your IPA won't run directly on any devices: it is only useful for submission to the App Store.

Therefore, our recommended approach is to use a development wildcard provisioning profile (one that works for any of your apps), right until you're ready to release to the App Store. Only at that point should you switch to your release provisioning profile.

.. _releasing-ios-provisioning_profile:

Creating provisioning profiles
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The Apple developer center has `good documentation <https://developer.apple.com/library/ios/#documentation/ToolsLanguages/Conceptual/DevPortalGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40011159>`_ about creating provisioning profiles, developer certificates and app IDs that should be your main reference.

When working with Forge, you will want to use a development wildcard provisioning profile when in development and testing phases, and a release provisioning profile when submitting to the App Store.

The result of these instructions assume you have your two provisioning profiles stored in the current directory, called ``Development.mobileprovision`` and ``Release.mobileprovision`` respectively.

.. _releasing-ios-ipa:

Creating an IPA
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
After you have created your provisioning profile, use ``forge package ios`` to produce an IPA file.

Depending on your local settings, you may also need to know the exact name of your developer certificate: more on that below.

Assuming you have a provisioning profile called ``Development.mobileprovision`` in the current directory, you would use a command like::

    forge package ios --ios.profile.provisioning-profile Development.mobileprovision

In the ``release`` directory, there will now be an ``ios`` sub-directory, containing your IPA.

The ``forge package ios`` prints out some useful configuration data as it runs, such as the devices this IPA will work with whether you used a Release provisioning profile and the app ID.

Getting the IPA onto your device
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
If you used a development key, you can now use iTunes to install the IPA onto your iPhone or iPod:

* drag the IPA onto the "Library" section in iTunes
* drag the app from the "Apps" section of iTunes onto your connected device

Common problems
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you have more than one developer certificate on your machine, you may hit errors like::

    [  ERROR] Something went wrong that we didn't expect:
    [  ERROR] Failed when running /usr/bin/codesign

Running the ``forge package ios`` command again with the ``-v`` flag for verbose output gives more information::

    [  DEBUG] Running: ('/usr/bin/codesign', '--force', '--preserve-metadata',
      '--entitlements', '/Users/james/../.template/generate_dynamic/dev.entitlements',
      '--sign', 'iPhone Developer', '--resource-rules=/myapp.app/ResourceRules.plist',
      '/myapp.app/')
    [  DEBUG] iPhone Developer: ambiguous (matches
      "iPhone Developer: James Brady (5W89HYT9F3)" and
      "iPhone Developer: James Brady (A639RL926N)" in
      /Users/james/Library/Keychains/login.keychain)

Here, there are two developer certificates for "James Brady" on the machine, and we have to specify the exact certificate to use with::

    forge package ios --provisioning-profile Development.mobileprovision \
      --certificate "iPhone Developer: James Brady (5W89HYT9F3)"

If you encounter errors about a mismatched profile ID, e.g.::

    [ ERROR] Provisioning profile and application ID do not match Provisioning
    profile ID: A8N4D63NB6.io.trigger.forge7faf8ebcb8a111e1910212313d1adcbe
    Application ID: A8N4D63NB6.com.spiffyapp Please see "Preparing your apps
    for app stores" in our docs: http://current-docs.trigger.io/releasing.html#ios

This is because when you created your provisioning profile, you didn't use the
ID automatically generated by Trigger
(``io.trigger.forge7faf8ebcb8a111e1910212313d1adcbe``) in this case.

This is no problem: just update your ``config.json`` to override the package
name to match your provisioning profile. In this example, you'd include::

    "package_names": {
        "ios": "com.spiffyapp"
    }

For more information, see :ref:`modules-package_names`.
