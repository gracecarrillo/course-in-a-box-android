---
title: Implement the second fragment
---

# Implement the second fragment
<br><br>

So far, you've focused on the first screen of your app. Next, you will update the Random button to display a random number between 0 and the current count on a second screen.

<img src="https://codelabs.developers.google.com/codelabs/build-your-first-android-app-kotlin/img/c7029fe48ec2a802.png" width="50%" height="50%">

## Update the layout for the second fragment
The screen for the new fragment will display a heading title and the random number. Here is what the screen will look like in the design view:

<img src="https://codelabs.developers.google.com/codelabs/build-your-first-android-app-kotlin/img/a991c2db96dcafb3.png" width="50%" height="50%">

The **%d** indicates that part of the string will be replaced with a number. The **R** is just a placeholder.

<br><br>
## Step 1: Add a TextView for the random number
<br><br>

1. Open `fragment_second.xml` (**app > res > layout > fragment_second.xml**) and switch to **Design** view if needed. Notice that it has a `ConstraintLayout` that contains a `TextView` and a `Button`.
2. Remove the chain constraint between the `TextView` and the` Button`.

<img src="https://codelabs.developers.google.com/codelabs/build-your-first-android-app-kotlin/img/e49352faab20c765.png">

3. Add another `TextView` from the palette and drop it near the middle of the screen. This `TextView` will be used to display a random number between 0 and the current count from the first `Fragment`.
4. Set the `id` to `@+id/textview_random` (`textview_random` in the **Attributes** panel.)
5. Constrain the top edge of the new `TextView` to the bottom of the first `TextView`, the left edge to the left of the screen, and the right edge to the right of the screen, and the bottom to the top of the **Previous** button.
6. Set both width and height to **wrap_content**.
7. Set the **textColor** to `@android:color/white`, set the **textSize** to **72sp**, and the **textStyle** to **bold**.

<img src="https://codelabs.developers.google.com/codelabs/build-your-first-android-app-kotlin/img/81dc7122e9ddaea1.png">

8. Set the text to "`R`". This text is just a placeholder until the random number is generated.
9. Set the `layout_constraintVertical_bias` to **0.45**.

This `TextView` is constrained on all edges, so it's better to use a vertical bias than margins to adjust the vertical position, to help the layout look good on different screen sizes and orientations.

Here is the XML code for the TextView that displays the random number:

```
<TextView
   android:id="@+id/textview_random"
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"
   android:text="R"
   android:textColor="@android:color/white"
   android:textSize="72sp"
   android:textStyle="bold"
   app:layout_constraintBottom_toTopOf="@+id/button_second"
   app:layout_constraintEnd_toEndOf="parent"
   app:layout_constraintStart_toStartOf="parent"
   app:layout_constraintTop_toBottomOf="@+id/textview_second"
   app:layout_constraintVertical_bias="0.45" />
```

<br><br>
## Step 2: Update the TextView to display the header
<br><br>

1. In `fragment_second.xml`, select `textview_second`, which currently has the text `"Hello second fragment. Arg: %1$s"` in the `hello_second_fragment` string resource.
2. If `android:text` isn't set, set it to the `hello_second_fragment` string resource.

```
android:text="@string/hello_second_fragment"
```

3. Change the `id` to `textview_header` in the **Attributes** panel.
4. Set the width to `match_constraint`, but set the height to `wrap_content`, so the height will change as needed to match the height of the content.
5. Set top, left and right margins to `24dp`. Left and right margins may also be referred to as "start" and "end" to support localization for right to left languages.
6. Remove any bottom constraint.
7. Set the text color to `@color/colorPrimaryDark` and the text size to `24sp`.
8. In `strings.xml`, change `hello_second_fragment` to `"Here is a random number between 0 and %d."`
9. Use **Refactor > Rename...** to change the name of `hello_second_fragment` to `random_heading`.

Here is the XML code for the TextView that displays the heading:

```
<TextView
   android:id="@+id/textview_header"
   android:layout_width="0dp"
   android:layout_height="wrap_content"
   android:layout_marginStart="24dp"
   android:layout_marginLeft="24dp"
   android:layout_marginTop="24dp"
   android:layout_marginEnd="24dp"
   android:layout_marginRight="24dp"
   android:text="@string/random_heading"
   android:textColor="@color/colorPrimaryDark"
   android:textSize="24sp"
   app:layout_constraintEnd_toEndOf="parent"
   app:layout_constraintStart_toStartOf="parent"
   app:layout_constraintTop_toTopOf="parent" />
```

