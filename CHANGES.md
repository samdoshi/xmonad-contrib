# Change Log / Release Notes

## 0.14 (Not Yet)

### Breaking Changes

  * `XMonad.Actions.GridSelect`

    - Added field `gs_bordercolor` to `GSConfig` to specify border color.

### Bug Fixes and Minor Changes

  * `XMonad.Hooks.EwmhDesktops.fullscreenEventHook`
  
    - Remove borders when fullscreen.

  * `XMonad.Actions.GridSelect`

    - The vertical centring of text in each cell has been improved.

  * `XMonad.Util.WindowProperties`

    - Added the ability to test if a window has a tag from
      `XMonad.Actions.TagWindows`

  * `XMonad.Layout.Magnifier`

    - Handle `IncMasterN` messages.

## 0.13 (February 10, 2017)

### Breaking Changes

  * The type of `completionKey` (of `XPConfig` record) has been
    changed from `KeySym` to `(KeyMask, KeySym)`. The default value
    for this is still bound to the `Tab` key.

  * New constructor `CenteredAt Rational Rational` added for
    `XMonad.Prompt.XPPosition`.

  * `XMonad.Prompt` now stores its history file in the XMonad cache
    directory in a file named `prompt-history`.

### New Modules

  * `XMonad.Layout.SortedLayout`

    A new LayoutModifier that sorts a given layout by a list of
    properties. The order of properties in the list determines
    the order of windows in the final layout. Any unmatched windows
    go to the end of the order.

  * `XMonad.Prompt.Unicode`

    A prompt to search a unicode character by its name, and put it into the
    clipboard.

  * `XMonad.Util.Ungrab`

    Release xmonad's keyboard and pointer grabs immediately, so
    screen grabbers and lock utilities, etc. will work. Replaces
    the short sleep hackaround.

  * `XMonad.Util.Loggers.NamedScratchpad`

    A collection of Loggers (see `XMonad.Util.Loggers`) for NamedScratchpads
    (see `XMonad.Util.NamedScratchpad`).

  * `XMonad.Util.NoTaskbar`

    Utility function and `ManageHook` to mark a window to be ignored by
    EWMH taskbars and pagers. Useful for `NamedScratchpad` windows, since
    you will usually be taken to the `NSP` workspace by them.

### Bug Fixes and Minor Changes

  * `XMonad.Hooks.ManageDocks`,

    - Fix a very annoying bug where taskbars/docs would be
      covered by windows.

    - Also fix a bug that caused certain Gtk and Qt application to
      have issues displaying menus and popups.

  * `XMonad.Layout.LayoutBuilder`

    Merge all functionality from `XMonad.Layout.LayoutBuilderP` into
    `XMonad.Layout.LayoutBuilder`.

  * `XMonad.Actions.WindowGo`

    - Fix `raiseNextMaybe` cycling between 2 workspaces only.

  * `XMonad.Actions.UpdatePointer`

    - Fix bug when cursor gets stuck in one of the corners.

  * `XMonad.Actions.Submap`

    Establish pointer grab to avoid freezing X, when button press occurs after
    submap key press.  And terminate submap at button press in the same way,
    as we do for wrong key press.

  * `XMonad.Actions.DynamicProjects`

    - Switching away from a dynamic project that contains no windows
      automatically deletes that project's workspace.

      The project itself was already being deleted, this just deletes
      the workspace created for it as well.

    - Added function to change the working directory (`changeProjectDirPrompt`)

    - All of the prompts are now multiple mode prompts.  Try using the
      `changeModeKey` in a prompt and see what happens!

## 0.12 (December 14, 2015)

### Breaking Changes

  * `XMonad.Actions.UpdatePointer.updatePointer` arguments were
    changed. This allows including aspects of both of the
    `TowardsCentre` and `Relative` methods. To keep the same behavior,
    replace the entry in the left column with the entry on the right:

    | < 0.12                              |   >= 0.12                        |
    |-------------------------------------|----------------------------------|
    | `updatePointer Nearest`             | `updatePointer (0.5, 0.5) (1,1)` |
    | `updatePointer (Relative x y)`      | `updatePointer (x,y) (0,0)`      |
    | `updatePointer (TowardsCentre x y)` | `updatePointer (0.5,0.5) (x,y)`  |

