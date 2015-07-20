Android测试分为了Instrumentation Test和JUnit Test

### Instrumentation
一般用于和Android组件相关的测试，测试类位于src/androidTest/java下,AS中默认打开

### JUnit Test
一般为传统的JUnit Test，测试类位于src/test/java下
在AS中如果需要使用JUnit Test，需要
1. 在Settings-->Gradle-->Experimental中，勾选 Enable Unit Testing support
2. 在对应Module的build.gradle文件的dependencies中加入引用声明`testCompile 'junit:junit:4.12'`

Instrumentation和JUnit可以在Build Variants面板中切换。

## 测试框架

### Ref:
[1]: [Testing Fundamentals](http://developer.android.com/tools/testing/testing_android.html)
[2]: [Unit testing support](http://tools.android.com/tech-docs/unit-testing-support)
[3]: [Gradle Plugin Samples 之 Gradle Unit Test](http://ask.android-studio.org/?/article/44)