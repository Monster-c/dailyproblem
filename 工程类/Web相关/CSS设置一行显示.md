# CSS设置一行显示



```css

.view-text{
  /**
	思路：
	1.设置inline-block属相
	2.强制不换行
	3.固定高度
	4.隐藏超出部分
	5.显示“……”
  */
  display: inline-block;
  white-space: nowrap; 
  width: 100%; 
  overflow: hidden;
  text-overflow:ellipsis;
}
```

