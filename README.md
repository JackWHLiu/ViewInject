1、自动注入视图（Inject Layout）
（1）建议Activity继承com.lwh.jackknife.app.Activity,Fragment继承com.lwh.jackknife.app.Fragment，也可自定义。
（2）保证布局的xml文件跟Activity和Fragment的Java类的命名遵循一定的映射关系（Java类名必须以Activity或Fragment结尾）。
使用“前缀_业务名称.xml”，如activity_main.xml。例如：MainActivity.java映射的xml文件名就为activity_main.xml，TTSFragment.java映射的xml文件名就为fragment_t_t_s.xml。 Java类以大写字母分隔单词，xml以下划线分隔单词。

2、自动绑定控件（Inject Views）
（1）不使用注解
直接在Activity或Fragment声明控件（View及其子类）为成员变量，不加任何注解。它会以这个View的名字来绑定该控件在xml中的id的value，即@+id/后指定的内容。`

（2）使用@ViewInject
优先级比不加注解高，简单的说，加上这个注解就不会使用默认的使用成员属性名来对应xml的控件id的方式，而是使用该注解指定的id与xml的控件id绑定。

（3）使用@ViewIgnore
优先级最高，加上该注解，jackknife会直接跳过该控件的自动注入。一般使用在使用Java代码new出来的控件提取到全局的情况。也可以在ViewStub懒加载布局的时候使用。

3、自动注册事件（Inject Events）
创建一个自定义的事件注解，在这个注解上配置@EventBase，并使用在你要实际回调的方法上，注意保持参数列表跟原接口的某个回调方法的参数列表保持一致。在jackknife-annotations-ioc中也提供了常用的事件的注解，比如@OnClick。