ZSSRichTextEditor
=============

The Editor
---

`ZSSRichTextEditor` is a beautiful Rich Text `WYSIWYG Editor` for `iOS`. It includes all of the standard editor tools one would expect from a `WYSIWYG` editor as well as an amazing source view with syntax highlighting.

![toolbar](https://user-images.githubusercontent.com/30858/132384030-59c0d2be-ab90-4535-9dd8-e5ee3e405e2e.gif)

The editor is used how any other text input area in iOS is used. A selection of text or content is made, then tapping on the toolbar item below will apply that style. A Source View is also included, you can make changes and this will be reflected in the editor preview.

![editor](https://user-images.githubusercontent.com/30858/132384094-9a1d2182-0c21-468d-b3d9-2049397e2af5.gif)

Colors
---

We wanted to have a really beautiful color picker to make changing colors really simple. So, we used the open-source HRColorPicker which was exactly what we were looking for. Choosing colors for text or background is simple and seamless.

![colors](https://user-images.githubusercontent.com/30858/132384119-6b4a836d-1c21-400a-bb5a-5d18534d3bd5.gif)

How It Works
---

Just subclass `ZSSRichTextEditor` and use the following:

```objective-c
// HTML Content to set in the editor
NSString *html = @"<!-- This is an HTML comment -->"
"<p>This is a test of the <strong>ZSSRichTextEditor</strong> by <a title=\"Zed Said\" href=\"http://www.zedsaid.com\">Zed Said Studio</a></p>";

// Set the base URL if you would like to use relative links, such as to images.
self.baseURL = [NSURL URLWithString:@"http://www.zedsaid.com"];

// If you want to pretty print HTML within the source view.
self.formatHTML = YES;

// set the initial HTML for the editor
[self setHTML:html];
```

If you want to retrieve the HTML from the editor:
```objective-c
// Returns an NSString
[self getHTML];
```

Insert HTML at the current caret position:
```objective-c
NSString *html = @"<strong>I love cats!</strong>";
[self insertHTML:html];
```

Change the tint color of the toolbar buttons:
```objective-c
// Set the toolbar item color
self.toolbarItemTintColor = [UIColor greenColor];

// Set the toolbar selected color
self.toolbarItemSelectedTintColor = [UIColor redColor];
```

Show only specified buttons in the toolbar:
```objective-c
self.enabledToolbarItems = @[ZSSRichTextEditorToolbarBold, ZSSRichTextEditorToolbarH1, ZSSRichTextEditorToolbarParagraph];
```

Always show the toolbar even when the keyboard is hidden:
```objective-c
self.alwaysShowToolbar = YES;
```

Set A Placeholder
---

```objective-c
[self setPlaceholder:@"This is a placeholder that will show when there is no content(html)"];

```

Insert Link and Insert Image
---

If you want to manually insert a link or image where the cursor is, you can use the following methods:

**Insert Image**
```objective-c
- (void)insertImage:(NSString *)url alt:(NSString *)alt;
```

**Insert Link**
```objective-c
- (void)insertLink:(NSString *)url title:(NSString *)title;
```

Custom Pickers
---

You can implement your own pickers for images and links if you have an alternate method that you are wanting to use. E.g., uploading an image from your camera roll then inserting the URL.

When the alternate picker icon (crosshair) is tapped it will call the corresponding method, which you need to override in your `ZSSRichTextEditor` subclass (see example project):

```objective-c
- (void)showInsertURLAlternatePicker {
    
    [self dismissAlertView];
    
    // Show your custom picker
    
}


- (void)showInsertImageAlternatePicker {
    
    [self dismissAlertView];
    
    // Show your custom picker
    
}
```

Custom Toolbar Buttons
---

```objective-c
UIButton *myButton = [[UIButton alloc] initWithFrame:CGRectMake(0.0f, 0.0f, buttonWidth, 28.0f)];
[myButton setTitle:@"My Button" forState:UIControlStateNormal];
[myButton addTarget:self
             action:@selector(didTapCustomToolbarButton:)
   forControlEvents:UIControlEventTouchUpInside];

[self addCustomToolbarItemWithButton:myButton];

```

Custom CSS
---

```objective-c
NSString *customCSS = @"a {text-decoration:none;} a:hover {color:#FF0000;}";
[self setCSS:customCSS];

```

Receive Editor Did Change Events
---

Add the following to your viewDidLoad method:

```objective-c
self.receiveEditorDidChangeEvents = YES;
```

Then you will receive events in the following method:

```objective-c
- (void)editorDidChangeWithText:(NSString *)text andHTML:(NSString *)html {
    
    NSLog(@"Text Has Changed: %@", text);
    
    NSLog(@"HTML Has Changed: %@", html);
    
}
```

Receive Hashtag & Mention Events
---

Hashtags:
```objective-c
- (void)hashtagRecognizedWithWord:(NSString *)word {
    
    NSLog(@"Hashtag has been recognized: %@", word);
    
}
```
Mentions:
```objective-c
- (void)mentionRecognizedWithWord:(NSString *)word {
    
    NSLog(@"Mention has been recognized: %@", word);
    
}
```

Supported Functions
---

ZSSRichTextEditor has the following functions:

*   Bold
*   Italic
*   Subscript
*   Superscript
*   Strikethrough
*   Underline
*   Remove Formatting
*   Font
*   Justify Left
*   Justify Center
*   Justify Right
*   Justify Full
*   Paragraph
*   Heading 1
*   Heading 2
*   Heading 3
*   Heading 4
*   Heading 5
*   Heading 6
*   Undo
*   Redo
*   Unordered List
*   Ordered List
*   Indent
*   Outdent
*   Insert Image
*   Insert Link
*   Quick Link
*   Unlink
*   Horizontal Rule
*   View Source
*   Text Color
*   Background Color

Installation
--------------
You can use `CocoaPods` for this fork (until [this issue](https://github.com/nnhubbard/ZSSRichTextEditor/issues/267) is resolved):

1. Add the dependency for this fork to your podfile:
    ```
    pod 'ZSSRichTextEditor', :git => 'https://github.com/codenameDuchess/ZSSRichTextEditor.git'
    ```
2. Run `pod install`

Or, manually install with the following instructions from the parent repo:

`ZSSRichTextEditor` requires iOS7 as well as `CoreGraphics.framework` and `CoreText.framework`.

- Copy the `Source` folder to your project.
- Subclass `ZSSRichTextEditor` and implement the methods as mentioned above.

**When using `ZSSRichTextEditor` in your own project, XCode will automatically add `ZSSRichTextEditor.js` to compile sources under build phases, this will cause `ZSSRichTextEditor` to not work correctly as the javascript file won't be included in your app. Instead, remove it from compile sources and add it to copy bundle resources.**

Attribution
--------------

`ZSSRichTextEditor` uses portions of code from the following sources:

| Component     | Description   | License  |
| :------------- |:-------------| :-----|
| [CYRTextView](https://github.com/illyabusigin/CYRTextView)      | CYRTextView is a UITextView subclass that implements a variety of features that are relevant to a syntax or code text view. | [MIT](https://github.com/illyabusigin/CYRTextView/blob/master/LICENSE) |
| [HRColorPicker](https://github.com/hayashi311/Color-Picker-for-iOS)      | Simple color picker for iPhone      |   [BSD](https://github.com/hayashi311/Color-Picker-for-iOS/blob/master/ColorPicker/HRColorPickerView.h) |
| [jQuery](https://jquery.com)      | jQuery is a fast, small, and feature-rich JavaScript library.      |   [MIT](http://jquery.org/license) |
| [JS Beautifier](https://github.com/einars/js-beautify)      | Makes ugly Javascript pretty      |   [MIT](https://github.com/einars/js-beautify/blob/master/LICENSE) |

Contact
--------------
Visit us online at [http://www.zedsaid.com](http://www.zedsaid.com) or [@zedsaid](https://twitter.com/zedsaid).
