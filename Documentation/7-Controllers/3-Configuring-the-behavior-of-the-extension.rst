.. include:: ../Includes.txt

Configuring the behavior of the extension
================================================================================================

Not all organizations are to be displayed in our example extensions,
but just the ones belonging to a certain status (like e.g. internal,
external, non-member). In the TypoScript template of our page we therefore
establish an option :class:`allowedStates` under the path
:class:`tx_sjroffers.settings`:

``plugin.tx_sjroffers {``

``settings {``

``allowedStates = 1,2``

``}``

``}``

Extbase makes the settings inside of the path
:class:`plugin.tx_sjroffers.settings` available as an array in
the class variable :class:`$this->settings`. Our Action
thus looks like this:

``public function indexAction() {``

``$this->view->assign('organizations',
$this->organizationRepository->findByStates(GeneralUtility::intExplode(',',$this->settings['allowedStates'])));``

``...``

``}``

In the :class:`OrganizationRepository`, we implemented a
Method :class:`findByStates()`, which we do not further
investigate here (see more in chapter 6, section "Implement individual
database queries"). The Method expects an array containing the allowed
states. We generate it from the comma seperated list using the TYPO3 API
function :class:`GeneralUtility::intExplode()`. We then pass on the
returned choice of organizations to the view, just as we are used to
do.

.. tip::

	Of course we could also have passed the comma seperated list
	directly to the Method :class:`findByStates()`. We do
	recommend, though, to prepare all parameter coming from outside
	(settings, form input) before passing them on to the two other
	components Model and View.
	</tip>In this chapter you've learned how to set the Objects of your domain
	in motion and how to control the flow of a page visit. You now are able to
	realize the two components *Model* and
	*Controller* of the MVC paradigm inside your extension.
	In the following chapter, we will address the third component, the
	*View*. We'll present the substantial scope of the
	template engine Fluid.