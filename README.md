# Keyboard 防京东，支付宝密码键盘和密码输入框
####效果图：
![image](https://github.com/GitPhoenix/Keyboard/blob/master/art/keyboard.gif)
####具体应用：

* 布局文件中
```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
                android:layout_width="match_parent"
                android:layout_height="match_parent">

    <com.github.phoenix.widget.PayEditText
        android:id="@+id/PayEditText_pay"
        android:layout_width="match_parent"
        android:layout_marginTop="20dp"
        android:paddingLeft="12dp"
        android:layout_alignParentTop="true"
        android:paddingRight="12dp"
        android:layout_height="48dp"/>

    <com.github.phoenix.widget.Keyboard
        android:id="@+id/Keyboard_pay"
        android:layout_alignParentBottom="true"
        android:layout_width="match_parent"
        android:layout_height="300dp"/>

</RelativeLayout>
```

* 代码中
```
//键
private static final String[] KEY = new String[] {
            "1", "2", "3",
            "4", "5", "6",
            "7", "8", "9",
            "<<", "0", "完成"
    };
//设置键盘
keyboard.setKeyboardKeys(KEY);
//键盘键的点击事件
keyboard.setOnClickKeyboardListener(new Keyboard.OnClickKeyboardListener() {
    @Override
    public void onKeyClick(int position, String value) {
        if (position < 11 && position != 9) {
            payEditText.add(value);
        } else if (position == 9) {
            payEditText.remove();
        }else if (position == 11) {
            //当点击d键盘上的完成时候，也可以通过payEditText.getText()获取密码，此时不应该注册OnInputFinishedListener接口
            Toast.makeText(getApplication(), "您的密码是：" + payEditText.getText(), Toast.LENGTH_SHORT).show();
            finish();
        }
    }
});

//当密码输入完成时的回调
payEditText.setOnInputFinishedListener(new PayEditText.OnInputFinishedListener() {
    @Override
    public void onInputFinished(String password) {
        Toast.makeText(getApplication(), "您的密码是：" + password, Toast.LENGTH_SHORT).show();
  }
});
```

* 键盘样式可以根据BaseAdapter的getItemViewType进行调整