<img src="https://codelabs.developers.google.com/codelabs/build-your-first-android-app-kotlin/img/ff7f9969afbd67ff.png">

<br><br>
## Step 3: Change the background color of the layout
<br><br>

Give your new activity a different background color than the first activity:

1. In `colors.xml`, add a new color resource:

```
<color name="screenBackground2">#26C6DA</color>
```

2. In the layout for the second activity, `fragment_second.xml`, set the background of the `ConstraintLayout` to the new color.

In the Attributes panel:

<img src="https://codelabs.developers.google.com/codelabs/build-your-first-android-app-kotlin/img/9948b482fb81ef5.png">

Or in XML:

```
android:background="@color/screenBackground2"
```

Your app now has a completed layout for the second fragment. But if you run your app and press the **Random** button, it may crash. The click handler that Android Studio set up for that button needs some changes. In the next task, you will explore and fix this error.

<br><br>
## Step 4: Examine the navigation graph
<br><br>

When you created your project, you chose **Basic Activity** as the template for the new project. When Android Studio uses the Basic Activity template for a new project, it sets up two fragments, and a navigation graph to connect the two. It also sets up a button to go from the first fragment to the second. This is the button you changed into the **Random** button. And now you want to send a number when the button is pressed.

1. Open `nav_graph.xml` (**app > res > navigation > nav_graph.xml**).

A screen similar to the **Layout Editor** in **Design** view appears. It shows the two fragments with some arrows between them. You can zoom with + and - buttons in the lower right, as you did with the **Layout Editor**.

2. You can freely move the elements in the navigation graph. For example, If the fragments appear with `SecondFragment` to the left, drag `FirstFragment` to the left of `SecondFragment` so they appear in the order you work with them.

<img src="https://codelabs.developers.google.com/codelabs/build-your-first-android-app-kotlin/img/504c2156d46d4d6b.png">

<br><br>
## Step 5: Enable SafeArgs
<br><br>

This will enable SafeArgs in Android Studio.

1. Open **Gradle Scripts > build.gradle (Project: My First App)** 
2. Find the `dependencies` section In the `buildscript` section, and add the following lines after the other `classpath` entries:

```
def nav_version = "2.3.0-alpha02"
classpath "androidx.navigation:navigation-safe-args-gradle-plugin:$nav_version"
```

3. Open **Gradle Scripts > build.gradle (Module: app)**
4. Just below the other lines that begin with apply plugin add a line to enable `SafeArgs`:

```
apply plugin: 'androidx.navigation.safeargs.kotlin'
```

Android Studio should display a message about the Gradle files being changed. Click **Sync Now** on the right hand side.

<img src="https://codelabs.developers.google.com/codelabs/build-your-first-android-app-kotlin/img/50cedf1769381459.png">

After a few moments, Android Studio should display a message in the Sync tab that it was successful:

<img src="https://codelabs.developers.google.com/codelabs/build-your-first-android-app-kotlin/img/a1c51cb92c04e07e.png">

6. Choose **Build > Make Project**. This should rebuild everything so that Android Studio can find `FirstFragmentDirections`.

**Troubleshooting: If the sync was not successful, confirm that you added the correct lines to the correct Gradle file. If there are still problems, check the developer's guide about Safe Args for an updated nav_version or other changes.**

<br><br>
## Step 6: Create the argument for the navigation action
<br><br>

