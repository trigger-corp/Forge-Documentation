.. _user-interface:

User Interface: ``forge.ui``
==================================================================================
Allows you to modify the current user interface. **NB** This module is not finalised, and is subject to change.


.. ``resetStyle``
	~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
	js:function:: ui.resetStyle()

	Applies css reset styling to display things similarly across all browsers.

	``formStyle``
	~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
	js:function:: ui.formStyle()

	Applies css reset styling to form elements.

	``createPage``
	~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
	js:function:: ui.createPage(options)

		:param object options: object containing
			content: HTML content to add to the page
			header: HTML header to append to the page
			footer: HTML footer to append to the page
		:return object: object with the following functions:
			show: display the newly created content in the page
			destroy: remove the content

	Create new content on the current page.