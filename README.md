# photo

[![pub package](https://img.shields.io/pub/v/photo.svg)](https://pub.dartlang.org/packages/photo)
![Hex.pm](https://img.shields.io/hexpm/l/plug.svg)

image picker, multi picker

support ios icloud

support video

use flutter as ui

if you want to build custom ui, you just need api to make custom ui. to use [photo_manager](https://github.com/CaiJingLong/flutter_photo_manager)

## screenshot

![image](https://github.com/CaiJingLong/some_asset/blob/master/image_picker1.gif)

## API incompatibility

API incompatibility

because support video, so the ImagePathEntity and ImageEntity rename to AssetPathEntity and AssetEntity.

so PhotoPicker.pickImage return type will change to List<AssetEntity>

## install

```yaml
dependencies:
  photo: ^0.1.3
```

## import

```dart
import 'package:photo/photo.dart';
import 'package:photo_manager/photo_manager.dart';
```

## use

```dart
void _pickImage() async {
    List<AssetEntity> imgList = await PhotoPicker.pickImage(
      context: context,
      // BuildContext requied

      /// The following are optional parameters.
      themeColor: Colors.green,
      // the title color and bottom color
      padding: 1.0,
      // item padding
      dividerColor: Colors.grey,
      // divider color
      disableColor: Colors.grey.shade300,
      // the check box disable color
      itemRadio: 0.88,
      // the content item radio
      maxSelected: 8,
      // max picker image count
      provider: I18nProvider.chinese,
      // i18n provider ,default is chinese. , you can custom I18nProvider or use ENProvider()
      rowCount: 5,
      // item row count
      textColor: Colors.white,
      // text color
      thumbSize: 150,
      // preview thumb size , default is 64
      sortDelegate: SortDelegate.common,
      // default is common ,or you make custom delegate to sort your gallery
      checkBoxBuilderDelegate: DefaultCheckBoxBuilderDelegate(
        activeColor: Colors.white,
        unselectedColor: Colors.white,
      ), // default is DefaultCheckBoxBuilderDelegate ,or you make custom delegate to create checkbox

      loadingDelegate:
          this, // if you want to build custom loading widget,extends LoadingDelegate [see example/lib/main.dart]
    );

```

## whole example

you can see [github](https://github.com/caijinglong/flutter_photo/blob/master/example/) [main.dart](https://github.com/caijinglong/flutter_photo/blob/master/example/lib/main.dart)

## about android

### glide

android use glide to create image thumb, version is 4.8.0

if you other android library use the library, and version is not same, then you need edit your android project's build.gradle

```gradle
rootProject.allprojects {

    subprojects {
        project.configurations.all {
            resolutionStrategy.eachDependency { details ->
                if (details.requested.group == 'com.github.bumptech.glide'
                        && details.requested.name.contains('glide')) {
                    details.useVersion "4.8.0"
                }
            }
        }
    }

}
```

if you use the proguard

see the [github](https://github.com/bumptech/glide#proguard)

## about ios

Because the album is a privacy privilege, you need user permission to access it. You must to modify the `Info.plist` file in Runner project.

like next

```plist
	<key>NSPhotoLibraryUsageDescription</key>
    <string>App need your agree, can visit your album</string>
```

xcode like image
![in xcode](https://github.com/CaiJingLong/some_asset/blob/master/flutter_photo2.png)
