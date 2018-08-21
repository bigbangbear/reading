> 一个使用 UILabel 实现段落样式的范例，主要是通过一个 NSParagraphStyle 的 headIndent 属性来完成整体段落缩进（首行除外）

### [Scalable bulleted lists with UILabel or UITextView](https://bendodson.com/weblog/2018/08/09/bulleted-lists-with-uilabel/)

![](https://bendodson.s3.amazonaws.com/weblog/2018/bulleted-list-scale.jpg)

#### 实现步骤

##### 步骤一

用数组连接，段落分割符号

```swift
let bullet = "•  "        
var strings = [String]()
strings.append("First line of your list")
strings.append("Second line of your list")
strings.append("etc")
strings = strings.map { return bullet + $0 }
```

##### 步骤二

为字符串设置显示属性

```swift
// 设置字体属性
var attributes = [NSAttributedStringKey: Any]()
attributes[.font] = UIFont.preferredFont(forTextStyle: .body)
attributes[.foregroundColor] = UIColor.darkGray
// 设置间距
let paragraphStyle = NSMutableParagraphStyle()
paragraphStyle.headIndent = (bullet as NSString).size(withAttributes: attributes).width
attributes[.paragraphStyle] = paragraphStyle
```

##### 步骤三

应用到 UILabel

```swift
// 设置换行符
let string = strings.joined(separator: "\n\n")
// 应用到 UILabel
label.attributedText = NSAttributedString(string: string, attributes: attributes)   
```