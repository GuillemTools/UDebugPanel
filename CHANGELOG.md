# Changelog

## v1.3.0
- Renamed AddButtonListSelector to AddButtonListInput.
- Renamed AddButtonElementListSelector to AddButtonListSelector.
- Added new AddButtonStringSelector. 
- Added UDebugPanel.Popups.AddActionsContainerPopup.
- Added DebugPanel.Popups.AddConsolePopup.

## v1.2.4
- Removed test file that could cause issues when building.

## v1.2.3
- Improved console popup and added an example on how to use it.
- Fixed exception when there is not an EventSystem.current.

## v1.2.2
- Fixed InvalidOperationException: Collection was modified when opening the panel.
- Fixed exception when popups stack was not cleared.

## v1.2.1
- On editor, focus on text input on string input popup and actions popup.

## v1.2.0
- Added previous section functionality.

## v1.1.3
- Added support for Enter Play Mode Options - Reload Domain disabled.
- Added methods for build stripping: UDebugPanelBuildUtils.StripFromBuild and UDebugPanelBuildUtils.UnstripFromBuild.

## v1.1.2
- Added Welcome window that appears the first time you import the asset.

## v1.1.1 
- Improved Game Example.

## v1.1.0
- Added UDebugPanel.AddGlobalOptionsObjects() that gathers all the static classes that have the [DebugActionsObject] attribute, and creates debug actions from them.
- Added [ShowAsDebugAction] for showing private properties when automatically creating debug actions from reflection.
- Added and [DontShowAsDebugAction] for hiding public properties when automatically creating debug actions from reflection.

## v1.0.0
Initial Release - Hurray!
