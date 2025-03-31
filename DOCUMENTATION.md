![DebugPanel_GithubBanner](https://github.com/user-attachments/assets/88fce122-00ee-46f3-8387-ba852b63d67b)

UDebug Panel is a lightweight and versatile ingame debug panel for Unity with C#. 
It can be incredible useful to be able to modify gameplay parameters while on the target device. 
This asset simplifies the process of creating a panel with debut options in your Unity projects, allowing you to focus on what matters: gameplay.

A debug panel, is a user interface that provides developers with tools and information to aid in debugging and profiling during the development of a software application or game.

This asset provides a suit of premade elements (buttons, int selector, float selector, enum selection, etc), while allowing for the creation of new ones, with ease.

If you find any issue, please report it [here](https://github.com/GuillemUnity/UnityDebugPanel/issues).

![DebugPanel_MainScreenshot](https://github.com/user-attachments/assets/49f453aa-c863-47fd-8a20-1524ad3b959b)

## 📋 Table of Contents
1. [Features](#-features)
2. [Installation](#-installation)
3. [After Installing](#%EF%B8%8F-after-installing)
4. [Getting Started](#-getting-started)
5. [Sections](#sections)
6. [Automatic Debug Actions](#-automatic-debug-actions)
7. [Manual Debug Actions](#%EF%B8%8F-manual-debug-actions)
8. [Custom Debug Actions](#-creating-more-debug-actions)

## 🍰 Features
- **Simple API**: Unity Debug Panel provides an intuitive and easy-to-use API with C#.
    ```csharp
    UDebugPanel.Show();
    UDebugPanel.Hide();

    IDebugActionsSection section = UDebugPanel.AddSection("Section name");
    section.AddButton("Button name", () => Debug.Log("Button click"));
    ```

- **Adaptative**: The different widgets support and adapt to different screen aspect ratios, making it a good fit for both, desktop and mobile.

    ![DebugPanel_Orientation](https://github.com/user-attachments/assets/3684ad70-4b88-4e33-bb63-f7b615e38b8e)

- **Smart**: You can automatically generate a debug options section using a class. Using reflection, changes that occur on the debug panel will affect the class instance.

    ![DebugPanel_AutomaticWidgetCreation](https://github.com/user-attachments/assets/ed1694a9-351c-488a-bf0c-8ce711da2be9)

- **Organization**: Organize your options using sections.

    ![DebugPanel_Organization](https://github.com/user-attachments/assets/73da65f3-5a1c-4f06-a9cb-41538a685f22)

- **Fuzzy search**: Quicly find the options you were looking for with the search bar!

    ![DebugPanel_FuzzySearch](https://github.com/user-attachments/assets/127754e0-5f44-463c-a746-ebb7d91c4dda)


- **Lightweight**: While your game is running, the panel does not exist at all until you want to show it.
When is hidden again, the panel is completely destroyed, so it does not impact the preformance of your game.

## 📦 Installation
Download and import from the Unity Asset Store. You can move the root folder anywhere you want in your project. 
The package has the following dependencies:
- [TextMeshPro](https://docs.unity3d.com/Packages/com.unity.ugui@2.0/manual/TextMeshPro/index.html) (Mandatory).

> [!NOTE]
> If you are using [Assembly Definitions](https://docs.unity3d.com/2020.1/Documentation/Manual/ScriptCompilationAssemblyDefinitionFiles.html), you may need to include the DebugPanel.Runtime assembly to your assemblies.
  
> [!NOTE]
> Works with both [New](https://docs.unity3d.com/Packages/com.unity.inputsystem@1.14/manual/index.html) and Old Input Systems.

## ✔️ After Installing
To quickly check if everything has been setup properly, you can go to `DebugPanel/Examples/Scenes/` and open any of the example scenes. When you run any of those scenes, a simple functionality example should play.

## 📚 Getting Started
### Showing / Hiding
- For **showing** the panel, you just need to call the `Show` method. The internal logic will take care of everything else.
    ```csharp
    UDebugPanel.Show();
    ```
- For **hiding** the panel, just call the `Hide` method.
    ```csharp
    UDebugPanel.Hide();
    ```
- For convenience, you can also **toggle** the panel. Just call the `Toggle` method.
    ```csharp
    UDebugPanel.Toggle();
    ```
### Automatic Toggle
We already provide some handy automatic input toggles for you.
```csharp
UDebugPanel.SetupToggleInput();
```
By calling ```UDebugPanel.SetupToggleInput()```, you will automatically setup toggle for:
- Keyboard F1 key.
- Middle mouse button.
- Triple finger tap on screen.
  
You can modify this behaviour using the method parameters.

### Controller navigation
The panel has support for navigation with a controller or keyboard.
You can enable controller navigation by calling:
```csharp
UDebugPanel.SetControllerSupport(true);
```
> [!NOTE]
> Must be called before showing the panel, to take effect.

![DebugPanel_ControllerInput](https://github.com/user-attachments/assets/bf87e1c7-ebe7-4dec-bfd6-c9b4035e21b3)

## 📂Sections
Debug actions are divided within different sections. These sections allow you to better organize your actions.
You cannot create a debug action outside of a section.
- **Creating** a new section is very simple, you just need to call `AddSection` and provide a section name: 
    ```csharp
    IDebugActionsSection section = UDebugPanel.AddSection("Section name");
    ```
- **Removing** a section is equally as simple. Just call `RemoveSection`, and provide the section you want to remove.
    ```csharp
    UDebugPanel.RemoveSection(section);
    ```
> [!NOTE]
> You don't need to show the panel before creating actions/sections.

> [!NOTE]
> You can see this functionality on the example DebugPanel.Sections.

## 🤖 Automatic Debug Actions
This asset has the ability of scanning for properties and methods in C# classes, to automatically create the adecuate widgets.

One of such classes may look like this:

```csharp
class Options
{
    [NumberStep(5)]
    public int IntProperty { get; set; }
            
    [NumberStep(2.5f)] 
    public float FloatProperty { get; set; }
            
    [NumberRange(-10, 10)] 
    public long LongProperty { get; set; }
            
    [DisplayName("Bool Property Custom Display Name")]
    public bool BoolProperty { get; set; }
    public EnumProperty EnumProperty { get; set; }
            
    public string StringValue { get; } = "Text";
    public int IntValue => IntProperty;
    public float FloatValue => FloatProperty;
    public long LongValue => LongProperty;
    public bool BoolValue => BoolProperty;
    public EnumProperty EnumValue => EnumProperty;
            
    public void Method()
    {
        Debug.Log("Calling Method");
    }
            
    [Category("Another Section")]
    public int IntProperty2 { get; set; }
            
    [Category("Another Section")]
    public int FloatProperty2 { get; set; }
}
```

Then we add the class like this:

```csharp
UDebugPanel.AddOptionsObject(new ExampleOptionsObject());
```

And we will get debug options like this:

![Reflection](https://github.com/user-attachments/assets/b4c068de-7087-4c2d-84d3-7e2a72d6b403)


> [!NOTE]
> You can see this functionality on the example DebugPanel.Reflection.

 
## ▶️ Manual Debug Actions
This is the most important part of this asset, the debug actions (or widgets). Once you have a section, you add debug actions to it:

#### Info:
- Info: a static string that cannot be changed one submited.
    ```csharp
    section.AddInfo("Some info that never changes");
    ```
    ![image](https://github.com/user-attachments/assets/d33c9613-883f-4861-bad6-ac6edea09f4c)

- Dynamic Info: a getter for a string that it's updated every frame.
    ```csharp
    section.AddInfoDynamic(() => "Some info that can change");
    ```
    ![image](https://github.com/user-attachments/assets/ab52b8d1-cee6-41dd-84ab-5c52b5d78e14)

#### Buttons:
- Button: a simple button with a name.
    ```csharp
    section.AddButton("Button name", () => Debug.Log("Pressed"));
    ```
    ![image](https://github.com/user-attachments/assets/9fe5bafa-787a-4c15-a106-2d523f790d38)

#### Toggle:
- Toggle: a simple bool toggle with a name. Requests a setter and a getter for the value.
    ```csharp
    bool someBool = false;
    section.AddToggle("Toggle name", val => someBool = val, () => someBool);
    ```
    ![image](https://github.com/user-attachments/assets/4370d97e-5c3e-40cf-8308-e30417f9abf8)

#### Number selectors:
- Int: an int selector with a name. Requests a setter and a getter for the value.
    ```csharp
    int someInt = 0;
    section.AddIntSelector("Int name", val => someInt = val, () => someInt);
    ```
    ![image](https://github.com/user-attachments/assets/9093b457-2999-4f13-97b2-2e7e2995304b)

- Float: a float selector with a name. Requests a setter and a getter for the value.
    ```csharp
    float someFloat = 0f;
    section.AddFloatSelector("Float name", val => someFloat = val, () => someFloat);
    ```
    ![image](https://github.com/user-attachments/assets/95d9f397-e418-4013-a171-017300585dc0)

- Long: a long selector with a name. Requests a setter and a getter for the value.
    ```csharp
    long someLong = 0;
    section.AddLongSelector("Long name", val => someLong = val, () => someLong);
    ```
    ![image](https://github.com/user-attachments/assets/c0f7458f-497b-41d2-a282-32c8f0d4efcf)

#### Advanced Buttons:
- Button large info: a button that opens a popup which can show information as text.
    ```csharp
    section.AddButtonLargeInfo("Button name", () => "This is some large info");
    ```
    ![image](https://github.com/user-attachments/assets/f9ae1792-b109-428f-8880-a9c5a4d11d50)
    ![image](https://github.com/user-attachments/assets/f4efba92-cdc4-4009-b859-08a51349f4a7)

- Button string input: a button that opens a popup where you can set a string value.
    ```csharp
    string _stringInput = "Empty";
    section.AddButtonStringInput("Button name", () => _stringInput, v => _stringInput = v);
    ```
    ![image](https://github.com/user-attachments/assets/ecf2c7cc-7086-445c-a4d4-8058f89972d7)
    ![image](https://github.com/user-attachments/assets/1388186d-1332-43b8-9342-b88942960f64)

- Button list selector: a button that opens a popup where you can select an item from a list of items.
    ```csharp
    List<string> _elementsList = new() {"Element1", "Element2", "Element3"};
    section.AddButtonListSelector("Button name", () => _elementsList, i => Debug.Log($"Selected {_elementsList[i]}"));
    ```
    ![image](https://github.com/user-attachments/assets/dc5d4abc-19a4-425a-a967-f5713d4741fd)
    ![image](https://github.com/user-attachments/assets/654d6ad0-7418-442a-a157-6409dd573dbb)

- Button element list selector: a button that opens a popup where you can select an item from a list of items. The current selected value is stored internally and shown on the button text.
    ```csharp
    List<string> _elementsList = new() {"Element1", "Element2", "Element3"};
    section.AddButtonElementListSelector("Button name", () => _elementsList, i => Debug.Log($"Selected {_elementsList[i]}"));
    ```
    ![image](https://github.com/user-attachments/assets/894fa82e-253b-49cb-aaf6-79b5696787da)
    ![image](https://github.com/user-attachments/assets/e7fb5daf-1327-4fd4-b768-e56fd92a6303)

- Button enum selector: a button that opens a popup where you can select the value of an enum. The current selected value is stored internally and shown on the button text.
    ```csharp
    TestEnum _elementEnumSelected = TestEnum.Element1;
    section.AddButtonEnumSelector("Button name",  i => _elementEnumSelected = i, () => _elementEnumSelected);
    ```
    ![image](https://github.com/user-attachments/assets/00613047-8ac5-4c33-a0d9-879b8f67cb12)
    ![image](https://github.com/user-attachments/assets/c64a9e0d-10a7-42de-a11e-bf038a1d08cd)


#### Nested Containers:
- Nested conatiner: a button that opens a popup which can have more debug actions.
    ```csharp
    section.AddButtonActionsContainer("Actions", s =>
    {
        s.AddButton("Another Button 1", () => Debug.Log("Button pressed"));
        s.AddButton("Another Button 2", () => Debug.Log("Button pressed"));
        s.AddButton("Another Button 3", () => Debug.Log("Button pressed"));
    });
    ```
    ![image](https://github.com/user-attachments/assets/a61c82c3-3ca5-4c42-8d8d-55948e9fe93a)
    ![image](https://github.com/user-attachments/assets/e192658c-a208-4146-aab9-0e13131266ec)

> [!NOTE]
> You can see debug actions functionality on the example DebugPanel.Widgets.

## 🆕 Creating More Debug Actions
Some times, your game may have specific needs that cannot be properly met by the default provided widgets. That's why you can create your own.
We are going to use the Info action as an example.

1. The first thing you need to do is create a new class and inherit from `DebugAction`. This interface will force you to implement `DebugActionWidget InitWidget(DebugActionWidget viewInstance)` method, which is responsable for setting  the values from the action, to the widget Ui. We will not implement it for now.
We should first set the information that the action will hold. In this case it's a string for the info.

    ```csharp
    public sealed class InfoDebugAction : DebugAction
    {
        readonly string _info
    
        public InfoDebugAction(string info)
        {
            _info = info;
            ActionName = info; // ActionName is used for search box functionality
        }

        public override void InitWidget(DebugActionWidget viewInstance)
        {
            throw new NotImplementedException();
        }
    }
    ```

3. Next, we need a new `DebugActionWidget`, which will be the actual GameObject placed on the Ui. Since the widget is made of a label, we will add a reference to it. We will  also add an Init method to set the label value.

    ```csharp
    public sealed class InfoDebugActionWidget : DebugActionWidget
    {
        public TextMeshProUGUI Label;

        public void Init(string info)
        {
            Label!.text = info;
        }
    }
    ```


4. Going back to the `InfoDebugAction` class, we need to implement `InitWidget`. The widget itself will be automatically instantiated internally. We need to init it here.

    ```csharp
    public sealed class IntDebugAction : IDebugAction
    {    
        readonly string _info
    
        public InfoDebugAction(string info)
        {
            _info = info;
            ActionName = info;
        }
    
        public override void InitWidget(DebugActionWidget viewInstance)
        {
            InfoDebugActionWidget widget = (InfoDebugActionWidget)viewInstance;
            widget.Init(ActionName);
        }
    }
    ```
5. For being able to use this new action on a section, just add an extension method that does this:

    ```csharp
    public static IDebugAction AddInfo(this IDebugActionsSection section, string info)
    {
        InfoDebugAction debugAction = new InfoDebugAction(info);
        section.Add(debugAction);
        return debugAction;
    }
    ```

6. Cool! Finally, befor using the action, you just need to let the Debug Panel know that it should link the new debug action with the new widget prefab.

    ```csharp
     UDebugPanel.RegisterWidgetPrefab<InfoDebugAction>(InfoDebugActionWidgetPrefab);
    ```
6. That's it. Everything is set up for using your new debug action.
> [!NOTE]
> You can see an example of a custom widget at the example scene DebugPanel.CustomWidgets.

### Creating more popups
> [!NOTE]
> You can see an example of how to create custom popups on DebugPanel.CustomPopups.
