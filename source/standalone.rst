.. _standalone:

Standalone Build API
================================================================================

Although we expect most users to interact with Trigger.io Forge through our
command-line tools and browser-based toolkit, we also offer a standlone build
API to be used programmatically from other environments.

Using this build API, all of your HTML, CSS and JavaScript is uploaded to our
server, along with keys and certificates required for signing purposes. Once
the build is complete, the packages can be downloaded for a limited time
period.

Due to the nature of this API, builds may take longer to complete when compared
to conventional usage. If you are able to use the Trigger tooling, it is
recommended to do so.

API details
--------------------------------------------------------------------------------
An example form is provided here: https://trigger.io/standalone/package

The various fields are described below:

=================== ================================= ======================================
Name                Label                             Expected value
=================== ================================= ======================================
email               email address                     The email address you used to sign up
                                                      to Trigger.io
password            Trigger.io password               The password you gave when you signed
                                                      up for Trigger.io
src_zip             src folder zip                    A zip file containing the contents of
                                                      your src folder. The zip should not
                                                      include the src folder itself; i.e.
                                                      ``config.json`` should be at the root
                                                      of the zip file.
and_keystore        Android keystore                  The file created by the ``keytool``
                                                      utility. See :ref:`releasing-keystore`.
and_storepass       password for Android keystore     The password needed to unlock your
                                                      keystore.
and_keyalias        alias for Android key             The name of the key in your keystore.
and_keypass         password for Android key          The password for the individual key in
                                                      your keystore.
ios_certificate     exported iOS certificate          A .p12 file containing your exported
                                                      iOS developer certificate. On Macs,
                                                      use Keychain Access; for Windows, see
                                                      :ref:`tools-ios-windows-certificate`.
ios_password        password for iOS certificate      Password you used when exporting your
                                                      iOS developer certificate.
ios_profile         iOS provisioning_profile          A .mobileprovision file you have
                                                      downloaded from the iOS provisioning
                                                      portal.
=================== ================================= ======================================

For example usage, see :ref:`standalone-usage`.

.. _standalone-usage:

Usage
--------------------------------------------------------------------------------

To package your app, use the ``/standalone/package`` endpoint::

    > curl \
        --header 'Accept: application/json' \
        --form email=james@trigger.io \
        --form password='my password' \
        --form src_zip=@my_app.zip \
        --form and_keystore=@debug.keystore \
        --form and_storepass=android \
        --form and_keyalias=androiddebugkey \
        --form and_keypass=android \
        -X POST \
        'https://trigger.io/standalone/package'
    {"id": "b0a05ec7-1683-40cc-b80b-716ba5d5067a", "result": "ok"}

This has started the packaging process and given you an ``id`` which you can
use to track the ongoing processing::

    > curl \
        --header 'Accept: application/json' \
        -X GET \
        'https://trigger.io/standalone/track/package/b0a05ec7-1683-40cc-b80b-716ba5d5067a'
    {"info": {"output": ""}, "state": "BUILDING", "id": "38b63a52-a35f-49fe-932a-39db3d82951a", "result": "ok"}

At this point, the build has started; repeated calls to
``/standalone/track/package`` will show when the processing has completed::

    > curl \
        --header 'Accept: application/json' \
        -X GET \
        'https://trigger.io/standalone/track/package/b0a05ec7-1683-40cc-b80b-716ba5d5067a'
    {"info": {
        "files": {
            "android": "https://trigger.io/media/993100fe3aa844c3ad11575e11aeb9fc/demo-1338404961.apk"
        },
        "output": "[   INFO] Forge tools running at version 3.3.0\n ..."
    },
    "state": "SUCCESS",
    "id": "38b63a52-a35f-49fe-932a-39db3d82951a",
    "result": "ok"}

We've formatted the last response for ease of viewing: the ``state`` property
transitioning to ``SUCCESS`` is the key point.

You are able to download the generated files from the URLs specified in the
``files`` hash.
