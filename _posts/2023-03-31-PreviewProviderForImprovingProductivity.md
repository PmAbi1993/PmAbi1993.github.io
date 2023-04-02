---
title: Preview Providers for UIKit
date: 2023-03-31 01:00 +0000 
pin: false
---

# Speeding up workflows in large projects.

SwiftUI came as the icing on the top of the cake for iOS Developers. While everyone was fixated on the declarative programming I had my sights fixed on the preview provider. `Yeah, You wished your team manager would bump your deployment target to iOS 16+ 🤣. You WISH.`

The big projects that are heavily rooted in UIKit won't go away any time soon, `But I know a few people who would use that as a reason to not study SwiftUI for a long time 😃. Don't be that person`. 

One of the best things we can do is add the preview provider to our controller and increase the speed of our working just as we do in SwiftUI.

## Why??

### 1. Fast trial and error programming

During times when a code is not particularly self-explanatory or when something doesn't work as intended or when you are trying something new, We have to do a lot of trial and error to get the specific code working. `Yeah, Like 100% of the time, Who are we kidding? That's how coding is supposed to work. Unless you use ChatGPT, That is just pure magic 😰`.

Moreover, if you are working on a big project, There is a high chance that the screen/view you might be working on might be visible only after going through 10 screens. It is unproductive to go through those 10 screens to reach our destination every time we make a change. PreviewProvider will help in getting the screen up without running making debugging heavenly. `If your project is not S.O.L.I.D based then you are screwed 😅. Good luck getting a screen up that has 10 different concrete dependencies and like a million Singletons.`

### 2. People love Programmatic UI

> Drag & Drop UI are for the weak. Art of a digital Michelangelo relies through his ability of using ancient magic of written code.
>
> ~ RHPUID: __*Random Hardcore Programmatic UI Developer.*__

Have you seen your project build time incrementing over time? `Initial commit: I can boil my coffee during build time, Final commit: I could burn my stake now in my build time`. Storyboards and XIBs do increase our build time if done improperly but please do remember that is not the only reason. But most developers I know rely on programmatic UI to decrease build time and create good reusable views.

### 3. Code Modularization

One of the finer observations is that, In the task of writing previewable views/controllers, developers start to write clean code following S.O.L.I.D principles. I have seen people start creating creational patterns such as Factories even without understanding what that is. These small steps inch us towards writing beautiful proper code with proper separation of concerns.

### 4. Showcase workflows 

If you are working on a project with multiple teams with minimal documentation, You can add a few mock data or custom data providers with specific workflows enabled through the ViewProvider, which would help the person trying to analyze the code work through your code easier. This could also help someone who can easily review your workflow while reviewing the pull request without going through a lot of hurdles.

## How??

Usually while working on a project, we have to hot reload on
 1. A UIViewController  
 2. UIView
 3. UITableView / UICollectionView

Let's create a basic ViewProvider for UIKit and then continue to wrap all the above 3 elements in them

### UIViewControllerPreview

```swift

struct UIViewControllerPreview<ViewController: UIViewController>: UIViewControllerRepresentable {
    let viewControllerBuilder: () -> ViewController

    func makeUIViewController(context: Context) -> ViewController {
        return viewControllerBuilder()
    }

    func updateUIViewController(_ uiViewController: ViewController, context: Context) {
        // Perform any updates here
    }
}

```

This struct is confirming to __*UIViewControllerRepresentable*__ which would handle the necessary actions to present your controller that we pass into the Visual renderer. Since this is a struct we can pass in an *instance* of your ViewController and the view provider will handle the rest. Yup, That's it. That is all it is to it. `If you ain't gonna add it now, You ain't gonna add it ever 🫡`.

In the view controller you have written, Write down the below code to slide the live render in.

```swift
struct ViewControllerPreview: PreviewProvider {
    static var previews: some View {
        UIViewControllerPreview {
            let storyBoard: UIStoryboard = .init(name: "Main", bundle: nil)
            guard let controller: ViewController = storyBoard.instantiateViewController(withIdentifier: "ViewController") as? ViewController else { fatalError() }
            let navController: UINavigationController = UINavigationController(rootViewController: controller)
            return navController
        }
    }
}
```

Remember that you are responsible for creating the instance of your view controller to your liking. So consider using a Factory method or a proper wrapper around your view controller to present stub, mock or spy data to pass on to your controller.
`If your controller is a monolithic mammoth, walk away now. Even god can't help you here. I feel your pain though 😢`.

### UIViewPreview

You can refer to the explanations above because this is the same code with a little tweak.

```swift
struct UIViewPreview<View: UIView>: UIViewRepresentable {
    let viewBuilder: () -> View

    func makeUIView(context: Context) -> View {
        return viewBuilder()
    }

    func updateUIView(_ uiView: View, context: Context) {
        // Perform any updates here
    }
}
```

On the call site, we can use 

```swift
struct MyCustomViewPreview: PreviewProvider {
    static var previews: some View {
        UIViewPreview {
            MyCustomView() // Add your custom view / nib here
        }
    }
}
```

### TableViewCells

You get the gist now. Just let the `UIViewRepresentable` represent a view. This can be any UIKit View you build. I added 3 variants to show you it is similar for all, In real life, you would only need one generic struct which could confirm to UIViewRepresentable that can be used to populate any children of a UIKit view.

```swift
struct UITableViewCellPreview<Cell: UITableViewCell>: UIViewRepresentable {
    let cellBuilder: () -> Cell

    func makeUIView(context: Context) -> Cell {
        return cellBuilder()
    }

    func updateUIView(_ uiView: Cell, context: Context) {
        // Perform any updates here
    }
}
// Call site
struct MyTableViewCell_Preview: PreviewProvider {
    static var previews: some View {
        UITableViewCellPreview {
            MyTableViewCell(style: .default, reuseIdentifier: "MyCell", viewData: MockViewData())
        }
    }
}
```

## Outro

If your team is adamant about not adding any SwiftUI code, Then you can add the preview provider as a snippet in the Xcode. So when you want to preview a view just add that snippet at the bottom of the code and before committing the code remove the added preview providers. 

Since this promotes increased UI testing capabilities & improved collaboration within teams of our projects, I hope this becomes a mandate everywhere 😃.

Let me know how it goes.