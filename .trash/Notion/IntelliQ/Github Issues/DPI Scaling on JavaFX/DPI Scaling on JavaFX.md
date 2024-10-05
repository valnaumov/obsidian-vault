---
Created: 2024-01-14T00:44
Updated: 2024-01-14T10:39
---
# The problem

On Java 8 we don’t have our UI being adjusted to Windows display scaling settings. It’s always the same size in physical pixels. Intellij IDEA’s interface is adjusted, for example.

On Java starting version 9 UI is scaled. On JavaFX version `21.0.1` and on my machine with 125% scaling the UI feels just too big. And I’m afraid the sizes of controls were not measured and set properly. For instance, I could adjust use an absolute value in px from the design mockup and match it on my machine with 125% scaling. I mostly used em units, so they should be scaled properly, but absolute units may not be (specified in code and FXML). I have set a system property `glass.win.uiScale=100%` to match the old behavior.

Scaling the UI according to the Windows scaling settings is the way to go. We need to do some test and think.

![[Notion 2/Attachments/Java_21_glass.win.uiScale100_Win_scaling_set_to_125.png]]

Java 21, glass.win.uiScale=100, Win scaling set to 125

![[Notion 2/Attachments/Java_21_glass.win.uiScale100_Win_scaling_set_to_100.png]]

Java 21, glass.win.uiScale=100, Win scaling set to 100

  

![[Notion 2/Attachments/Java_21_glass.win.uiScale_not_set_Win_scaling_set_to_125.png]]

Java 21, glass.win.uiScale not set, Win scaling set to 125

![[Notion 2/Attachments/Java_21_glass.win.uiScale_not_set_Win_scaling_set_to_100.png]]

Java 21, glass.win.uiScale not set, Win scaling set to 125

  

# A few articles on the topic

> [!info] Screen resolutions and dpi  
>  
> [https://www.reddit.com/r/JavaFX/comments/twbl2l/screen_resolutions_and_dpi/](https://www.reddit.com/r/JavaFX/comments/twbl2l/screen_resolutions_and_dpi/)  

> [!info] DPI Scaling in Windows GUIs  
> Comparing automatic scaling to variable Windows pixel densities in WPF, JavaFX, Windows Forms & Swing.  
> [https://kynosarges.org/GuiDpiScaling.html](https://kynosarges.org/GuiDpiScaling.html)  

> [!info] JavaFX DPI Scaling in Java 9  
> While porting my projects to Java SE 9 I noticed that the JavaFX team has slipped in some small but important changes concerning DPI scaling that appear to be only documented in the Java bug databa…  
> [https://news.kynosarges.org/2018/01/26/javafx-dpi-scaling-in-java-9/](https://news.kynosarges.org/2018/01/26/javafx-dpi-scaling-in-java-9/)