### New Modules

  * `XMonad.Actions.AfterDrag`

    Perform an action after the current mouse drag is completed.

  * `XMonad.Actions.DynamicProjects`

    Imbues workspaces with additional features so they can be treated
    as individual project areas.

  * `XMonad.Actions.LinkWorkspaces`

    Provides bindings to add and delete links between workspaces. It
    is aimed at providing useful links between workspaces in a
    multihead setup. Linked workspaces are viewed at the same time.

  * `XMonad.Config.Bepo`

    This module fixes some of the keybindings for the francophone
    among you who use a BEPO keyboard layout. Based on
    `XMonad.Config.Azerty`

  * `XMonad.Config.Dmwit`

    Daniel Wagner's configuration.

  * `XMonad.Config.Mate`

    This module provides a config suitable for use with the MATE
    desktop environment.

  * `XMonad.Config.Prime`

    A draft of a brand new config syntax for xmonad.

  * `XMonad.Hooks.DynamicProperty`

    Module to apply a `ManageHook` to an already-mapped window when a
    property changes. This would commonly be used to match browser
    windows by title, since the final title will only be set after (a)
    the window is mapped, (b) its document has been loaded, (c) all
    load-time scripts have run.

  * `XMonad.Hooks.ManageDebug`

    A `manageHook` and associated `logHook` for debugging `ManageHook`s.
    Simplest usage: wrap your xmonad config in the `debugManageHook`
    combinator.  Or use `debugManageHookOn` for a triggerable version,
    specifying the triggering key sequence in `XMonad.Util.EZConfig`
    syntax. Or use the individual hooks in whatever way you see fit.

  * `XMonad.Hooks.WallpaperSetter`

    Log hook which changes the wallpapers depending on visible
    workspaces.

  * `XMonad.Hooks.WorkspaceHistory`

    Keeps track of workspace viewing order.

  * `XMonad.Layout.AvoidFloats`

    Find a maximum empty rectangle around floating windows and use
    that area to display non-floating windows.

  * `XMonad.Layout.BinarySpacePartition`

    Layout where new windows will split the focused window in half,
    based off of BSPWM.

  * `XMonad.Layout.Dwindle`

    Three layouts: The first, `Spiral`, is a reimplementation of
    `XMonad.Layout.Spiral.spiral` with, at least to me, more intuitive
    semantics.  The second, `Dwindle`, is inspired by a similar layout
    in awesome and produces the same sequence of decreasing window
    sizes as Spiral but pushes the smallest windows into a screen
    corner rather than the centre.  The third, `Squeeze` arranges all
    windows in one row or in one column, with geometrically decreasing
    sizes.

  * `XMonad.Layout.Hidden`

    Similar to `XMonad.Layout.Minimize` but completely removes windows
    from the window set so `XMonad.Layout.BoringWindows` isn't
    necessary.  Perfect companion to `XMonad.Layout.BinarySpacePartition`
    since it can be used to move windows to another part of the BSP tree.

  * `XMonad.Layout.IfMax`

    Provides `IfMax` layout, which will run one layout if there are
    maximum `N` windows on workspace, and another layout, when number
    of windows is greater than `N`.

  * `XMonad.Layout.PerScreen`

    Configure layouts based on the width of your screen; use your
    favorite multi-column layout for wide screens and a full-screen
    layout for small ones.

  * `XMonad.Layout.Stoppable`

    This module implements a special kind of layout modifier, which when
    applied to a layout, causes xmonad to stop all non-visible processes.
    In a way, this is a sledge-hammer for applications that drain power.
    For example, given a web browser on a stoppable workspace, once the
    workspace is hidden the web browser will be stopped.

  * `XMonad.Prompt.ConfirmPrompt`

    A module for setting up simple confirmation prompts for
    keybindings.

  * `XMonad.Prompt.Pass`

    This module provides 3 `XMonad.Prompt`s to ease passwords
    manipulation (generate, read, remove) via [pass][].

  * `XMonad.Util.RemoteWindows`

    This module implements a proper way of finding out whether the
    window is remote or local.

  * `XMonad.Util.SpawnNamedPipe`

    A module for spawning a pipe whose `Handle` lives in the xmonad state.

  * `XMonad.Util.WindowState`

    Functions for saving per-window data.

### Miscellaneous Changes

  * Fix issue #9: `XMonad.Prompt.Shell` `searchPredicate` is ignored,
    defaults to `isPrefixOf`

  * Fix moveHistory when alwaysHighlight is enabled

  * `XMonad.Actions.DynamicWorkspaceGroups` now exports `addRawWSGroup`

  * Side tabs were added to the tabbed layout

  * `XMonad/Layout/IndependentScreens` now exports `marshallSort`

  * `XMonad/Hooks/UrgencyHook` now exports `clearUrgency`

  * Exceptions are now caught when finding commands on `PATH` in `Prompt.Shell`

  * Switched to `Data.Default` wherever possible

  * `XMonad.Layout.IndependentScreens` now exports `whenCurrentOn`

  * `XMonad.Util.NamedActions` now exports `addDescrKeys'`

  * EWMH `DEMANDS_ATTENTION` support added to `UrgencyHook`

  * New `useTransientFor` modifier in `XMonad.Layout.TrackFloating`

  * Added the ability to remove arbitrary workspaces

## 0.9 (October 26, 2009)

### Updates that Require Changes in `xmonad.hs`

  * `XMonad.Hooks.EwmhDesktops` no longer uses `layoutHook`, the
    `ewmhDesktopsLayout` modifier has been removed from
    xmonad-contrib. It uses `logHook`, `handleEventHook`, and
    `startupHook` instead and provides a convenient function `ewmh` to
    add EWMH support to a `defaultConfig`.

  * Most `DynamicLog` users can continue with configs unchanged, but
    users of the quickbar functions `xmobar` or `dzen` will need to
    change `xmonad.hs`: their types have changed to allow easier
    composition with other `XConfig` modifiers. The `dynamicLogDzen`
    and `dynamicLogXmobar` functions have been removed.

  * `WindowGo` or `safeSpawn` users may need to change command lines
    due to `safeSpawn` changes.

  * People explicitly referencing the "SP" scratchpad workspace should
    change it to "NSP" which is also used by the new
    `Util.NamedScratchpad` module.

  * (Optional) People who explicitly use `swapMaster` in key or mouse
    bindings should change it to `shiftMaster`. It's the current
    default used where `swapMaster` had been used previously. It works
    better than `swapMaster` when using floating and tiled windows
    together on the same workspace.

## See Also

<https://wiki.haskell.org/Xmonad/Notable_changes_since_0.8>

[pass]: http://www.passwordstore.org/