1. In the navigation graph, click on `FirstFragment`, and look at the **Attributes** panel to the right. (If the panel isn't showing, click on the vertical **Attributes** label to the right.)
2. In the Actions section, it shows what action will happen for navigation, namely going to `SecondFragment`.
3. Click on `SecondFragment`, and look at the **Attributes** panel.

The **Arguments** section shows `nothing`.

4. Click on the **+** in the **Arguments** section.
5. In the **Add Argument** dialog, enter `myArg` for the name and set the type to **Integer**, then click the **Add** button.

<img src="https://codelabs.developers.google.com/codelabs/build-your-first-android-app-kotlin/img/c334d61be24eb01d.png">

<br><br>
## Step 6: Send the count to the second fragment
<br><br>

The **Next/Random** button was set up by Android Studio to go from the first fragment to the second, but it doesn't send any information. In this step you'll change it to send a number for the current count. You will get the current count from the text view that displays it, and pass that to the second fragment.

1. Open `FirstFragment.kt` (**app > java > com.example.myfirstapp > FirstFragment**)
2. Find the method `onViewCreated()` and notice the code that sets up the click listener to go from the first fragment to the second.
3. Replace the code in that click listener with a line to find the count text view, `textview_first`.

```
val showCountTextView = view.findViewById<TextView>(R.id.textview_first)
```

4. Get the text of the view and convert it to an `Int`.

```
val currentCount = showCountTextView.text.toString().toInt()
```

5. Create an action with currentCount as the argument to `actionFirstFragmentToSecondFragment()`.

```
val action = FirstFragmentDirections.actionFirstFragmentToSecondFragment(currentCount)
```

6. Add a line to find the nav controller and navigate with the action you created.

```
findNavController().navigate(action)
```

Here is the whole method, including the code you added earlier:

```
override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
   super.onViewCreated(view, savedInstanceState)

   view.findViewById<Button>(R.id.random_button).setOnClickListener {
       val showCountTextView = view.findViewById<TextView>(R.id.textview_first)
       val currentCount = showCountTextView.text.toString().toInt()
       val action = FirstFragmentDirections.actionFirstFragmentToSecondFragment(currentCount)
       findNavController().navigate(action)
   }

   // find the toast_button by its ID
   view.findViewById<Button>(R.id.toast_button).setOnClickListener {
       // create a Toast with some text, to appear for a short time
       val myToast = Toast.makeText(context, "Hello Toast!", Toast.LENGTH_SHORT)
       // show the Toast
       myToast.show()
   }

   view.findViewById<Button>(R.id.count_button).setOnClickListener {
       countMe(view)
   }
}
```

7. Run your app. Click the **Count** button a few times. Now when you press the **Random** button, the second screen shows the correct string in the header, but still no count or random number, because you need to write some code to do that.

<br><br>
## Step 7: Update SecondFragment to compute and display a random number
<br><br>

You have written the code to send the current count to the second fragment. The next step is to add code to `SecondFragment.kt` to retrieve and use the current count.

1. In `SecondFragment.kt`, add an import for `navArgs` to the list of imported libraries.

```
import androidx.navigation.fragment.navArgs
```

2. In `SecondFragment.kt`, before `onViewCreated()`, add a line to define where the arguments are.

```
val args: SecondFragmentArgs by navArgs()
```

3. In `SecondFragment.kt` below where the click listener is created, add lines to get the count argument, get the string and format it with the count, and then set it for textview_header.

```
val count = args.myArg
val countText = getString(R.string.random_heading, count)
view.findViewById<TextView>(R.id.textview_header).text = countText
Add code to get a random number between 0 and the count.
val random = java.util.Random()
var randomNumber = 0
if (count > 0) {
   randomNumber = random.nextInt(count + 1)
}
```

4. Add code to convert that number into a string and set it as the text for `textview_random`.

```
view.findViewById<TextView>(R.id.textview_random).text = randomNumber.toString()
```

Here is the whole method.

```
    val args: SecondFragmentArgs by navArgs()

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)

        view.findViewById<Button>(R.id.button_second).setOnClickListener {
            findNavController().navigate(R.id.action_SecondFragment_to_FirstFragment)
        }

        val count = args.myArg
        val countText = getString(R.string.random_heading, count)
        view.findViewById<TextView>(R.id.textview_header).text = countText

        val random = java.util.Random()
        var randomNumber = 0
        if (count > 0) {
            randomNumber = random.nextInt(count + 1)
        }
        view.findViewById<TextView>(R.id.textview_random).text = randomNumber.toString()
    }
```

 
6. Run the app. Press the **Count** button a few times, then press the **Random** button. Does the app display a random number in the new activity?

<img src="https://codelabs.developers.google.com/codelabs/build-your-first-android-app-kotlin/img/6cba94311109e72f.png">

### Congratulations, you have built your first Android app!


