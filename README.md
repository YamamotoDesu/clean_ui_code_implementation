## Clean Your UI Code in Flutter

### 1. Section Definition

- Header
- Leading Information
- Image List
- Size Information
- Description
- Review
- Price Information
- Bottom Fixed Button (Add to Cart button)

### 2. Create Custom Scaffold Module

Custom Scaffold Module
```dart
class ProductDetailScaffold extends StatelessWidget {  
  const ProductDetailScaffold({  
    Key? key,  
    required this.header,  
    required this.leadingInfoView,  
    required this.imgListView,  
    required this.sizeInfoView,  
    required this.descriptionView,  
    required this.reviewListView,  
    required this.priceInfoView,  
    required this.bottomFixedButton,  
  }) : super(key: key);  
  
  final Widget header;  
  final Widget leadingInfoView;  
  final Widget imgListView;  
  final Widget sizeInfoView;  
  final Widget descriptionView;  
  final Widget reviewListView;  
  final Widget priceInfoView;  
  final Widget bottomFixedButton;  
  
  @override  
  Widget build(BuildContext context) {  
    return Scaffold(  
      backgroundColor: Colors.white,  
      body: Stack(  
        children: [  
          SingleChildScrollView(  
            child: Column(  
              children: <Widget>[  
                header,  
                const SizedBox(height: 15),  
                Padding(  
                  padding: const EdgeInsets.symmetric(horizontal: 20),  
                  child: Column(  
                    crossAxisAlignment: CrossAxisAlignment.start,  
                    children: <Widget>[  
                      leadingInfoView,  
                      const SizedBox(height: 20),  
                      imgListView,  
                      const SizedBox(height: 15),  
                      sizeInfoView,  
                      const SizedBox(height: 20),  
                      descriptionView,  
                      const SizedBox(height: 15),  
                      reviewListView,  
                      const SizedBox(height: 20),  
                      priceInfoView,  
                      SizedBox(  
                        height: MediaQuery.of(context).padding.bottom + 96,  
                      )  
                    ],  
                  ),  
                ),  
              ],  
            ),  
          ),  
  
          /// BOTTOM FIXED BUTTON  
          Positioned(  
            bottom: 0,  
            child: bottomFixedButton,  
          )  
        ],  
      ),  
    );  
  }  
}
```

### 3. Widget Modularization
Before applying the Scaffold, you need to extract each widget separated by section into individual Stateless Widgets.

```dart
/// Extracted as a Stateless Widget (🙆‍♂️)
class ProductDetailHeader extends StatelessWidget {  
  const ProductDetailHeader({Key? key}) : super(key: key);  
  
  @override  
  Widget build(BuildContext context) {  
    return Container(  
      height: 386,  
      decoration: BoxDecoration(  
        image: DecorationImage(  
            image: Image.asset(Assets.imagesProductImg0).image,  
            fit: BoxFit.fitHeight),  
      ),  
    );  
  }  
}

/// Extracted as a method (🙅‍♂️)
_buildHeader() {
    return Container(  
      height: 386,  
      decoration: BoxDecoration(  
        image: DecorationImage(  
            image: Image.asset(Assets.imagesProductImg0).image,  
            fit: BoxFit.fitHeight),  
      ),  
    ); 
}
```

When extracting a section, it’s important to extract it as a StatelessWidget rather than a method. This is because extracting it as a StatelessWidget allows you to separate the BuildContext, preventing the use of shared context in the widget tree.

If the BuildContext is not separated, widgets that are unrelated to the state can be rebuilt together when a state change occurs in a different widget. Using StatelessWidget helps to minimize widget rebuilds.

### Naming the separated widgets
To create unique names, you can prepend the page name to the widget name:

ProductDetailHeader
ProductDescriptionView
ProductPriceInfoView

📝 However, one drawback of this naming convention is that the class names can become too long. A better alternative is to use the private access modifier.

```dart
part of '../product_detail_screen.dart';
  
class _Header extends StatelessWidget {  
  const _Header({Key? key}) : super(key: key);  
  
  @override  
  Widget build(BuildContext context) {  
    return Container(  
      height: 386,  
      decoration: BoxDecoration(  
        image: DecorationImage(  
            image: Image.asset(Assets.imagesProductImg0).image,  
            fit: BoxFit.fitHeight),  
      ),  
    );  
  }  
}
```

💡 By using the access modifier, you can specify a class name, preventing other pages from importing that header module, making widget modularization more reliable.

![image](https://github.com/YamamotoDesu/clean_ui_code_implementation/assets/47273077/d69dd91a-8c97-411b-95e0-c88486ecc346)
