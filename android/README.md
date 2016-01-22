
### 文件的命名
#### 类的命名
命名应该遵循[驼峰命名法](http://baike.baidu.com/link?url=36TNYWM87ZKQKN5r1RayLumvi7wqv3vmVcgi7eicJVD4VpbpNyMUp443RFJ4coFeosuNIg1TZny2p9fTTlpOva)
对于继承自 Android 组件的类来说，命名是应以改组件的名称结尾；例如： `SignInActivity`, `SignInFragment`, `ImageUploaderService`, `ChangePasswordDialog`。
#### Res 中文件的命名
资源文件应该以小写 + 下划线( _ )的格式命名。
##### 图片文件
以下是对于图片文件的命名习惯

| Asset Type   | Prefix            |        Example               |
|:--------------| :------------------|:-----------------------------|
| Action bar   | `ab_`             | `ab_stacked.9.png`          |
| Button       | `btn_`             | `btn_send_pressed.9.png`    |
| Dialog       | `dialog_`         | `dialog_top.9.png`          | 
| Divider      | `divider_`        | `divider_horizontal.9.png`  |
| Icon         | `ic_`              | `ic_star.png`               |
| Menu         | `menu_ `           | `menu_submenu_bg.9.png`     |
| Notification | `notifi_`    | `notifi_bg.9.png`     |
| Tabs         | `tab_`            | `tab_pressed.9.png`         |

对于图标的命名习惯

| Asset Type                      | Prefix             | Example                      |
| :--------------------------------| :----------------   | :---------------------------- | 
| Icons                           | `ic_`              | `ic_star.png`                |
| Launcher icons                  | `ic_launcher`      | `ic_launcher_calendar.png`   |
| Menu icons and Action Bar icons | `ic_menu`          | `ic_menu_archive.png`        |
| Status bar icons                | `ic_stat_notify`   | `ic_stat_notify_msg.png`     |
| Tab icons                       | `ic_tab`           | `ic_tab_recent.png`          |
| Dialog icons                    | `ic_dialog`        | `ic_dialog_info.png`         |

对于选择器状态的命名习惯

| State	       | Suffix          | Example                     |
|:--------------|:-----------------|:-----------------------------|
| Normal       | `_normal`       | `btn_order_normal.9.png`    |
| Pressed      | `_pressed`      | `btn_order_pressed.9.png`   |
| Focused      | `_focused`      | `btn_order_focused.9.png`   |
| Disabled     | `_disabled`     | `btn_order_disabled.9.png`  |
| Selected     | `_selected`     | `btn_order_selected.9.png`  |

##### 布局文件
布局文件应该和将要用于的 Android 组件的名称相匹配，但是这次应以组件的名称开头。例如， 如果我们为 `SignInActivity`,创建布局文件，那布局文件的名称就应该为 `activity_sign_in.xml`.

| Component        | Class Name             | Layout Name                   |
| ---------------- | ---------------------- | ----------------------------- |
| Activity         | `UserProfileActivity`  | `activity_user_profile.xml`   |
| Fragment         | `SignUpFragment`       | `fragment_sign_up.xml`        |
| Dialog           | `ChangePasswordDialog` | `dialog_change_password.xml`  |
| AdapterView item | ---                    | `item_person.xml`             |
| Partial layout   | ---                    | `partial_stats_bar.xml`       |

一个特殊的情况就是在为 Adapter 中的子项创建布局的时候， 例如， 显示 ListView 中的内容。在这种情况下，布局文件的前缀应该为 `item_`
应该注意到还有一个特殊情况的存在，那就是在创建一个布局中的其中一小块布局时，在这种情况下就应该使用前缀 `partial_`
##### menu 文件
与布局文件的命名的规则相似，menu 文件也应该和将要用于的 Android 组件的名称相匹配。例如，当我们在为 `UserActivity` 创建 menu 文件时，那 menu 文件的名称就应该是 `activity_user.xml`
命名规则是不把单词 `menu` 作为名称的一部分，因为这些文件已经存放在 `menu` 的文件下了。
##### 资源文件
在 `values` 文件夹中的资源文件在命名时应该为复数。例如， `strings.xml`, `styles.xml`, `colors.xml`, `dimens.xml`, `attrs.xml`
## 代码规范
### Java 语言的规范
#### 不要忽略异常的处理
永远不要编写出以下的代码
```Java
void setServerPort(String value) {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) { }
}
```
不要认为你的代码永远不会触发此类的异常或者不足以处理,或者如以上代码似的,在你的代码里留下缺口让别人在以后帮你来填上.你必须按照规范来捕获每一个异常.也可以查看 [Android 官方的文档描述](https://source.android.com/source/code-style.html#dont-ignore-exceptions).
#### 不要捕获通用的异常
永远不要编写以下的代码
```Java
try {
    someComplicatedIOFunction();        // may throw IOException
    someComplicatedParsingFunction();   // may throw ParsingException
    someComplicatedSecurityFunction();  // may throw SecurityException
    // phew, made it all the way
} catch (Exception e) {                 // I'll just catch all exceptions
    handleError();                      // with one generic handler!
}
```
具体原因可以查看 [Android 官方文档描述](https://source.android.com/source/code-style.html#dont-catch-generic-exception)
#### 不要使用 finalizers
不要使用 finalizers ([不知道 finalize 的可以查看这里](http://stackoverflow.com/questions/2506488/when-is-the-finalize-method-called-in-java)). 即便 finalizer 最终都是会被调用的但是什么时候会别调用是没有保证的. 在大多数的情况下,你可以通过好的异常捕获机制来取代 finalizer. 如果在某种情况下你必须要使用到它, 定义一个 `close()` 方法(或者类似的)然后准确的说明一下什么时候该方法会被调用到.
#### 规范的引用
这是一个不好的引用编写: `import foo.*;`
这是一个合格的引用编写: `import foo.Bar;`
更多信息查看[这里](https://source.android.com/source/code-style.html#fully-qualify-imports)

### Java 风格规范
####  变量的定义与命名
变量应该定义在文件头部的位置,并且应该遵循以下的命名规则.
- Private, 非静态变量应该已 **m** 开头命名
- Private, 静态变量应该已 **s** 开头命名
- 其余的变量应该已小写字母开头
- 静态的常量应该都是以大写字母加下划线的格式命名. 例如, `ALL_CAPS_WITH_UNDERSCORES`.
例子如下
```Java
public class MyClass {
    public static final int SOME_CONSTANT = 42;
    public int publicField;
    private static MyClass sSingleton;
    int mPackagePrivate;
    private int mPrivate;
    protected int mProtected;
}
```
#### 将英文的缩略词也看做成一个单词
| Good           | Bad            |
| -------------- | -------------- |
| `XmlHttpRequest` | `XMLHTTPRequest` |
| `getCustomerId`  | `getCustomerID`  |
| `String url`     | `String URL`     |
| `long id`        | `long ID`        |
#### 使用空格来进行缩进
使用**4 个空格**来进行代码块的缩进
```Java
if (x == 1) {
    x++;
}
```
使用** 8 个空格**来进行代码的换行
```Java
Instrument i =
        someLongExpression(that, wouldNotFit, on, one, line);
```
#### 大括号的使用规范
左大括号应该跟在其之前的代码在同一行上
```Java
class MyClass {
    int func() {
        if (something) {
            // ...
        } else if (somethingElse) {
            // ...
        } else {
            // ...
        }
    }
}
```
如果条件语句跟结果语句正好可以在同一行上并且其长度也小于同一行的最大长度限制, 则可以省略大括号
例如
```Java
if (condition) body();
```
错误的范例
```Java
if (condition)
    body();  // bad!
```
#### 注解
##### 注解的应用
根据 Android 官方文档, 在 Java 中对于一些预先确定的注解的标准应用如下
- `@Override`: 该注解**必须用与**任何时候想要重写或者实现父类的某个方法的时候. 例如,当你使用了 `@inheritdocs` 标签,并且是源于一个类而并不是接口的时候,你必须同时也在此方法上加上 `@Override` 标签.
- `@SuppressWarnings`: 该标签只有在遇到无法忽略的警告的条件下才可以使用. 如果一个警告符合"无法忽略掉"的条件时,该标签是必须需要被使用的,为的是保证所有的警告都能反映出代码中实际存在的问题.
更多关于注解的规范请参考[这里](http://source.android.com/source/code-style.html#use-standard-java-annotations)
##### 注解格式
- 类,方法和构造函数: 当注解被用于类,方法和构造函数的时候,应该将注解位于注释的下面,并且每个注解作为一行的形式.如下所示
```Java
/* This is the documentation block about the class */
@AnnotationA
@AnnotationB
public class MyAnnotatedClass { }
```
- 对象: 注解应该与对象保持在同一行,除非该行达到了最大字符的限制数.
```Java
@Nullable @Mock DataManager mDataManager;
```
#### 限制变量的作用域
局部变量的作用域应该保持到最小.这样可以增加代码的可读性和维护性,并且降低出错的概率.
局部变量应该尽量在它第一次被调用的时候被声明出来.而且声明局部变量时应该初始化该变量,如果你还没有足够的信息来初始化该变量,那就应该推迟声明直到拥有足够的信息来初始化此变量的时候.更多信息可查看[这里](https://source.android.com/source/code-style.html#limit-variable-scope)
#### 日志的规范
请使用公司通用的 `LogUtil` 类来取代 Android 原生的 `Log` 类来打印日志.
#### 类成员排列的规范
这部分没有强制的要求,但是使用一种合乎逻辑并且常用的方式来排列类成员,可以增强代码的可读性
- 常量
- 对象
- 构造函数
- 重写和回调函数(包括公有的和私有的)
- 公有函数
- 私有函数
- 内部类及内部接口
 
例如:
```Java
public class Child extends Parent {

    private static final int CONSTANT = 1;

    private String mName;
    private int mAge;
    
    public Child(String name, int age) {
        mName = name;
        mAge = age;
    }

    @Override
    public void changeName() {
        ...
    }
    
    public void setName(String name) {
            mName = name;
    }

    private void setSomething() {
        ...
    }

    static class AnInnerClass {

    }
}
```
如果你的类是继承自**Android 的组件**,例如 Activity 和 Fragment, 比较好的习惯是按照该组件的生命周期来重写方法.例如,如果你有一个 Activity 实现了 `onCreate()`, `onDestroy()`, `onPause()` 和 `onResume()`,则正确的顺序为:
```Java
public class MainActivity extends Activity {

    //Order matches Activity lifecycle
    @Override
    public void onCreate() {}

    @Override
    public void onResume() {}

    @Override
    public void onPause() {}

    @Override
    public void onDestroy() {}

}
```
#### 函数中参数的顺序
在编写 Android 的代码时,函数中含有参数 `Context` 是非常常见的.如果遇到这种情况,那么必须将**Context**作为第一个参数.
对应的**回调接口**应该永远作为函数的最后一个参数
例如:
```Java
// Context always goes first
public User loadUser(Context context, int userId);

// Callbacks always go last
public void loadUserAsync(Context context, int userId, UserCallback callback);
```
#### 字符串常量的命名
Android SDK 中包含很多需要键值对的元素例如, `SharedPreferences`, `Bundle` 和 `Intent`.即使在写一个很小的 app 应用时,也会产生很多字符串常量.
当使用以上组件的时候,你**必须**将字符串定义为 `static final`,并且它们的前缀应该遵循以下的命名规则:

| Element            | Field Name Prefix |
| -----------------  | ----------------- |
| SharedPreferences  | `PREF_`             |
| Bundle             | `BUNDLE_`           |
| Fragment Arguments | `ARGUMENT_`         |
| Intent Extra       | `EXTRA_`            |
| Intent Action      | `ACTION_`           |
虽然 `Fragment.getArguments()` 返回的也是一个 Bundle,但是为了用于区分,所以使用 `ARGUMENT_` 作为其前缀.
```Java
// Note the value of the field is the same as the name to avoid duplication issues
static final String PREF_EMAIL = "PREF_EMAIL";
static final String BUNDLE_AGE = "BUNDLE_AGE";
static final String ARGUMENT_USER_ID = "ARGUMENT_USER_ID";

// Intent-related items use full package name as value
static final String EXTRA_SURNAME = "com.myapp.extras.EXTRA_SURNAME";
static final String ACTION_OPEN_USER = "com.myapp.action.ACTION_OPEN_USER";
```
#### Fragment 和 Activity 中的参数
当数据通过 `Intent` 或 `Bundle` 传递给 `Fragment` 和 `Activity`的时候, Key 的命名必须要遵循以上的命名规范.
当 `Activity` 或 `Fragment` 需要接受参数的时候, 需要创建一个 `public static` 的方法来创建与之相关的 `Intent` 或 `Fragment`.
Activity 的情况下,通常将方法命名为 `getStartIntent()`:
```Java
public static Intent getStartIntent(Context context, User user) {
    Intent intent = new Intent(context, ThisActivity.class);
    intent.putParcelableExtra(EXTRA_USER, user);
    return intent;
}
```
Fragment 的情况下,通常将方法命名为 `newInstance()`,通过传入的参数来创建 Fragment
```Java
public static UserFragment newInstance(User user) {
    UserFragment fragment = new UserFragment;
    Bundle args = new Bundle();
    args.putParcelable(ARGUMENT_USER, user);
    fragment.setArguments(args)
    return fragment;
}
```
**注意 1**:此类方法应该声明在类的前部, `onCreate()` 方法之前
**注意 2**:如果我们已经声明了以上的方法,那么为 Intent 或 Bundle 声明的 `Key` 应该是 `private`, 因为不需要类之外来使用.
#### 行长度的限制
一行代码的长度不应该超过** 100 个字符**,如果一行代码过长,通常有如下两种方法来减少代码的长度:
- 提取出一个`局部变量`或`方法`**(推荐)**
- 通过换行将一行代码变为多行

有两种例外的情况可以允许行代码超过 100 个字符
- 无法换行的代码,例如: 网址 URL
- `package` 和 `import` 的声明

##### 换行的规范
这里也没有强制行的规范,但是有几条比较通用的规范希望可以遵守
**运算符**
当要在运算符处进行换行的时候,换行应该在运算符之前,例如:
```Java
int longName = anotherVeryLongVariable + anEvenLongerOne - thisRidiculousLongOne
        + theFinalOne;
```
但是以上规则不适用于 `=` 运算符,换行应该在等号运算符之后,例如:
```Java
int longName =
        anotherVeryLongVariable + anEvenLongerOne - thisRidiculousLongOne + theFinalOne;
```
**方法链的情况下**
当多个方法在同一行组合在一起成为方法链的时候.例如, Builder 模式下,每一个方法应该独立成一行,并换行应该在 `.` 之前.
```Java
Picasso.with(context).load("http://ribot.co.uk/images/sexyjoe.jpg").into(imageView);
```
```Java
Picasso.with(context)
        .load("http://ribot.co.uk/images/sexyjoe.jpg")
        .into(imageView);
```
**多个参数的情况下**
当一个函数多个参数并且参数过长时,我们应该在 `,` 后进行换行.
```Java
loadPicture(context, "http://ribot.co.uk/images/sexyjoe.jpg", mImageViewProfilePicture, clickListener, "Title of the picture");
```
```Java
loadPicture(
        context,
        "http://ribot.co.uk/images/sexyjoe.jpg",
        mImageViewProfilePicture,
        clickListener,
        "Title of the picture"
   );
```
#### 针对于 RxJava 的规范
Rx 的方法链同样需要换行.每一个操作必须独立为一行,而且换行应该在 `.` 之前.
```Java
public Observable<Location> syncLocations() {
    return mDatabaseHelper.getAllLocations()
            .concatMap(new Func1<Location, Observable<? extends Location>>() {
                @Override
                 public Observable<? extends Location> call(Location location) {
                     return mRetrofitService.getLocation(location.id);
                 }
            })
            .retry(new Func2<Integer, Throwable, Boolean>() {
                 @Override
                 public Boolean call(Integer numRetries, Throwable throwable) {
                     return throwable instanceof RetrofitError;
                 }
            });
}
```
## XML 的规范
### 使用自结束标签
当一个 XML 里的元素内没有其他元素时,应该使用自结束标签
这是正确的:
```xml
<TextView
    android:id="@+id/text_view_profile"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />
```
这是错误的:
```xml
<!-- Don\'t do this! -->
<TextView
    android:id="@+id/text_view_profile"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" >
</TextView>
```
### 资源的命名
资源的 ID 和名称都应该是**小写 + 下划线**的格式
#### ID 的命名
ID 应该已控件的名称作为前缀来命名.例如:

| Element            | Prefix            |
| -----------------  | ----------------- |
| `TextView`           | `text_`             |
| `ImageView`          | `image_`            |
| `Button`             | `button_`           |
| `Menu`               | `menu_`             |
ImageView 例子:
```xml
<ImageView
    android:id="@+id/image_profile"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />

```
Menu 例子:
```xml
<menu>
    <item
        android:id="@+id/menu_done"
        android:title="Done" />
</menu>
```
##### 字符串
字符串的名字应该已一个可以标明其所属领域的前缀来做开头. 例如, `registration_email_hint` 或 `registration_name_hint`.如果一个字符串不属于任何的领域,那应该遵循以下规则:

| Prefix             | Description                           |
| -----------------  | --------------------------------------|
| `error_`             | An error message                      |
| `msg_`               | A regular information message         |
| `title_`             | A title, i.e. a dialog title          |
| `action_`            | An action such as "Save" or "Create"  |
#### Style 和 Theme
不同于其他的资源命名规范, Style 中的名字应该遵循[驼峰命名法](http://baike.baidu.com/link?url=36TNYWM87ZKQKN5r1RayLumvi7wqv3vmVcgi7eicJVD4VpbpNyMUp443RFJ4coFeosuNIg1TZny2p9fTTlpOva)
#### Color
color 中颜色的命名应该遵循**小写 + 下划线**的格式
### 提供 Android 性能的编码规范
#### 不要在 Android 程序里使用 enum
虽然使用 enum 很方便,但是会比使用静态变量产生多于两倍的内存消耗,所以 Android 官方强烈建议不要在Android程序里面使用到enum.
使用 Android Typedef Annotations 可以代替 enum, 具体的使用发放请参考[这里](http://tools.android.com/tech-docs/support-annotations)
#### 关于数组遍历
```Java
static class Foo {
    int mSplat;
}

Foo[] mArray = ...

// 最慢,消耗最多
public void zero() {
    int sum = 0;
    for (int i = 0; i < mArray.length; ++i) {
        sum += mArray[i].mSplat;
    }
}

public void one() {
    int sum = 0;
    Foo[] localArray = mArray;
    int len = localArray.length;

    for (int i = 0; i < len; ++i) {
        sum += localArray[i].mSplat;
    }
}

// 推荐
public void two() {
    int sum = 0;
    for (Foo a : mArray) {
        sum += a.mSplat;
    }
}
```
`zero()` 是最慢的方法,因为 JIT 还不能对当数组进行遍历时每次都要去获得数组的长度进行优化.
`one()` 更快一点, 因为它所有的数据都拿出来存放在局部变量里,避免了查找.只有提供了数组的长度对性能有了一定的提升
`two()` 在没有 JIT 的设备里是最快的,在有 JIT 的设备里于**one()**难已分上线.它使用了 Java 1.5 版本中的增强版语法
 所以应该默认使用**增强版的 for** 循环.