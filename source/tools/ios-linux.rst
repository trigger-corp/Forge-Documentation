.. _tools-ios-linux:

Developing iOS apps on Linux
============================

Forge allows the development of iOS apps on Linux without the use
of an OS X machine. To do this you will need a physical iOS device (the iOS
simulator will only run on OS X), and an iOS developer account. In order
to sign your application (which is required to install it onto the device, even
for testing), we provide a remote signing service, which your app will be sent
to, signed and returned as part of the ``forge run ios`` and ``forge package ios``
command.

Setting up Forge to run iOS apps
--------------------------------

Requirements:

- Apple iOS developer account.
- ideviceinstaller installed on the device you are going to develop with
- An iOS device connected via USB to the machine you wish to develop on

In order to sign your application you need to provide us with the following:

- A signing certificate and password
- A provisioning profile

Both of these can be created and managed from the Apple iOS provisioning
portal, which should be accessible from the iOS developer center:
https://developer.apple.com/ios/. The instructions on that site are for OS X,
more detailed instructions for creating a developer certificate on Linux are
included below.

Once these are setup you should be able to use ``forge run ios`` to install the app on your device.

.. _tools-ios-linux-certificate:

Creating a signing certificate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a certificate you need to generate a certificate signing request, in
Linux this can be done by following these steps:

- Run ``openssl req -subj "/CN=Connor Dunn/O=User" -nodes -newkey rsa:2048 -keyout private.key -out request.csr`` replacing ``Connor Dunn`` with your name as registered with your Apple ID.
- On the iOS provisioning portal site choose to create a new certificate and upload the file ``request.csr`` you just created
- Your certificate request should be approved shortly: when it is, download it to the folder you ran the original command, the next steps assume it is called ``ios_development.cer``.
- Run ``openssl x509 -inform der -in ios_development.cer -out certificate.pem`` to convert the certificate format
- Run ``openssl pkcs12 -export -in certificate.pem -inkey private.key -name "iOS Developement Certificate" -out certificate_with_key.p12`` to package the certificate and key. The password you supply will be the one you need to provide to Forge, and prevents unauthorized users from using the certificate if they were to come into possession of the certificate file.
- You should now be able to configure the ``developer_certificate_path`` and ``developer_certificate_password`` in your ``local_config.json`` file.

.. note:: This will leave you with a few files you no longer need, you can safely delete ``request.csr``, ``ios_development.cer`` and ``certificate.pem``. You can also delete ``private.key`` as it is included in the p12 file, if you don't delete it you should store it securely as it can be used to sign with your certificate. You should keep ``certificate_with_key.p12`` to use with Forge, and make sure it and the password are stored securely so others can't sign as you.

Creating a provisioning profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once you have created a certificate you need to create a provisioning profile, this is also done via the iOS provisioning portal website:

- First make sure your device has been added to the provisioning portal, to do this you will need the device identifier (UDID), this can be found by clicking on the device's serial number in iTunes.
- Next create an app id, for development entering ``*`` as a Bundle Identifier is recommended, as it means multiple apps can be signed with a single provisioning profile.
- Finally create a development provisioning profile, making sure you choose the correct app id and enable any devices you wish to be able to test with.
- You can now download and configure the location of your provisioning profile in ``local_config.json``.

.. note:: Provisioning profiles must be recreated if certificates or devices are changed.
