### Accessibility improvements in Windows Forms controls for .NET 4.8

#### Details

The Windows Forms Framework is continuing to improve how it works with accessibility technologies to better support Windows Forms customers. These include the following changes:

- Changes to improve display during High Contrast mode.
- Changes to interaction with Narrator.
- Changes in the Accessible hierarchy (improving navigation through the UI Automation tree).

#### Suggestion

**How to opt in or out of these changes**
In order for the application to benefit from these changes, it must run on the .NET Framework 4.8. The application can opt in into these changes in either of the following ways:

- It is recompiled to target the .NET Framework 4.8. These accessibility changes are enabled by default on Windows Forms applications that target the .NET Framework 4.8.
- It targets the .NET Framework 4.7.2 or earlier version and opts out of the legacy accessibility behaviors by adding the following [AppContext switch](../../../../docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) to the `<runtime>` section of the app config file and setting it to `false`, as the following example shows.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7"/>
  </startup>
  <runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true/false;key2=true/false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false" />
  </runtime>
</configuration>
```

Note that to opt in to the accessibility features added in .NET Framework 4.8, you must also opt in to accessibility features of .NET Framework 4.7.1 and 4.7.2 as well. Applications that target the .NET Framework 4.8 and want to preserve the legacy accessibility behavior can opt in to the use of legacy accessibility features by explicitly setting this AppContext switch to `true`.Enabling the keyboard ToolTip invocation support requires adding the `Switch.System.Windows.Forms.UseLegacyToolTipDisplay=false` line to the AppContextSwitchOverrides value:

```xml
<AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false;Switch.System.Windows.Forms.UseLegacyToolTipDisplay=false" />
```

Note that enabling this feature requires opting in to the aforementioned accessibility features of .NET Framework 4.7.1 - 4.8. Also, if any of the accessibility features are not opted in but the tooltip display feature is opted in, a runtime <xref:System.NotSupportedException> will be thrown on the first access to these features. The exception message indicates that keyboard ToolTips require accessibility improvements of level 3 to be enabled.

**Use of OS-defined colors in High Contrast themes**

- Improved high-contrast themes.

**Improved Narrator support**

- Narrator now announces the sort direction of the <xref:System.Windows.Forms.DataGridViewColumn> when announcing an accessible name of a <xref:System.Windows.Forms.DataGridViewCell>.

**Improved CheckedListBox Accessibility support**

- Improved Narrator support for the <xref:System.Windows.Forms.CheckedListBox> control. When navigating to the <xref:System.Windows.Forms.CheckedListBox> control using the keyboard, Narrator focuses the <xref:System.Windows.Forms.CheckedListBox> item and announces it.
- An empty CheckedListBox control now has a focus rectangle drawn for a virtual first item when the control becomes focused.

**Improved ComboBox Accessibility support**

- Enabled UI Automation support for the <xref:System.Windows.Forms.ComboBox> control, with the ability to use UI Automation notifications and other UI Automation features.
**Improved DataGridView Accessibility support**

- Enabled UI Automation support for <xref:System.Windows.Forms.DataGridView> control with ability to use UI Automation notifications and other UI Automation features.
- The UI Automation element which corresponds to the <xref:System.Windows.Forms.DataGridViewComboBoxEditingControl> or <xref:System.Windows.Forms.DataGridViewTextBoxEditingControl> is now a child of corresponding editing cell.

**Improved LinkLabel Accessibility support**

- Improved <xref:System.Windows.Forms.LinkLabel> control accessibility: Narrator announces the disabled state for the link if the corresponding <xref:System.Windows.Forms.LinkLabel> control is disabled.

**Improved ProgressBar Accessibility support**

- Enabled UI Automation support for the <xref:System.Windows.Forms.ProgressBar> control with the ability to use UI Automation notifications and other UI Automation features. Developers are now able to use UI Automation notifications which Narrator can announce to indicate progress.
For an overview of UI automation events overview, including UI automation notification events, see the [UI Automation Events Overview](/windows/desktop/WinAuto/uiauto-eventsoverview).

**Improved PropertyGrid Accessibility support**

- Enabled UI Automation support for the <xref:System.Windows.Forms.PropertyGrid> control, with the ability to use UI Automation notifications and other UI Automation features.
- The UI Automation element which corresponds to the currently edited property is now a child of the corresponding property item UI Automation element.
- The UI Automation property item element is now a child of the corresponding category element if the parent <xref:System.Windows.Forms.PropertyGrid> control is set to category view.

**Improved ToolStrip support**

- Enabled UI Automation support for the <xref:System.Windows.Forms.ToolStrip> control, with the ability to use UI Automation notifications and other UI Automation features.
- Improved navigation through <xref:System.Windows.Forms.ToolStrip> items.
- In items mode, Narrator focus does not disappear and does not go to hidden items.

**Improved Visual cues**

- An empty <xref:System.Windows.Forms.CheckedListBox> control now displays a focus indicator when it receives focus.
Note: UI automation support is enabled for controls in runtime but is not used in design time. For an overview of UI automation, see the [UI Automation Overview](../../../../docs/framework/ui-automation/ui-automation-overview.md).

**Invoking controls' ToolTips with a keyboard**

- Control tooltip can now be invoked by focusing the control with keyboard. This feature needs to be enabled explicitly for the application (see section **&quot;How to opt in or out of these changes&quot;**)

| Name    | Value       |
|:--------|:------------|
| Scope   | Major       |
| Version | 4.8         |
| Type    | Retargeting |
