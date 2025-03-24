![DebugPanel_GithubBanner](https://github.com/user-attachments/assets/ddbd1616-6055-4c13-b566-d1306ea06e00)

Unity Debug Panel is a lightweight and versatile ingame debug panel for Unity with C#. 
It can be incredible useful to be able to modify gameplay parameters while on the target device. 
This asset simplifies the process of creating a panel with debut options in your Unity projects, allowing you to focus on what matters: gameplay.

A debug panel, is a user interface that provides developers with tools and information to aid in debugging and profiling during the development of a software application or game.

This asset provides a suit of premade elements (buttons, int selector, float selector, enum selection, etc), while allowing for the creation of new ones, with ease.

![DebugPanel_MainScreenshot](https://github.com/user-attachments/assets/49f453aa-c863-47fd-8a20-1524ad3b959b)

## 🍰 Features
- **Simple API**: Unity Debug Panel provides an intuitive and easy-to-use API with C#.
    ```csharp
    UDebugPanel.Show();
    UDebugPanel.Hide();

    IDebugActionsSection section = UDebugPanel.AddSection("Section name");
    section.AddButton("Button name", () => Debug.Log("Button click"));
    ```

- **Adaptative**: The different widgets support and adapt to different screen aspect ratios, making it a good fit for both, desktop and mobile.

    ![DebugPanel_Orientation](https://github.com/user-attachments/assets/d72b89f5-55b7-49de-aee9-847a20cfdb79)

- **Smart**: You can automatically generate a debug options section using a class. Using reflection, changes that occur on the debug panel will affect the class instance.

  ![AutomaticArt](https://github.com/Guillemsc/GDebugPanelGodot/assets/17142208/08886a94-e062-4532-a907-81c6482b2696)

- **Organization**: Organize your options using collapsable sections.

  ![Gif2](https://github.com/Guillemsc/GDebugPanelGodot/assets/17142208/a181cbeb-eb6a-4b8e-9de0-118f9b27d2bb)

- **Fuzzy search**: Quicly find the options you were looking for with the search bar!

  ![Gif](https://github.com/Guillemsc/GDebugPanelGodot/assets/17142208/5f47d808-69ab-4e5d-8aa9-18f0be2c2f87)

- **Lightweight**: While your game is running, the panel does not exist at all until you want to show it.
When is hidden again, the panel is completely destroyed, so it does not affect to the preformance of your game.

## 📦 Installation
Download and import from the Unity Asset Store. You can move the root folder anywhere you want in your project. 
The package has the following dependencies:
- [TextMeshPro](https://docs.unity3d.com/Packages/com.unity.ugui@2.0/manual/TextMeshPro/index.html) (Mandatory).
  
> [!NOTE]
> Works with both New and Old input systems

## ✔️ After installing
To quickly check if everything has been setup properly, you can go to DebugPanel/Examples/Scenes/ and open any of the example scenes. When you run any of those scenes, a simple functionality example should play.

## 📚 Getting started
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

### Sections
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

### Automatic debug actions
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

 
### Manual debug actions
This is the most important part of this asset, the debug actions (or widgets). Once you have a section, you add debug actions to it:

#### Info:
- Info: a static string that cannot be changed one submited.
    ```csharp
    section.AddInfo("Some info that never changes");
    ```
- Dynamic Info: a getter for a string that it's updated every frame.
    ```csharp
    section.AddInfoDynamic(() => "Some info that can change");
    ```
#### Buttons:
- Button: a simple button with a name.
    ```csharp
    section.AddButton("Button name", () => Debug.Log("Pressed"));
    ```
#### Toggle:
- Toggle: a simple bool toggle with a name. Requests a setter and a getter for the value.
    ```csharp
    bool someBool = false;
    section.AddToggle("Toggle name", val => someBool = val, () => someBool);
    ```
#### Number selectors:
- Int: an int selector with a name. Requests a setter and a getter for the value.
    ```csharp
    int someInt = 0;
    section.AddIntSelector("Int name", val => someInt = val, () => someInt);
    ```
- Float: a float selector with a name. Requests a setter and a getter for the value.
    ```csharp
    float someFloat = 0f;
    section.AddFloatSelector("Float name", val => someFloat = val, () => someFloat);
    ```
- Long: a long selector with a name. Requests a setter and a getter for the value.
    ```csharp
    long someLong = 0;
    section.AddLongSelector("Long name", val => someLong = val, () => someLong);
    ```
#### Advanced Buttons:
- Button large info: a button that opens a popup which can shown information as text.
    ```csharp
    section.AddButtonLargeInfo("Button name", () => "This is some large info");
    ```
- Button string input: a button that opens a popup where you can set a string value.
    ```csharp
    string _stringInput = "Empty";
    section.AddButtonStringInput("Button name", () => _stringInput, v => _stringInput = v);
    ```
- Button list selector: a button that opens a popup where you can select an item from a list of items.
    ```csharp
    List<string> _elementsList = new() {"Element1", "Element2", "Element3"};
    section.AddButtonListSelector("Button name", () => _elementsList, i => Debug.Log($"Selected {_elementsList[i]}"));
    ```
- Button element list selector: a button that opens a popup where you can select an item from a list of items. The current selected value is stored internally and shown on the button text.
    ```csharp
    List<string> _elementsList = new() {"Element1", "Element2", "Element3"};
    section.AddButtonElementListSelector("Button name", () => _elementsList, i => Debug.Log($"Selected {_elementsList[i]}"));
    ```
- Button enum selector: a button that opens a popup where you can select the value of an enum. The current selected value is stored internally and shown on the button text.
    ```csharp
    TestEnum _elementEnumSelected = TestEnum.Element1;
    section.AddButtonEnumSelector("Button name",  i => _elementEnumSelected = i, () => _elementEnumSelected);
    ```
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
> [!NOTE]
> You can see debug actions functionality on the example DebugPanel.Widgets.

### Creating more debug actions
Some times, your game may have specific needs that cannot be properly met by the default provided widgets. That's why you can create your own.
We are going to use the Info action as an example.

1. The first thing you need to do is create a new class and inherit from `DebugAction`. This interface will force you to implement `DebugActionWidget InitWidget(RectTransform popupsParent, DebugActionWidget viewInstance)` method, which is responsable for setting  the values from the action, to the widget Ui. We will not implement it for now.
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

        public override void InitWidget(RectTransform popupsParent, DebugActionWidget viewInstance)
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
    
        public override void InitWidget(RectTransform popupsParent, DebugActionWidget viewInstance)
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
